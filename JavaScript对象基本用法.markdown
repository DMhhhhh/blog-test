# JavaScript对象基本用法

## 声明对象的两种语法

Object 是 JavaScript 的一种 数据类型
。它用于存储各种键值集合和更复杂的实体。

The Object class represents one of JavaScript\'s data types. It is used
to store various keyed collections and more complex entities.

### 写法

```javascript
let obj = { \'name\': \'frank\', \'age\': 18 }

let obj = new Object({\'name\': \'frank\'})
```

键名是字符串，不是标识符，可以包含任意字符

引号可省略，省略之后就只能写标识符

就算引号省略了，键名也还是字符串（重要）

**每个 key 都是对象的属性名（property）**

**每个 value 都是对象的属性值**

### 奇怪的属性名

#### 所有属性名会自动变成字符串

```javascript
let obj = {

1: \'a\',

3.2: \'b\',

1e2: true,

1e-2: true,

.234: true,

0xFF: true

};

Object.keys(obj)

=\> \[\"1\", \"100\", \"255\", \"3.2\", \"0.01\", \"0.234\"\]
```
#### 细节

Object.keys(obj) 可以得到 obj 的所有 key

### 变量作属性名

#### 如何用变量做属性名

之前都是用常量做属性名

```javascript
let p1 = \'name\'

let obj = { p1 : \'frank\'} 这样写，属性名为 \'p1\'

let obj = { \[p1\] : \'frank\' } 这样写，属性名为 \'name\'
```
#### 对比

不加 \[ \] 的属性名会自动变成字符串

加了 \[ \] 则会当做变量求值

值如果不是字符串，则会自动变成字符串

## 如何删除对象的属性

#### delete obj.xxx 或 delete obj\[\'xxx\'\]

即可删除 obj 的 xxx 属性

请区分「属性值为 undefined」和「不含属性名」

#### 不含属性名

```javascript
\'xxx\' in obj === false
```

#### 含有属性名，但是值为 undefined

```javascript
\'xxx\' in obj && obj.xxx === undefined
```

#### 注意 obj.xxx === undefined

不能断定 \'xxx\' 是否为 obj 的属性

#### 类比

你有没有卫生纸？

A: 没有 // 不含属性名

B: 有，但是没带 // 含有属性名，但是值为 undefined

## 如何查看对象的属性

### 查看所有属性（读属性）

#### 查看自身所有属性

```
Object.keys(obj)
```

#### 查看自身+共有属性

```
console.dir(obj)
```

或者自己依次用 Object.keys 打印出 obj.\_\_proto\_\_

#### 判断一个属性是自身的还是共有的

```javascript
obj.hasOwnProperty(\'toString\')
```

### 查看属性

#### 两种方法查看属性

中括号语法：
```javascript
obj['key']
```

点语法：
```javascript
obj.key
```

坑新人语法：
```javascript
obj[key] // 变量 key 值一般不为 \'key\'
```

#### 请优先使用中括号语法

点语法会误导你，让你以为 key 不是字符串

等你确定不会弄混两种语法，再改用点语法

## 如何修改或增加对象的属性

### 修改或增加属性（写属性）

#### 直接赋值

```javascript
let obj = {name: \'frank\'} // name 是字符串

obj.name = \'frank\' // name 是字符串

obj\[\'name\'\] = \'frank\'

obj\[name\] = \'frank\' // 错，因 name 值不确定

obj\[\'na\'+\'me\'\] = \'frank\'

let key = \'name\'; obj\[key\] = \'frank\'

let key = \'name\'; obj.key = \'frank\' // 错，因为 obj.key 等价于
obj\[\'key\'\]
```

#### 批量赋值

```javascript
Object.assign(obj, {age: 18, gender: \'man\'})
```

### 修改或增加共有属性

#### 无法通过自身修改或增加共有属性

```javascript
let obj = {}, obj2 = {} // 共有 toString

obj.toString = \'xxx\' 只会在改 obj 自身属性

obj2.toString 还是在原型上
```

#### 我偏要修改或增加原型上的属性

```javascript
obj.\_\_proto\_\_.toString = \'xxx\' // 不推荐用 \_\_proto\_\_

Object.prototype.toString = \'xxx\'
```

一般来说，不要修改原型，会引起很多问题

### 修改隐藏属性

#### 不推荐使用 \_\_proto\_\_

```javascript
let obj = {name:\'frank\'}

let obj2 = {name: \'jack\'}

let common = {kind: \'human\'}

obj.\_\_proto\_\_ = common

obj2.\_\_proto\_\_ = common
```

#### 推荐使用 Object.create

```javascript
let obj = Object.create(common)

obj.name = \'frank\'

let obj2 = Object.create(common)

obj2.name = \'jack\'
```

规范大概的意思是，要改就一开始就改，别后来再改

## \'name\' in obj和obj.hasOwnProperty(\'name\') 的区别

'name' in
obj判断对象obj是否存在'name'属性；obj.hasOwnProperty(\'name\')判断属性'name'是obj自身属性还是共有属性
