# JS语法入门

## 表达式&语句 Expression&Statement

表达式(expression)产生一个值，可以写在任何需要一个值的地方。而语句(statement)是一个行为，例如循环和条件语句，一个程序基本上就是一个语句序列。任何需要语句的地方，也可以写表达式，这样的语句是表达式语句。反过来却不行：你不能在需要表达式的时候使用语句，例如一个
if 语句不能作为函数的参数。

### 二者区别

1.  表达式一般都有值，语句可能有也可能没有

2.  语句一般会改变环境（声明、赋值）

### 注意

1.  1+2表达式的值为3

2.  add(1,2)表达式的值为函数的返回值

3.  console.log表达式的值为函数本身

4.  console.log(3)表达式的值为函数的返回值（undefined）

## 标识符 Identifier

代码中用来标识[变量](https://developer.mozilla.org/en-US/docs/Glossary/Variable)、[函数](https://developer.mozilla.org/zh-CN/docs/Glossary/Function)、或[属性 (en-US)](https://developer.mozilla.org/en-US/docs/Glossary/property)的字符序列。

### 规则

1.  第一个字符，可以是Unicode字母或\$或_或中文

2.  后面的字符，除了上面所说，还可以有数字

**注意**：变量名是标识符（如var \_ = 1; var \$ = 2 等）

## 条件语句Conditional Statement 

### If eles语句
语法

```javascript
if (表达式) {

语句

} else if (表达式) {

语句

} else {

语句

}
```

### 三元（条件）运算符 Ternary (Conditional) operator

**条件（三元）运算符**是
JavaScript 仅有的使用三个操作数的运算符。一个条件后面会跟一个问号（?），如果条件为 [truthy](https://developer.mozilla.org/zh-CN/docs/Glossary/Truthy) ，则问号后面的表达式
A 将会执行；表达式 A
后面跟着一个冒号（:），如果条件为 [falsy](https://developer.mozilla.org/zh-CN/docs/Glossary/Falsy) ，则冒号后面的表达式
B
将会执行。本运算符经常作为 [if](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else) 语句的简捷形式来使用。

语法


`（表达式）？语句：语句`


## 循环与迭代

### while 语句

一个 while
语句只要指定的条件求值为真（true）就会一直执行它的语句块。一个 while
语句看起来像这样：

```javascript
while (condition)

    statement
```

条件检测会在每次 statement 执行之前发生。如果条件返回为真， statement
会被执行并紧接着再次测试条件。如果条件返回为假，执行将停止并把控制权交回给
while 后面的语句。

### for 语句

一个 for 循环会一直重复执行，直到指定的循环条件为 false。 J一个 for
语句是这个样子的：

```javascript
for (\[initialExpression\]; \[condition\]; \[incrementExpression\])

    statement
```

当一个 for 循环执行的时候，会发生以下过程：

1.  如果有初始化表达式
    initialExpression，它将被执行。这个表达式通常会初始化一个或多个循环计数器，但语法上是允许一个任意复杂度的表达式的。这个表达式也可以声明变量。

2.  计算 condition 表达式的值。如果 condition 的值是
    true，循环中的语句会被执行。如果 condition 的值是 false，for
    循环终止。如果 condition 表达式整个都被省略掉了，condition
    的值会被认为是 true。

3.  循环中的 statement 被执行。如果需要执行多条语句，可以使用块（{ \...
    }）来包裹这些语句。

4.  如果有更新表达式 incrementExpression，执行更新表达式。

5.  回到步骤 2。

### Break语句

使用 break 语句来终止循环，switch， 或者是链接到 label 语句。

-   当你使用不带 label 的 break 时， 它会立即终止当前所在的
while，do-while，for，或者 switch 并把控制权交回这些结构后面的语句。

-   当你使用带 label 的 break 时，它会终止指定的带标记（label）的语句。

break 语句的语法看起来像这样：

`break [label];`

在语法中，被 \[\] 包裹的内容是可省略的，也就是 label
可以省略。若省略，则终止当前所在的循环或 switch；若不省略，则终止指定的
label 语句。

### Continue语句

continue 语句可以用来继续执行（跳过代码块的剩余部分并进入下一循环）一个
while、do-while、for，或者 label 语句。

-   当你使用不带 label 的 continue 时， 它终止当前 while，do-while，或者
    for 语句到结尾的这次的循环并且继续执行下一次循环。

-   当你使用带 label 的 continue 时， 它会应用被 label 标识的循环语句。

continue 语句的语法看起来像这样：

`continue [label];`

### label语句

一个 label 提供了一个让你在程序中其他位置引用它的标识符。例如，你可以用
label 标识一个循环， 然后使用 break 或者 continue
来指出程序是否该停止循环还是继续循环。

label 语句的语法看起来像这样：

```javascript
label :

    statement
```

label 的值可以是任何的非保留字的 JavaScript 标识符， statement
可以是任意你想要标识的语句（块）。
