## 问答

---
### 1. 在什么场景下会出现外边距合并？如何合并？如何不让相邻元素外边距合并？给个父子外边距合并的范例
* 外边距合并指的是垂直方向上的外边距合并，产生的条件如下：
    * 必须是处于文档流中的块级盒子并处于同一个BFC中。
    * 外边距必须是紧邻着的，即两个外边距之间不能有如Line box、clearance、padding、border等存在。
* 如何合并
合并的效果就两个margin合并为是只存在一个margin，取margin值更大者。
* 如何不让相邻外边距合并
只要破坏外边距合并产生的条件即可。常用的有：
    * overflow设置成非visiable生成BFC，并且让两个元素处于不同的BFC中。
    * 根据需要设置定位或者浮动使其中之一脱离文档流。
    * 设置border使外边距不紧邻。

### 2. 去除inline-block内缝隙有哪几种常见方法?
去除inline-block内缝隙的常见方法：
  * 让行内块元素的标签紧挨着，中间不要有空格、换行。
  * 使用浮动。
  * 使用负边距。


### 3. 父容器使用overflow: auto| hidden撑开高度的原理是什么？
原理是父容器触发了BFC，在其内开辟了一个独立空间，不再受子元素的浮动影响，自然有高度了。

### 4. BFC是什么？如何形成BFC，有什么作用?
* BFC(Block Formatting Context)——块级格式化上下文，指的是在其内开辟了一个独立空间，使内部的元素不受外部影响。
* 触发形成BFC的方法如下：
  * 浮动或者绝对、固定定位触发BFC。
  * overflow属性值非visiable。
  * display成非块级盒子。
* 作用
  * 清除浮动
  * 消除外边距合并

### 5. 浮动导致的父容器高度塌陷指什么？为什么会产生？有几种解决方法
* 浮动导致的父容器高度塌陷指浮动元素脱离文档流，自然没有了高度。
* 解决方法有两种：
    * 用clear:both(left或right)清除浮动造成的影响（使用调用一个伪元素的方法最佳），涉及的方法有task10中有提到，这里不做赘述。
    * 通过触发BFC来消除浮动带来的影响。父容器使用overflow:hidden最佳，其它方法请看task10。
### 6. 以下代码每一行的作用是什么？ 为什么会产生作用？ 和BFC撑开空间有什么区别？
```
.clearfix:after{
    content: '';
    display: block;
    clear: both;
}
.clearfix{
    *zoom: 1;
}
```
* 作用
用于清除浮动元素对父元素的影响。
* 原理
.clearfix:after声明在父元素内最后面创建一个子元素的伪元素，内容为空、块级元素、清除所有子元素的浮动；
.clearfix声明兼容IE6。
* 与BFC区别
之前已经多次提及清除浮动的方法主要有两种性质:一种是用clear清除浮动，一种是触发BFC清除浮动。本题代码为前者，BFC撑开空间为后者。

## 代码

---
[task11-1](https://github.com/jirengu-inc/jrg-renwu7/blob/master/members/%E8%B5%96%E9%9C%84/task-11/task11-1.html)
[task11-1 preview](http://book.jirengu.com/jirengu-inc/jrg-renwu7/members/%E8%B5%96%E9%9C%84/task-11/task11-1.html)

[task11-2](https://github.com/jirengu-inc/jrg-renwu7/blob/master/members/%E8%B5%96%E9%9C%84/task-11/task11-2.html)
[task11-2 preview](http://book.jirengu.com/jirengu-inc/jrg-renwu7/members/%E8%B5%96%E9%9C%84/task-11/task11-2.html)

## 参考

---
[理解 bfc 和边距合并](http://www.w3cplus.com/css/understanding-bfc-and-margin-collapse.html)


---
**本文章著作权归九霄所有，转载须说明来源**
