# promise  深度理解
# 1.初步了解
promise 有3个状态 分别是等待中 解决 报错  resolve 对应的是结局 reject 对应是报错
promise 实例向构造函数传递一个回调函数 有resolve 和reject 2个函数可以调用 resolve 改变状态 为解决 reject 改变状态为报错 promise 原型上有一个方法叫做then
实例方法调用.then（）传递2 个函数 第一个函数对应接收成功的参数 ，第二个函数接收错误的信息.then方法是先判断当前的状态再异步调用响应的函数。假如实例化是传入的函数 里面有异步编程 就会先跳过执行resolve（）或者reject（） 那么状态就一直在等待， 所以then 函数还要对等待中处理 。在等待中我们可以把then 的 2个函数先订阅做个标记添加到电脑中，等异步时间到执行resolve 的时候工作人员在电脑查找一下，就可以直接分配了
<script>
     class promiseA {
       static PENDING = 'pending'
       static FULFILLED = 'fulfilled'
       static REJECTED = 'rejected'
       constructor(fn){
         this.status = promiseA.PENDING
         this.value = null
          fn(this.resolve.bind(this),this.reject.bind(this))
       }
       resolve(value){
         this.status = promiseA.FULFILLED
         this.value = value
       }
       reject(value){
         this.status = promiseA.FULFILLED
         this.value = value
       }
       then(onResolve,onReject){
         if (this.status == promiseA.FULFILLED) {
           onResolve(this.value)
         }
         if (this.status == promiseA.REJECTED) {
           onReject(this.value)
         }
       }
     }

     const PromiseB = new promiseA((resolve,reject)=>{
          resolve('我草你成功了')
          reject('你和他妈的猪一样')
     }).then(value=>{
        console.log(value+'我是resolve传过来的值')
     },(err=>{
        console.log(err+'我是reject传过来的值')
     })
     )
</script>