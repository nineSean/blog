## Cookie

### 是什么
- 1994年网景公司的Lou Montulli发明。属于HTTP协议层面上的技术

- 后端
    - 通过给响应头设置`Set-Cookie`字段设置cookie响应给前端，代码示例如下

        ```js
        response.setHeader('Set-Cookie', `username=${data.name}`)
        
        // setHeader通过key/value的形式设置cookie
        // 而value后面可以添加指令来对cookie值进行限制
        // 指令包括Expires Max-Age HttpOnly Secure Path等
        // 值与指令，指令与指令之间通过分号隔开
        ```
    
- 前端
    - 获取
        - 浏览器通过响应头中的`Set-Cookie`字段获取cookie保存
        - JS通过`document.cookie`可以获取cookie
    - 设置
        - JS通过`document.cookie`亦可设置cookie，代码示例如下

          ```js
          document.cookie = `tag=xxxx`
          
          // 设置多个值时，只有最前面的生效
          // 相较于设置，称追加更合适，因为设置相同名称的值只会添加而不会替换
          ```
          
    - 删除
        - 通过控制台的Application -> Storage -> Cookies删除
        - JS通过设置过期时间删除，代码示例如下

            ```js
            document.cookie = `data=xxx; expires=${new Date(1).toGMTString()}`
            ```

### 为什么
- HTTP是无状态的协议，cookie发明的目的就是维护用户状态。在后端给前端种好cookie，前端每次请求都会带上cookie，而后端凭此识别用户身份
- 能够客户端存储数据，但是不是主要用途，该功能被localStorage替代

### 特性
- 域名
    - 遵守同源策略
- 有效期
    - `Expires`
      
      ```js
      // 后端
      response.setHeader('Set-Cookie', `username=xxx; expires=${new Date(12312312323123123123).toGMTString()}`)
      
      // 前端前文有提
      ```
       
    - `Max-Age`

     ```js
     response.setHeader('Set-Cookie', 'username=xx; Max-Age=5') //Max-Age单位为秒
     
     // 注意当Expires与Max-Age共存时，后者权重大
     ```
     
     - none
         - 当不设置有效期时，在关闭浏览器后失效
    
- 路径
    - 用于限制同域名下cookie在哪个目录生效 
- HttpOnly
    - 目的是为了防止前端JS修改cookie，可以有效防御XSS
- Secure
    - 在HTTPS或者SSL协议下才传递cookie，HTTP协议不会传递cookie，如此确保了在通讯过程中cookie的安全
- 上限4KB

### 性能优化
- cookie在相关域名下面 — cdn流量损耗
    - 描述：只要在一个域名下的请求都会带上cookie，对于请求静态文件cookie是无用的（因为cookie的目的前文有提是维护用户状态，静态文件请求不涉及服务端逻辑）；cookie上限为4kb，大量的静态文件请求将会损耗非常庞大的流量
    - 解决方案：把静态资源放在cdn上，而cdn域名与主域名区分开

### 更多待深入

- 登录用户的凭证设置
    - 用户ID
    - 用户ID + 签名
    - SessionId

