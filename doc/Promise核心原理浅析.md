# Promise核心原理浅析

- 核心原理是通过then方法传入回调，内部创建回调队列，在resolve/reject的时候调用队列里的回调(重点：执行队列里的回调必须是异步的，只要如此才能获取注册的回调)，刚好把获取的数据传入。

- 链式调用待完善。

- 解开了一个疑惑：event loop里Promise属于microtask，`new Promise(fn).then(resolve)`里Promise的回调是同步的，then的回调是异步，under the hood终于看清了。（注：由于Promise属于microtask，而setTimeout属于marcotask，应该不是用setTimeout实现异步，这里仅作模拟）

- 核心代码简单实现

```js
function fakePromise(fn){
    let status = 'pending'
    let successArray = []
    let failArray = []
    function resolve(){
        status = 'resolved'
        todoThen.apply(undefined, arguments)
    }
    function reject(){
        status = 'rejected'
        todoThen.apply(undefined, arguments)
    }
    function todoThen(){
        setTimeout(() => { //异步保证获取注册回调
          if(status == 'resolved'){
              successArray.forEach(callback => {
                  callback.apply(undefined, arguments)
              })
          }else if(status == 'rejected'){
              failArray.forEach(callback => {
                  callback.apply(undefined, arguments)
              })
          }
        })
    }
    fn.call(undefined, resolve, reject)
    return {
        then(resolved, rejected){
            successArray.push(resolved)
            failArray.push(rejected)
            return undefined // 待实现链式调用
        }
    }
}
```

