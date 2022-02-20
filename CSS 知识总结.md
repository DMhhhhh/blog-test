# Critical Rendering Path关键渲染路径

The Critical Rendering Path is the sequence of steps the browser goes
through to convert the HTML, CSS, and JavaScript into pixels on the
screen. **关键渲染路径**是浏览器将 HTML，CSS 和 JavaScript
转换为屏幕上的像素所经历的步骤序列。

## Constructing the Object Model构建对象模型

Before the browser can render the page, it needs to construct the DOM
and CSSOM trees. As a result, we need to ensure that we deliver both the
HTML and CSS to the browser as quickly as possible.
浏览器渲染页面前需要先构建 DOM 和 CSSOM 树。因此，我们需要确保尽快将
HTML 和 CSS 都提供给浏览器。

-   Bytes → characters → tokens → nodes → object model.

    字节 → 字符 → 令牌 → 节点 → 对象模型。

-   HTML markup is transformed into a Document Object Model (DOM); CSS
    markup is transformed into a CSS Object Model (CSSOM).

    HTML 标记转换成文档对象模型 (DOM)；CSS 标记转换成 CSS 对象模型

-   DOM and CSSOM are independent data structures.

    DOM 和 CSSOM 是独立的数据结构。

-   Chrome DevTools Timeline allows us to capture and inspect the
    construction and processing costs of DOM and CSSOM.

    Chrome DevTools Timeline 让我们可以捕获和检查 DOM 和 CSSOM的构建和处理开销。

### Document Object Model 文档对象模型(DOM)
![avatar](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/images/full-process.png)

1.  **Conversion:** The browser reads the raw bytes of HTML off the disk
    or network, and translates them to individual characters based on
    specified encoding of the file (for example, UTF-8).

    **转换**:浏览器从磁盘或网络读取HTML的原始字节，并根据文件的指定编码（例如UTF-8）将它们转换成各个字符。

2.  **Tokenizing:** The browser converts strings of characters into
    distinct tokens---as specified by the [[W3C HTML5
    standard]](http://www.w3.org/TR/html5/); for example,
    \"\<html\>\", \"\<body\>\"---and other strings within angle
    brackets. Each token has a special meaning and its own set of rules.

    **令牌化**:浏览器将字符串转换成 [W3C HTML5标准](http://www.w3.org/TR/html5/)规定的各种令牌，例如，"\<html\>"、"\<body\>"，以及其他尖括号内的字符串。每个令牌都具有特殊含义和一组规则。

3.  **Lexing:** The emitted tokens are converted into \"objects,\" which
    define their properties and rules.

    **词法分析**:发出的令牌转换成定义其属性和规则的"对象"。

4.  **DOM construction:** Finally, because the HTML markup defines
    relationships between different tags (some tags are contained within
    other tags) the created objects are linked in a tree data structure
    that also captures the parent-child relationships defined in the
    original markup: the *HTML* object is a parent of the *body* object,
    the *body* is a parent of the *paragraph* object, and so on. DOM

    **构建**:最后，由于HTML标记定义不同标记之间的关系（一些标记包含在其他标记内），创建的对象链接在一个树数据结构内，此结构也会捕获原始标记中定义的父项-子项关系: *HTML* 对象是 *body* 对象的父项，*body* 是 *paragraph* 对象的父项，依此类推。

Every time the browser processes HTML markup, it goes through all of the
steps above: convert bytes to characters, identify tokens, convert
tokens to nodes, and build the DOM tree. This entire process can take
some time, especially if we have a large amount of HTML to process.
浏览器每次处理HTML标记时，都会完成以上所有步骤:
将字节转换成字符，确定令牌，将令牌转换成节点，然后构建DOM树。这整个流程可能需要一些时间才能完成，有大量HTML需要处理时更是如此。

### CSS Object Model CSS对象模型(CSSOM)

As with HTML, we need to convert the received CSS rules into something
that the browser can understand and work with. Hence, we repeat the HTML
process, but for CSS instead of HTML:

与处理HTML时一样，我们需要将收到的CSS规则转换成某种浏览器能够理解和处理的东西。因此，我们会重复HTML过程，不过是为CSS而不是
HTML:
![avatar](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/images/cssom-construction.png)

The CSS bytes are converted into characters, then tokens, then nodes,
and finally they are linked into a tree structure known as the \"CSS
Object Model\" (CSSOM):

CSS字节转换成字符，接着转换成令牌和节点，最后链接到一个称为"CSS对象模型"(CSSOM)的树结构内:
![avatar](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/images/cssom-tree.png)

Also, note that the above tree is not the complete CSSOM tree and only
shows the styles we decided to override in our stylesheet. Every browser
provides a default set of styles also known as \"user agent
styles\"---that's what we see when we don't provide any of our own---and
our styles simply override these defaults.

还请注意，以上树并非完整的 CSSOM
树，它只显示了我们决定在样式表中替换的样式。每个浏览器都提供一组默认样式（也称为"User
Agent
样式"），即我们不提供任何自定义样式时所看到的样式，我们的样式只是替换这些默认样式（例如[默认
IE 样式](http://www.iecss.com/)）。

## Render-tree Construction, Layout, and Paint渲染树构建、布局及绘制

The CSSOM and DOM trees are combined into a render tree, which is then
used to compute the layout of each visible element and serves as an
input to the paint process that renders the pixels to screen. Optimizing
each of these steps is critical to achieving optimal rendering
performance.

CSSOM 树和 DOM
树合并成渲染树，然后用于计算每个可见元素的布局，并输出给绘制流程，将像素渲染到屏幕上。优化上述每一个步骤对实现最佳渲染性能至关重要。

-   The DOM and CSSOM trees are combined to form the render tree.

    DOM树与CSSOM树合并后形成渲染树。

-   Render tree contains only the nodes required to render the page.

    渲染树只包含渲染网页所需的节点。

-   Layout computes the exact position and size of each object.

    布局计算每个对象的精确位置和大小。

-   The last step is paint, which takes in the final render tree and
    renders the pixels to the screen.

     最后一步是绘制，使用最终渲染树将像素渲染到屏幕上。

### Render-tree Construction渲染树构建 

First, the browser combines the DOM and CSSOM into a \"render tree,\"
which captures all the visible DOM content on the page and all the CSSOM
style information for each node.第一步是让浏览器将 DOM 和 CSSOM
合并成一个"渲染树"，网罗网页上所有可见的 DOM 内容，以及每个节点的所有CSSOM 样式信息。
![avatar](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/images/render-tree-construction.png)

To construct the render tree, the browser roughly does the
following为构建渲染树，浏览器大体上完成了下列工作:

1.  Starting at the root of the DOM tree, traverse each visible node. 从
    DOM 树的根节点开始遍历每个可见节点。

    -   Some nodes are not visible (for example, script tags, meta tags,
        and so on), and are omitted since they are not reflected in the
        rendered output.
        某些节点不可见（例如脚本标记、元标记等），因为它们不会体现在渲染输出中，所以会被忽略。

    -   Some nodes are hidden via CSS and are also omitted from the
        render tree; for example, the span node\-\--in the example
        above\-\--is missing from the render tree because we have an
        explicit rule that sets the \"display: none\" property on it.
        某些节点通过 CSS 隐藏，因此在渲染树中也会被忽略，例如，上例中的
        span
        节点\-\--不会出现在渲染树中，\-\--因为有一个显式规则在该节点上设置了"display:
        none"属性。

2.  For each visible node, find the appropriate matching CSSOM rules and
    apply them. 对于每个可见节点，为其找到适配的 CSSOM 规则并应用它们。

3.  Emit visible nodes with content and their computed styles.
    发射可见节点，连同其内容和计算的样式。

### Layout 布局

With the render tree in place, we can proceed to the \"layout\" stage.Up
to this point we\'ve calculated which nodes should be visible and their
computed styles, but we have not calculated their exact position and
size within
the [viewport](https://developers.google.com/web/fundamentals/design-and-ux/responsive#set-the-viewport) of
the device\-\--that\'s the \"layout\" stage, also known as \"reflow.\"
有了渲染树，我们就可以进入"布局"阶段。到目前为止，我们计算了哪些节点应该是可见的以及它们的计算样式，但我们尚未计算它们在设备[视口](https://developers.google.com/web/fundamentals/design-and-ux/responsive#set-the-viewport)内的确切位置和大小\-\--这就是"布局"阶段，也称为"自动重排"。

To figure out the exact size and position of each object on the page,
the browser begins at the root of the render tree and traverses
it.为弄清每个对象在网页上的确切大小和位置，浏览器从渲染树的根节点开始进行遍历。

The output of the layout process is a \"box model,\" which precisely
captures the exact position and size of each element within the
viewport: all of the relative measurements are converted to absolute
pixels on the screen.
布局流程的输出是一个"盒模型"，它会精确地捕获每个元素在视口内的确切位置和尺寸:
所有相对测量值都转换为屏幕上的绝对像素。

### Painting 绘制

Finally, now that we know which nodes are visible, and their computed
styles and geometry, we can pass this information to the final stage,
which converts each node in the render tree to actual pixels on the
screen. This step is often referred to as \"painting\" or
\"rasterizing.\"最后，既然我们知道了哪些节点可见、它们的计算样式以及几何信息，我们终于可以将这些信息传递给最后一个阶段:
将渲染树中的每个节点转换成屏幕上的实际像素。这一步通常称为"绘制"或"栅格化"。

## 总结

Here\'s a quick recap of the browser\'s
steps下面简要概述了浏览器完成的步骤:

1.  Process HTML markup and build the DOM tree.

    处理 HTML 标记并构建 DOM 树。

2.  Process CSS markup and build the CSSOM tree.

    处理 CSS 标记并构建 CSSOM 树。

1.  Combine the DOM and CSSOM into a render tree.

    将 DOM 与 CSSOM 合并成一个渲染树。

2.  Run layout on the render tree to compute geometry of each node.

    根据渲染树来布局，以计算每个节点的几何信息。

3.  Paint the individual nodes to the screen.

    将各个节点绘制到屏幕上。

参考：<https://developers.google.com/web/fundamentals/performance/critical-rendering-path/constructing-the-object-model>

<https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-tree-construction>

# transition

transition可以为一个元素在不同状态之间切换的时候定义不同的过渡效果。比如在不同的伪元素之间切换，像是 [:hover](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:hover)，[:active](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:active) 或者通过
JavaScript 实现的状态变化。

## [语法](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition#%E8%AF%AD%E6%B3%95)

```css
/\* Apply to 1 property \*/

/\* property name \| duration \*/

transition: margin-right 4s;

/\* property name \| duration \| delay \*/

transition: margin-right 4s 1s;

/\* property name \| duration \| timing function \*/

transition: margin-right 4s ease-in-out;

/\* property name \| duration \| timing function \| delay \*/

transition: margin-right 4s ease-in-out 1s;

/\* Apply to 2 properties \*/

transition: margin-right 4s, color 1s;

/\* Apply to all changed properties \*/

transition: all 0.5s ease-out;
```

# animation

[CSS](https://developer.mozilla.org/zh-CN/docs/Web/CSS) **animation** 属性是 [[animation-name]](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-name)，[[animation-duration]](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-duration), [[animation-timing-function]](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-timing-function)，[[animation-delay]](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-delay)，[[animation-iteration-count]](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-iteration-count)，[[animation-direction]](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-direction)，[[animation-fill-mode]](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-fill-mode) 和 [[animation-play-state]](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-play-state) 属性的一个简写属性形式。

## 语法

animation-name属性指定应用的一系列动画，每个名称代表一个由[[\@keyframes]](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@keyframes)定义的动画序列。

animation-duration属性指定一个动画周期的时长。

[CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) animation-timing-function属性定义CSS动画在每一动画周期中执行的节奏。可能值为一或多个 [\<timing-function\>](https://developer.mozilla.org/en-US/docs/Web/CSS/easing-function)

animation-delay [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS)属性定义动画于何时开始，即从动画应用在元素上到动画开始的这段时间的长度。

**animation-iteration-count** [CSS](https://developer.mozilla.org/en-US/CSS) 属性
  定义动画在结束前运行的次数 可以是1次 无限循环.

animation-direction CSS
属性指示动画是否反向播放，它通常在简写属性[[animation]](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation)中设定

[CSS](https://developer.mozilla.org/en-US/CSS) 属性 **animation-fill-mode** 设置CSS动画在执行之前和之后如何将样式应用于其目标。

**animation-play-state** [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) 属性定义一个动画是否运行或者暂停。可以通过查询它来确定动画是否正在运行。另外，它的值可以被设置为暂停和恢复的动画的重放。

恢复一个已暂停的动画，将从它开始暂停的时候，而不是从动画序列的起点开始在动画。

# \@keyframes

关键帧 **\@keyframes** [at-rule](https://developer.mozilla.org/zh-CN/docs/Web/CSS/At-rule) 规则通过在动画序列中定义关键帧（或waypoints）的样式来控制CSS动画序列中的中间步骤。和 [转换
transition](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Transitions) 相比，关键帧
keyframes 可以控制动画序列的中间步骤。

JavaScript 可以通过
CSS对象模型的 [CSSKeyframesRule] (en-US) 接口来访问 @keyframes。

要使用关键帧,
先创建一个带名称的 @keyframes 规则，以便后续使用 [[animation-name]](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-name) 属性将动画同其关键帧声明匹配。每个 @keyframes 规则包含多个关键帧，也就是一段样式块语句，每个关键帧有一个百分比值作为名称，代表在动画进行中，在哪个阶段触发这个帧所包含的样式。

可以按任意顺序列出关键帧百分比；它们将按照其应该发生的顺序来处理。

# CSS选择器

CSS选择器是CSS规则的第一部分。它是元素和其他部分组合起来告诉浏览器哪个HTML元素应当是被选为应用规则中的CSS属性值的方式。

## [选择器列表](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Selectors#%E9%80%89%E6%8B%A9%E5%99%A8%E5%88%97%E8%A1%A8)

如果你有多个使用相同样式的CSS选择器，那么这些单独的选择器可以被混编为一个"选择器列表"，这样，规则就可以应用到所有的单个选择器上了。可以将它们组合起来，在它们之间加上一个逗号，变为选择器列表。
```css
h1, .special {

color: blue;

}
```
## [类型选择器](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Selectors/Type_Class_and_ID_Selectors#%E7%B1%BB%E5%9E%8B%E9%80%89%E6%8B%A9%E5%99%A8)

**类型选择器**有时也叫做"标签名选择器*"*或者是"元素选择器"，因为它在文档中选择了一个HTML标签/元素的缘故。

## [全局选择器](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Selectors/Type_Class_and_ID_Selectors#%E5%85%A8%E5%B1%80%E9%80%89%E6%8B%A9%E5%99%A8)

全局选择器，是由一个星号（\*）代指的，它选中了文档中的所有内容（或者是父元素中的所有内容，比如，它紧随在其他元素以及邻代运算符之后的时候）。

## [类选择器](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Selectors/Type_Class_and_ID_Selectors#%E7%B1%BB%E9%80%89%E6%8B%A9%E5%99%A8)

类选择器以一个句点（.）开头，会选择文档中应用了这个类的所有物件。

## [ID选择器](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Selectors/Type_Class_and_ID_Selectors#id%E9%80%89%E6%8B%A9%E5%99%A8)

ID选择器开头为#而非句点，不过基本上和类选择器是同种用法。

## [用户行为伪类](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements#%E7%94%A8%E6%88%B7%E8%A1%8C%E4%B8%BA%E4%BC%AA%E7%B1%BB)

一些伪类只会在用户以某种方式和文档交互的时候应用。这些**用户行为伪类**，有时叫做**动态伪类**，表现得就像是一个类在用户和元素交互的时候加到了元素上一样。案例包括：

-   [:hover](https://developer.mozilla.org/en-US/docs/Web/CSS/:hover)------上面提到过，只会在用户将指针挪到元素上的时候才会激活，一般就是链接元素。

-   [:focus](https://developer.mozilla.org/en-US/docs/Web/CSS/:focus)------只会在用户使用键盘控制，选定元素的时候激活。

## 关系选择器

### [后代选择器](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Selectors/Combinators#%E5%90%8E%E4%BB%A3%E9%80%89%E6%8B%A9%E5%99%A8)

后代选择器------典型用单个空格（ ）字符------组合两个选择器，比如，第二个选择器匹配的元素被选择，如果他们有一个祖先（父亲，父亲的父亲，父亲的父亲的父亲，等等）元素匹配第一个选择器。选择器利用后代组合符被称作后代选择器。

### 子代关系选择器

子代关系选择器是个大于号（\>），只会在选择器选中直接子元素的时候匹配。继承关系上更远的后代则不会匹配。例如，只选中作为\<article\>的直接子元素的\<p\>元素：
```css
article \> p
```