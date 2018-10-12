## XSS小结

- Cross Site Scripting —— 跨站点脚本攻击
- 分类
    - 反射型
        - 攻击脚本代码写在query中随请求发送到服务器，服务器解析query中的攻击代码放入模板再响应请求，浏览器执行攻击脚本
        - 举例

            ```js
            // 隐藏元素自动执行
            xxxx.com/?xss=<img src=null onerror=alert(0)>

            // 引诱用户点击执行
            xxx.com/?xss=<p onclick=alert(1)>

            // 嵌入iframe以植入广告
            xxxx.com/?xss=<iframe src='//xxxad.com'></iframe>
            ```

    - 存储型
        - 攻击脚本是注入到页面任何可以用户输入的区域，然后随请求发动到服务端并存储在服务端；服务端解析脚本，脚本非法操作数据库。与反射型的差别是脚本的位置不同，脚本只要一次成功存储在服务端即可自动完成攻击
- 防御
    - 编码
        - 对用户输入内容进行HTML Entity（即字符转义）
    - 过滤
        - 反转义
            - 使用encode.js对HTML Entity反转义
        - 校正
            - 使用domParse.js
            - 代码示例

                ```js
                // 由于用户输入是不可测的，解析过程容易出错，所以下面的函数要放到try...catch中
                HTMLParse(decodeStr,{
                    start: function(tag, attrs, unary){}，//把开标签解析为tag为标签字符串， attrs为属性数组， unary布尔值true为单标签。在回调里处理过滤逻辑
                    end: function(tag){}, // 闭标签
                    chars: function(text){}, // innerText
                    comment: function(text){} // 标签内部注释
                })
                ```

        - 过滤掉危险标签与DOM属性，处理过程上面校正有提到
            - tag

             > style script img link iframe frame ...

            - attribute

             > onclick onerror ...



- [参考](https://www.imooc.com/learn/812)