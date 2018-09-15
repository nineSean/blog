### 关键词

---
标签属性 `<a>`标签 `<p>`标签 列表标签 `<table>`标签

### 知识点

---
#### 1. Doctype
文档类型，定义不同的文档类型，浏览器提供不同的支持。
#### 2. 规范的HTML文件
```
    <!Doctype html>
    <html>
      <head></head>
      <body></body>
    </html>
```
规范的HTML文件必须包括这四个标签。
#### 3. 标签分类
* 双标签
双标签包括开始标签和结束标签。如下
```
      <div></div>
      <ul></ul>
```
* 单表签
```
      <img src="" alt="">
      <img src="" alt=""/>
```
上面的写法是规范写法，在html5中兼容下面写法为上面的写法。

#### 4. 标签属性
* 公有属性
所有标签都有的属性，如id、class、style等。
* 建议属性值都用引号包着。
* 结束标签`<`与`/`之间不能有空格。
* 大小写敏感
  * 不敏感：标签名、属性名。
  * 敏感：属性值。

#### 5. `<a>`标签
* 写法
```
      <a href="xxxxx">...</a>
```
* 特有属性
href
  * 绝对路径
Linux：以`/`开头
window：以盘符如` C:\ `开头
href=/absolute/path.html
  * 相对路径
只要以目录名开始的就是相对路径
href=relative/path.html
  * 网址
以`//`或者`http`开头
href=//[www.baidu.com](http://www.baidu.com/)
href=[http://www.baidu.com](http://www.baidu.com/)
  * 伪协议
`javascript:JS代码`
href=javascript:alert(1)
  * `#`id
* 默认样式
`: link`
`: hover`
`: visited`
`: active`
* 默认动作
跳转页面
* target属性
属性值有以下几种
  * _blank
  * _parent
  * _top
  * _self

#### 6. `<h1>`到`<h6>`标签
* 表达页面、文章的逻辑层次
* 默认样式
加粗、大小、line-height

#### 7. `<strong>`标签
* 表示逻辑上着重、强调
* 默认样式
加粗
* `<b>`标签效果一样，但无语义，不推荐使用  

#### 8. `<em>`标签
* 表示语气上的强调
* 默认样式
斜体
* `<i>`标签效果一样，但无语义，不推荐使用

#### 9. `<p>`标签
* 表示一个段落
* 默认样式
段落间距
* **可以不闭合**
`<p>`元素紧跟着 address, article, aside, blockquote, div, dl, fieldset, footer, form, h1, h2, h3, h4, h5, h6, header, hgroup, hr, main, nav, ol, p, pre, section, table, ul元素时结束标签可以省略。

#### 10. 列表标签
* 有序列表
表示有顺序的列表
```
        <ol>
          <li></li>
          <li></li>
        </ol>
```
默认样式
按照阿拉伯数字1、2、3顺序排序

* 无序列表
表示无顺序的列表
```
          <ul>
          <li></li>
          <li></li>
        </ul>
```
默认样式
`<li>`里内容的前面加个小圆点

* `<dl>`列表
```
      <dl>
        <dt></dt>
        <dd></dd>

        <dt></dt>
        <dd></dd>
      </dl>
```
dd标签的内容对dt标签里的术语进行定义、描述

#### 11. `<table>`标签
* 写法
```
	  <table>
        <colgroup>
                <col width=100>
                <col width=200>
                <col>
        </colgroup>
		<thead>
			<tr>
				<td>表头1</td>
				<td>表头2</td>
				<td>表头3</td>
			</tr>
		</thead>
		<tbody>
			<tr>
				<td>数据1</td>
				<td>数据2</td>
				<td>数据3</td>
			</tr>
			<tr>
				<td>数据1</td>
				<td>数据2</td>
				<td>数据3</td>
			</tr>
		</tbody>
		<tfoot>
			<tr>
				<td>汇总</td>
				<td>总数</td>
			</tr>
		</tfoot>
	  </table>
```
`<table>`标签包括表头`<thead>`、主体`<tbody>`、尾部`<tfoot>`三部分，如果没写默认都属于主体。
`<td>`表示表格数据，如果不是表示数据可用`<th>`代替。   
`<colgroup>` 标签用于定义列宽，但有违结构、样式分离的原则。

#### 12. 浏览器如何识别HTML
* file协议
该协议下浏览器通过文件后缀来识别。
* http协议
该协议下浏览器根据MIME类型识别。
* 浏览器如何识别HTML类型
文档类型`<!doctype>`标签声明，若未声明浏览器靠猜。    
    

### 拓展知识

---
1. [JS伪协议](http://www.cnblogs.com/song-song/p/5277838.html)
2. [MIME类型](http://www.cnblogs.com/jsean/articles/1610265.html)

### 参考

---
[W3C Recommendation](https://www.w3.org/TR/html5/grouping-content.html#the-p-element)


---
**本文章著作权归九霄所有，转载须说明来源**
