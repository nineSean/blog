

## 问答

---
### 1. 说说库和框架的区别？
* 库（library）
基础功能的代码集合而成，供程序员调用的方法集。比较灵活，但是没有框架方便。
* 框架（framework）
规范开发者按照框架设计的解决方案写代码，不是简单的工具集。比库更庞大、规范。

* 两者区别在于库是工具集合，它是框架的子集；而框架是一套规范性的解决方案，它是库的超集。

### 2. jquery 能做什么？
jQuery提供了易于使用且兼容众多浏览器的API，使诸如 HTML 文档遍历和操作、CSS操作、事件处理、动画和 Ajax操作更加简单。

### 3. jquery 对象和 DOM 原生对象有什么区别？如何转化？
区别在于继承的属性与方法不一样
* jQuery对象———>DOM原生对象
jQuery对象[0]即可，举例如下：

```javascript
var $head = $('#head');//获取节点生成jQuery对象
var head = $head[0];//转换
```

* DOM原生对象———>jQuery对象
$(DOM原生对象)即可，举例如下：

```javascript
var head = document.getElementById('#head');//获取节点生成DOM对象
var $head = $(head);//转换
```

### 4. jquery中如何绑定事件？bind、unbind、delegate、live、on、off都有什么作用？推荐使用哪种？使用on绑定事件使用事件代理的写法？
* jQuery绑定/解绑事件的方法有：.bind()/.unbind()、.delegate()/.undelegate()、.live()/.die()、.on()/.off()。
* bind、unbind、delegate、live区别与推荐事件绑定的方法
    * .bind()
先查找到所有相关元素，然后把函数绑定到每个元素指定事件上。(unbind解绑同理)
    * .delegate()
先查找到所有相关元素，把事件、.delegate()中的选择器这两个参数与函数绑定在之前查找到的元素上，当事件冒泡到此元素上时与绑定的参数匹配后是否一致再执行函数。
    * .live()
先查找到所有相关元素，然后把这些元素、事件这两个参数绑定在根元素document上，当事件冒泡到根元素上时与绑定的参数匹配后是否一致再执行函数。
（注：也可以通过设置参数绑定至其它节点，[点击查看](http://js.jirengu.com/tuduxicoru/2/edit?html,js,console,output)）
    * .on()
以上几种绑定事件的方法都有其局限性或者被弃用，.on()把上面三种方法统一了，用起来更方便，故而推荐此法。
(相对应的解绑方法为.off())
* .on() 绑定事件的写法

```javascript
$('ul').on('click','li',function(){//中间的选择器参数可选，省略则ul都能触发事件。
//to do
});
```

### 5. jquery 如何展示/隐藏元素？
.hide()/.show()方法隐藏/展示元素，而.toggle()则在两种状态互相切换如下：

```javascript
//展示
$('.sidebar').show()
//隐藏
$('#footer').hide()
//切换
$('.sidebar').toggle()
```

### 6. jquery 动画如何使用？
动画方法：

```javascript
$(selector).animate({params},speed,callback);
//必需项：params，此参数设置最终动画的CSS属性。
//可选项：speed，设置动画效果 时长，取值为“fast”、“slow”或者毫秒数。
//可选项：callback，设置动画完成后执行的函数。
```

* [查看demo](http://js.jirengu.com/bikuwijaqa/1/edit)

### 7. 如何设置和获取元素内部 HTML 内容？如何设置和获取元素内部文本？
* .html()
获取元素内部HTML内容,如果括号内有参数则设置HTML内容。
* .text()
获取元素内部文本，如果括号内有参数则设置文本。

* [查看demo](http://js.jirengu.com/pusufiraqo/2/edit)

### 8. 如何设置和获取表单用户输入或者选择的内容？如何设置和获取元素属性？
* .val()
获取表单用户输入或选择内容，如果括号内有参数则设置内容。
* .attr('attribute'[,'value'])
无中括号的参数则获取元素制定属性，若有中括号内的参数则设置属性为此属性值。
* [查看demo](http://js.jirengu.com/qujununiso/1/edit)

## 代码

---
### 1. [点击查看导航demo](http://book.jirengu.com/jirengu-inc/jrg-fe7/%E4%BD%9C%E4%B8%9A%E5%AE%89%E6%8E%92/jscode/JS8-jqery%E8%AF%AD%E6%B3%95/8-1.html)
[task25-1 code](https://github.com/jirengu-inc/jrg-renwu7/blob/master/members/%E8%B5%96%E9%9C%84/task-25/task25-1.html)
[task25-1 preview](http://book.jirengu.com/jirengu-inc/jrg-renwu7/members/%E8%B5%96%E9%9C%84/task-25/task25-1.html)
### 2. [点击查看tab切换demo](http://book.jirengu.com/jirengu-inc/jrg-fe7/%E4%BD%9C%E4%B8%9A%E5%AE%89%E6%8E%92/jscode/JS8-jqery%E8%AF%AD%E6%B3%95/8-2.html)
[task25-2 code](https://github.com/jirengu-inc/jrg-renwu7/blob/master/members/%E8%B5%96%E9%9C%84/task-25/task25-2.html)
[task25-2 preview](http://book.jirengu.com/jirengu-inc/jrg-renwu7/members/%E8%B5%96%E9%9C%84/task-25/task25-2.html)
#### Q:点奢侈品2的时候页面跳到了顶部，可能是什么原因？如何解决
* 由于点击li非a的区域不会跳到顶部，所以可能是a标签的属性href='#',在此情况点击a标签默认锚点为#top——会跳到页面顶部。可以把a标签设置成死链接：href='javascript:void(0)'或者取消默认事件:event.preventDefault()。
### 3. [点击查看代理demo](http://book.jirengu.com/jirengu-inc/jrg-fe7/%E4%BD%9C%E4%B8%9A%E5%AE%89%E6%8E%92/jscode/JS8-jqery%E8%AF%AD%E6%B3%95/8-3.html)
[task25-3 code](https://github.com/jirengu-inc/jrg-renwu7/blob/master/members/%E8%B5%96%E9%9C%84/task-25/task25-3.html)
[task25-3 preview](http://book.jirengu.com/jirengu-inc/jrg-renwu7/members/%E8%B5%96%E9%9C%84/task-25/task25-3.html)


## 参考

---
[框架与库有什么关系和区别](https://segmentfault.com/q/1010000000752015)
[库与框架的区别](http://www.cnblogs.com/xuld/archive/2011/02/20/1958933.html)

[jQuery的.bind()、.live()和.delegate()之间的区别](http://article.yeeyan.org/view/213582/179910)
[]()

[]()
[]()

[]()
[]()

---
**本文章著作权归九霄所有，转载须说明来源**

---

