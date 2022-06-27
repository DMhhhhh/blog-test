# JS函数的执行时机

## 1 解释为什么如下代码会打印 6 个 6

```javascript
for (i = 0; i < 6; i++) {
  setTimeout(() => {
    console.log(i);
  }, 0);
}
```

setTimeout是异步执行的，堆栈中碰到setTimeout会交给浏览器内核处理，等待setTimeout达到触发条件（即设定的时间），再返回给执行队列。简而言之，就是计时的这个操作是在浏览器端进行的，在计时完成后，将settimeout中的操作放入任务队列中。

任务队列可分为宏任务（macro-task）和微任务（micro-task）。XHR回调、事件回调（鼠标键盘事件）、setImmediate、setTimeout、setInterval、indexedDB数据库操作等I/O以及UI
rendering都属于宏任务（也有文章说UI
render不属于宏任务，目前还没有定论），process.nextTick、Promise.then、Object.observer(已经被废弃)、MutationObserver(html5新特性)属于微任务。注意进入到任务队列的是具体的执行任务的函数。比如上述例子setTimeout()中的timer函数。另外不同类型的任务会分别进入到他们所属类型的任务队列，比如所有setTimeout()的回调都会进入到setTimeout任务队列，所有then()回调都会进入到then队列。当前的整体代码我们可以认为是宏任务。事件循环从当前整体代码开始第一次事件循环，然后再执行队列中所有的微任务，当微任务执行完毕之后，事件循环再找到其中一个宏任务队列并执行其中的所有任务，然后再找到一个微任务队列并执行里面的所有任务，就这样一直循环下去。

### 分析代码

1.  首先执行整体代码，声明变量i=1

2.  代码继续执行到for循环进行第一次循环，发现是执行setTimeout()，此时新建一个setTimeout类型宏任务队列并派发这个setTimeout中的回调函数到该宏任务队列中去，然后继续执行for循环直到for循环中止，此时变量i值为6（for循环一共执行6次，setTimeout宏任务队列中有6个任务）

3.  第一轮事件循环的宏任务执行完成（整体代码可以看做宏任务）。此时宏任务队列中只有一个setTimeout类型的宏任务队列。此时第一轮事件循环完成。

4.  开始第二轮事件循环：执行setTimeout类型队列（宏任务队列）中的所有任务，它的作用就是打印变量i，此时变量i值为6，所以打印出6个6

5.  第二轮事件循环结束，全部代码执行完毕。

## 2 写出让上面代码打印 0、1、2、3、4、5 的方法

```javascript
for (let i = 0; i < 6; i++) {
  setTimeout(() => {
    console.log(i);
  }, 0);
}
```

## 3 除了使用 for let 配合，还有什么其他方法可以打印出 0、1、2、3、4、5

```javascript
for (var i = 0; i < 6; i++) {
  (function (i) {
    setTimeout(() => {
      console.log(i);
    }, 0);
  })(i);
}
```

**引入IIFE**

参考链接：<https://www.jianshu.com/p/3e482748369d>
