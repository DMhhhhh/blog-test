# 简述 DOM 事件模型

浏览器的事件模型，就是通过监听函数（listener）对事件做出反应。事件发生后，浏览器监听到了这个事件，就会执行对应的监听函数。这是事件驱动编程模式（event-driven）的主要编程方式。

## 事件冒泡和捕捉 Event bubbling and capture

一个事件发生后，会在子元素和父元素之间传播（propagation）。这种传播分成三个阶段。

第一阶段：从window对象传导到目标节点（上层传到底层），称为"捕获阶段"（capture
phase）。

第二阶段：在目标节点上触发，称为"目标阶段"（target phase）。

第三阶段：从目标节点传导回window对象（从底层传回上层），称为"冒泡阶段"（bubbling
phase）。

这种三阶段的传播模型，使得同一个事件会在多个节点上触发。![图示
描述已自动生成](img/image1.png)

## 事件的代理delegation

由于事件会在冒泡阶段向上传播到父节点，因此可以把子节点的监听函数定义在父节点上，由父节点的监听函数统一处理多个子元素的事件。这种方法叫做事件的代理（delegation）。

```javascript
var ul = document.querySelector('ul');

ul.addEventListener('click', function (event) {

if (event.target.tagName.toLowerCase() === 'li') {

// some code

}

});
```

上面代码中，click事件的监听函数定义在\<ul\>节点，但是实际上，它处理的是子节点\<li\>的click事件。这样做的好处是，只要定义一个监听函数，就能处理多个子节点的事件，而不用在每个\<li\>节点上定义监听函数。而且以后再添加子节点，监听函数依然有效。

如果希望事件到某个节点为止，不再传播，可以使用事件对象的stopPropagation方法。
```javascript

// 事件传播到 p 元素后，就不再向下传播了

p.addEventListener('click', function (event) {

event.stopPropagation();

}, true);

// 事件冒泡到 p 元素后，就不再向上冒泡了

p.addEventListener('click', function (event) {

event.stopPropagation();

}, false);
```
上面代码中，stopPropagation方法分别在捕获阶段和冒泡阶段，阻止了事件的传播。

但是，stopPropagation方法只会阻止事件的传播，不会阻止该事件触发\<p\>节点的其他click事件的监听函数。也就是说，不是彻底取消click事件。

## Event 对象

事件发生以后，会产生一个事件对象，作为参数传给监听函数。浏览器原生提供一个Event对象，所有的事件都是这个对象的实例，或者说继承了Event.prototype对象。

### 实例方法

#### Event.preventDefault()

Event.preventDefault方法取消浏览器对当前事件的默认行为。比如点击链接后，浏览器默认会跳转到另一个页面，使用这个方法以后，就不会跳转了；再比如，按一下空格键，页面向下滚动一段距离，使用这个方法以后也不会滚动了。该方法生效的前提是，事件对象的cancelable属性为true，如果为false，调用该方法没有任何效果。

注意，该方法只是取消事件对当前元素的默认影响，不会阻止事件的传播。如果要阻止传播，可以使用stopPropagation()或stopImmediatePropagation()方法。
```javascript

// HTML 代码为

// <input type="checkbox" id="my-checkbox" />

var cb = document.getElementById('my-checkbox');

cb.addEventListener(

'click',

function (e){ e.preventDefault(); },

false

);
```

#### Event.stopPropagation()

stopPropagation方法阻止事件在 DOM
中继续传播，防止再触发定义在别的节点上的监听函数，但是不包括在当前节点上其他的事件监听函数。

#### Event.stopImmediatePropagation()

Event.stopImmediatePropagation方法阻止同一个事件的其他监听函数被调用，不管监听函数定义在当前节点还是其他节点。也就是说，该方法阻止事件的传播，比Event.stopPropagation()更彻底。

如果同一个节点对于同一个事件指定了多个监听函数，这些函数会根据添加的顺序依次调用。只要其中有一个监听函数调用了Event.stopImmediatePropagation方法，其他的监听函数就不会再执行了。
```javascript

function l1(e){

e.stopImmediatePropagation();

}

function l2(e){

console.log('hello world');

}

el.addEventListener('click', l1, false);

el.addEventListener('click', l2, false);
```

上面代码在el节点上，为click事件添加了两个监听函数l1和l2。由于l1调用了event.stopImmediatePropagation方法，所以l2不会被调用。
