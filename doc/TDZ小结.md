### TDZ小结

---

- TDZ是什么
  - temporal dead zone - 暂存性死区
  - let与const才具有，而var不具有
  - 存在于**进入作用域与变量声明之间**，在此期间访问该变量会抛错
  - 仍然存在**变量提升**

- TDZ意义

  - 在声明前使用变量一般都是意外，所以抛错是一种提醒、警告
  - 建立一种机制，在运行时让每个变量都有正确的值（如运行时的类型检查）

- TDZ下typeof抛错

  - 也是一种提醒
  - 不用typeof检查变量的存在，如下：

  ```javascript
  //用typeof
  if(typeof globalVariable === 'undefined'){
      var globalVariable = {...}
  }

  //不用typeof
  if(!(globalVariable in window)){
      window.globalVariable = {...}
  }
  //创建全局变量，慎用
  ```






#### 参考

---

- https://stackoverflow.com/questions/33198849/what-is-the-temporal-dead-zone
- [http://2ality.com/2015/10/why-tdz.html](http://2ality.com/2015/10/why-tdz.html)