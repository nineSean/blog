## RegExp

---
* 概念
正则表达式(Regular Expression)是计算机科学的一个概念。正则表达式使用单个字符串来描述、匹配一系列符合某个句法规则的字符串。在很多文本编辑器里，正则表达式通常被用来检索、替换那些符合某个模式的文本。

## 问答

---
### 1. `\d，\w,\s,[a-zA-Z0-9],\b,.,*,+,?,x{3},^$`分别是什么?

字符|含义
:-:|:-:
\d|匹配任意数字
\w|匹配任意数字、字母、下划线和汉字
\s|匹配任意空白符，包括空格、tab、换行、回车
[a-zA-Z0-9]|匹配字母和数字
\b|匹配单词的边界（开始或者结束）
.|匹配任意非空白字符
*|匹配1次或者多次
+|匹配0次或者多次
?|匹配0次或者1次
x{3}|匹配3个x
^|匹配字符串的开始边界
$|匹配字符串的结束边界


### 2. 贪婪模式和非贪婪模式指什么?
 * 贪婪模式
 匹配量词、边界等会默认尽可能多、尽可能长的匹配。
 * 非贪婪模式
 匹配量词、边界等会尽可能少、尽可能短的匹配。

## 代码

---
### 1. 写一个函数`trim(str)`，去除字符串两边的空白字符

```javascript
    function trim(str){
        var strArr = str.split(/^\s+/g)
        var toStr = strArr.join('')
        strArr = toStr.split(/\s+$/g)
        return strArr.join('')
    }
    trim('   1 2   3    ')
```

```javascript
    function trim(str){
        var fixStr = str.replace(/^\s+|\s+$/g,'')
        return fixStr
    }
    trim(' asdf df    df 1   ')
```

### 2. 使用实现`addClass(el, cls)、hasClass(el, cls)、removeClass(el,cls)`，使用正则

```javascript
    function hasClass(el,cls){
        var reg = new RegExp('(\\s|^)' + cls + '(\\b|$)', 'g')
        return reg.test(el.className)
    }

    function addClass(el,cls){
        if(!hasClass(el,cls)){
            return el.className += ' ' + cls
        }
        console.log('已有该类名')
    }

    function removeClass(el,cls){
        if(!!hasClass(el,cls)){
            return el.className.replace(cls,'')
        }
        console.log('没有该类名')
    }
```

由于该题需要获取DOM，代码如下：
[preview](http://js.jirengu.com/qakeregoni/4/edit)

### 3. 写一个函数`isEmail(str)`，判断用户输入的是不是邮箱

```javascript
    function isEmail(str){
        var reg = new RegExp('\\w+@\\w+\\.(com)$','g')
        if(reg.test(str)){
            return console.log('邮箱格式正确')
        }
        return console.log('邮箱格式有误')
    }
    isEmail('vipatlx@qq.com')
    isEmail('vipatlx@qq .com') 
    isEmail('vipatlx@.com')   
```

### 4. 写一个函数`isPhoneNum(str)`，判断用户输入的是不是手机号

```javascript
    function isPhoneNum(str){
        var reg = /^(86)?1[34578]\d{9}$/g 
        if(reg.test(str)){
            return console.log('手机号码格式正确')
        }
        return console.log('手机号码格式有误')
    }
    isPhoneNum('12334562452')
    isPhoneNum('123345f2452')
    isPhoneNum('123342452')
    isPhoneNum('18779778355')

```

### 5. 写一个函数`isValidUsername(str)`，判断用户输入的是不是合法的用户名（长度6-20个字符，只能包括字母、数字、下划线）

```javascript
    function isValidUsername(str){
        // var reg = /^[\d_a-zA-Z]{6,20}$/g
        var reg = /^\w{6,20}$/g//\w不匹配汉字，《正则表达式30分钟入门教程》有误
        if(reg.test(str)){
            return console.log('用户名格式正确')
        }
        return console.log('用户名格式有误') 
    }
    isValidUsername('a123456789')   
    isValidUsername('a12345678 9')   
    isValidUsername('a12345678我9')   
    isValidUsername('a12345678932423423423dsdfsdf') 
```

### 6. 写一个函数`isValidPassword(str)`, 判断用户输入的是不是合法密码（长度6-20个字符，包括大写字母、小写字母、数字、下划线至少两种）

```javascript
    function isValidPassword(str){
        var basicStr = /^\w{6,20}$/g,
            W = /^[A-Z]{6,20}$/g
            w = /^[a-z]{6,20}$/g
            d = /^\d{6,20}$/g
            line = /^_{6,20}$/g
        if(basicStr.test(str)){
            if(W.test(str)|w.test(str)|d.test(str)|line.test(str)){
                return console.log('用户名格式有误') 
            }
            return console.log('用户名格式正确')
        }
        return console.log('用户名格式有误') 
    }
    isValidPassword('sdfsdfe')
    isValidPassword('aaaaaa')
    isValidPassword('dsfsd')
    isValidPassword('_dsfsd')
```

### 7. 写一个正则表达式，得到如下字符串里所有的颜色（#121212）

```javascript
var re = /*正则...*/

var subj = "color: #121212; background-color: #AA00ef; width: 12px; bad-colors: f#fddee #fd2 "

alert( subj.match(re) )  // #121212,#AA00ef
```

### 8. 下面代码输出什么? 为什么? 改写代码，让其输出`hunger, world`.

```javascript
    var str = 'hello  "hunger" , hello "world"';
    var pat =  /".*"/g;
    str.match(pat);  //[""hunger" , hello "world""],默认为贪婪匹配，尽可能的长的匹配字符
```

```javascript
    var str = 'hello  "hunger" , hello "world"';
    var pat =  /".*?"/g;//?激活懒惰匹配，尽可能短的匹配
    str.match(pat);
```

### 9. 补全如下正则表达式，输出字符串中的注释内容. (可尝试使用贪婪模式和非贪婪模式两种方法)

```javascript
str = '.. <!-- My -- comment \n test --> ..  <!----> .. '
re = /.. your regexp ../

str.match(re) // '<!-- My -- comment \n test -->', '<!---->'
```
非贪婪模式

```javascript
    str = '.. <!-- My -- comment \n test --> ..  <!----> .. '
    re = /<!--[.|\n]*?-->/mg

    console.log(str.match(re))   // '<!-- My -- comment \n test -->', '<!---->'
```



### 10. 补全如下正则表达式

```javascript
    var re = /<\w+.*?>/g

    var str = '<> <a href="/"> <input type="radio" checked> <b>'
    str.match(re) // '<a href="/">', '<input type="radio" checked>', '<b>'    
```



## 参考

---
[正则表达式30分钟入门教程](http://deerchao.net/tutorials/regex/regex.htm#mission)

[正则表达式](http://book.jirengu.com/fe/%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/Javascript/%E6%AD%A3%E5%88%99%E5%9F%BA%E6%9C%AC%E8%AF%AD%E6%B3%95.html)
[]()

[]()
[]()

[]()
[]()

[]()
[]()

[]()
[]()


---
**本文章著作权归九霄所有，转载须说明来源**
