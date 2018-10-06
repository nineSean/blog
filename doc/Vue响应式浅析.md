# Vue响应式

- 通过`Object.defineProperty`实现get与set监听

- 同样实现了把data对象属性代理到Vue实例对象上

- [代码演示](https://jsbin.com/guxesof/edit?html,js,output)

```js
let vm = {
  data: {
    name: 'sean',
    age: 29
  }
}

for (let prop in vm.data) {
  Object.defineProperty(vm, prop, {
      get() {
        console.log('get')
        return this.data[prop]
      },
      set(newVal) {
        console.log('set')
        this.data[prop] = newVal
      }
  })
}

console.log(vm.name)
console.log(vm.age = 10)
```

