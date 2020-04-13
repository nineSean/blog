# Node端与Web端带/不带var赋值的差异

## 测试环境
- chrome version 80.0.3987.163
- node v13.7.0

## 由一道面试引发的糗事

今天看到一道面试题是这样的：

```js
function a(){
    console.log(this.name)
}
name = 'hello'
a.call()
```

群友直接抛出为什么结果是`undefined`，不及细想，直接回到如下：

> call第一参数不传就是undefined，执行a.call() => 进入函数体 => this为undefined浏览器环境帮你换成window => 找window.name，a声明时的上下文中window.name为undefined（词法作用域）

这人丢大发了，因为群友接着又问了这题的变种：

```js
function a(){
    console.log(this.name)
}
var name = 'hello'
a.call()
```

为啥还是`undefined`？

这下引起重视，赶紧现在chrome上打印下看看，不论上下两种情况，都是打印`hello`啊，这不是把2个人的脸都打肿了么？

## 思考

- Web端打印还是符合预期的，那群友的问题肯定是出在Node端，赶紧Node端打印一波；
- 不带`var`的打印'hello'；
- 带`var`的打印undefined；
- 第二种情况有点百思不得其解，得好好分析下。

## Web端分析

### 不带`var`

```js
function a(){
    console.log(this.name)
}
name = 'hello'
a.call()

// hello
```

1. 未声明变量直接赋值`name = 'hello'`，整个语句提升到顶部，`name`为全局变量；
2. `a.call()`执行，进入函数体，绑定函数体内的`this`为`undefined`，直接`script`标签引入的情况下，浏览器转换`this`为`window`（注意：script标签添加了`type=module`属性后，浏览器不会转换`undefined`为`window`）；
3. 打印`window.name`，即为`hello`。

### 带`var`

```js
function a(){
    console.log(this.name)
}
var name = 'hello'
a.call()

// hello
```

1. `var`变量声明提升；
2. 函数声明`a`；
3. `name = 'hello'`；
4. `a.call()`执行，进入函数体，绑定函数体内的`this`为`undefined`，直接`script`标签引入的情况下，浏览器转换`this`为`window`；（注意：script标签添加了`type=module`属性后，浏览器不会转换`undefined`为`window`）
5. `var`声明的变量，浏览器挂在到了window上，`window.name`指向`var`声明的`name`，即为`hello`。

## Node端分析

### Node中的全局变量

global 最根本的作用是作为全局变量的宿主；按照 ECMAScript 的定义，满足以下条件的变量是全局变量：

- 在最外层定义的变量；
- 全局对象的属性；
- 未声明直接赋值的变量。

当你定义一个全局变量时，这个变量同时也会成为全局对象的属性，反之亦然。

需要注意的是，在Node.js中你不可能在最外层定义变量，因为所有用户代码都是属于当前模块的，而模块本身不是最外层上下文。

由于未声明直接赋值的变量会造成全局变量，请使用`const`与`let`声明变量。

### 不带`var`

```js
function a(){
    console.log(this.name)
}
name = 'hello'
a.call()

// hello
```

1. `name = 'hello'`不会提升，但是执行到这一句的时候name会挂在到global对象上；
2. `a.call()`执行，进入函数体，绑定函数体内的`this`为`undefined`，JS引擎转换`this`为`global`；
3. 打印`global.name`，即为`hello`。

### 带`var`

```js
function a(){
    console.log(this.name)
}
var name = 'hello'
a.call()

// undefined
```

1. `var`变量声明提升；
2. 函数声明`a`；
3. `name = 'hello'`；
4. `a.call()`执行，进入函数体，绑定函数体内的`this`为`undefined`，JS引擎转换`this`为`global`；
5. 由于模块内的局部变量`name`不等于全局`global.name`，而`global.name`又未赋值，所以`global.name`为undefined。


## 有不正之处，请斧正


