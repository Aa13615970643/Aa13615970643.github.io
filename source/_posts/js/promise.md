# promise 深度理解
# 1.初步了解
promise 有3个状态 分别是等待中 解决 报错 resolve 对应的是结局 reject 对应是报错
promise 实例向构造函数传递一个回调函数 有resolve 和reject 2个函数可以调用 resolve 改变状态 为解决 reject 改变状态为报错 promise 原型上有一个方法叫做then
实例方法调用.then（）传递2 个函数 第一个函数对应接收成功的参数 ，第二个函数接收错误的信息.then方法是先判断当前的状态再异步调用响应的函数。假如实例化是传入的函数 里面有异步编程
就会先跳过执行resolve（）或者reject（） 那么状态就一直在等待， 所以then 函数还要对等待中处理 。在等待中我们可以把then 的 2个函数先订阅做个标记添加到电脑中，等异步时间到执行resolve
的时候工作人员在电脑查找一下，就可以直接分配了

# 第一步
首页我们先创建了一个class类,创建3个静态属性pendding fulfilled rejected ，constructor接收一个方法定义一个value定义一个status，初始化status
的值为pendding，调用方法传入2个class类的方法resolve reject,
这个2个方法分别判断status 是否是等待中 是的话把状态分别改变为fulfilled 和rejected并把传过来的value赋值给this.value，
因为我们是链式操作所以我们在class类上定义了一个then方法,分别接收2个函数， onResolve, onReject。then方法上根据当前状态status来决定执行那个函数并把this.value传过去
这就是初步的promise

# 第二部
处理报错 加入 fn onResolve onReject 函数执行有报错，抛出错误信息调用reject方法并且把错误信息传过去，
then 方法 如果传入不是函数我们就要设置一个默认的函数，onResolve, onReject原生的promise 微任务 ，我们这里直接用宏任务代替,用setimeout 包裹onResolve, onReject
有因为 resolve, reject 是异步的话 那就先执行 .then 方法了但是现在的状态是pendding ,所有我们需要处理下pengding 我们可以先把传过来的方法储存在一个数组里面，等到主线程执行完的执行异步函数
resolve reject的时候异步调用数组里面方法

#第三部 链式操作
.then 是返回一个新的promiseA实例，并且把 onResolve onReject执行的结果传递给给新的promise实例的.then 的onReosolve2

# 第四如果then 返回的是promise
如果then返回的是Promise呢？所以我们需要判断分别处理返回值为Promise与普通值的情况,
如果返回的是promise 实例比如叫a 当前的叫b 调用a的.then方法传入onResolve onReject 在里面调用b的reject 和resolve方法
```

<script>
  class promiseA {
    static PENDING = 'pending'
    static FULFILLED = 'fulfilled'
    static REJECTED = 'rejected'
    constructor(fn) {
      this.status = promiseA.PENDING
      this.value = null
      this.callbacks = [];
      try {
        fn(this.resolve.bind(this), this.reject.bind(this))
      } catch (error) {
        this.reject(error)
      }
    }

    resolve(value) {
      if (this.status == promiseA.PENDING) {
        this.status = promiseA.FULFILLED
        this.value = value
        setTimeout(() => {
          this.callbacks.map(callback => {
            callback.onResolve(value);
          });
        }, 0);

      }

    }

    reject(value) {
      if (this.status == promiseA.PENDING) {
        this.status = promiseA.REJECTED
        this.value = value
        setTimeout(() => {
          this.callbacks.map(callback => {
            callback.onReject(value);
          });
        }, 0);

      }

    }

    then(onResolve, onReject) {
      return new promiseA((resolve, reject) => {
        if (typeof onResolve != "function") {
          onResolve = value => value
        }
        if (typeof onReject != "function") {
          onReject = value => value
        }
        if (this.status == promiseA.PENDING) {
          this.callbacks.push({
            onResolve: value => {
              try {
                let val = onResolve(this.value)
                if (val instanceof promiseA) {
                  val.then(resolve, reject)
                } else {
                  resolve(val)
                }
              } catch (error) {
                reject(error);
              }
            },
            onReject: value => {
              try {
                let val = onReject(this.value)
                if (val instanceof promiseA) {
                  val.then(resolve, reject)
                } else {
                  resolve(val)
                }

              } catch (error) {
                reject(error);
              }
            }
          });
        }
        if (this.status == promiseA.FULFILLED) {
          setTimeout(() => {
            try {
              let val = onResolve(this.value)
              if (val instanceof promiseA) {
                /*            val.then((val)=>{resolve(val)},(val)=>{reject(val)})    */
                /* 简写  */
                val.then(resolve, reject)
              } else {
                resolve(val)
              }

            } catch (error) {
              reject(error)
            }

          }, 0)

        }
        if (this.status == promiseA.REJECTED) {
          setTimeout(() => {
            try {
              let val = onReject(this.value)
              if (val instanceof promiseA) {
                val.then(resolve, reject)
              } else { resolve(val) }

            } catch (error) {
              reject(error)
            }
          }, 0)

        }
      })
    }
  }
  /* 进行对比 */
  const PromiseB = new promiseA((resolve, reject) => {
    resolve('sss')
  })
  PromiseB.then((value) => {
    return new promiseA((resolve)=>{
      resolve('2222222222222')
    });
  }).then((value) => {
    console.log(value)
  })
  /* 原生promise */
  const promiseC = new Promise(() => {
    resolve('aa')
  }).then((value) => {
    console.log(value)
  },(value)=>{
     return new  Promise((resolve)=>{
      resolve('bbbbbbbbbbb')
    }); 
  }).then((val)=>{
    console.log(val)
  })
</script>
```
这样就基本完成了

# 接下来我们优化下代码

```

<script>
  class promiseA {
    static PENDING = 'pending'
    static FULFILLED = 'fulfilled'
    static REJECTED = 'rejected'
    constructor(fn) {
      this.status = promiseA.PENDING
      this.value = null
      this.callbacks = [];
      try {
        fn(this.resolve.bind(this), this.reject.bind(this))
      } catch (error) {
        this.reject(error)
      }
    }

    pare(promise,val,resolve,reject){
       if (promise == val) {
          throw new TypeError('你他妈的滚')
       }
            try {
              if (val instanceof promiseA) {
                val.then(resolve, reject)
              } else { resolve(val) }

            } catch (error) {
              reject(error)
            }

    }
    resolve(value) {
      if (this.status == promiseA.PENDING) {
        this.status = promiseA.FULFILLED
        this.value = value
        setTimeout(() => {
          this.callbacks.map(callback => {
            callback.onResolve(value);
          });
        }, 0);

      }

    }

    reject(value) {
      if (this.status == promiseA.PENDING) {
        this.status = promiseA.REJECTED
        this.value = value
        setTimeout(() => {
          this.callbacks.map(callback => {
            callback.onReject(value);
          });
        }, 0);

      }

    }

    then(onResolve, onReject) {
      let promise = new promiseA((resolve, reject) => {
        if (typeof onResolve != "function") {
          onResolve = value => value
        }
        if (typeof onReject != "function") {
          onReject = value => value
        }
        if (this.status == promiseA.PENDING) {
          this.callbacks.push({
            onResolve: value => {
               this.pare(promise,onResolve(this.value),resolve,reject)
            },
            onReject: value => {
                this.pare(promise,onReject(this.value),resolve,reject)
            }
          });
        }
        if (this.status == promiseA.FULFILLED) {
          setTimeout(() => {
            this.pare(promise,onResolve(this.value),resolve,reject)

          }, 0)

        }
        if (this.status == promiseA.REJECTED) {
          setTimeout(() => {
            this.pare(promise,onReject(this.value),resolve,reject)
      },0)
      }
      })
      return promise
    }
    
  }
  
  /* 进行对比 */
  const PromiseB = new promiseA((resolve, reject) => {
    resolve('sss')
  })
  let a =PromiseB.then((value) => {
     return a
  })
  /* 原生promise */
  const promiseC = new Promise(() => {
    resolve('aa')
  }).then((value) => {
    console.log(value)
  },(value)=>{
     return new  Promise((resolve)=>{
      resolve('bbbbbbbbbbb')
    }); 
  }).then((val)=>{
    console.log(val)
  })
</script>
```

then 方法中两个回调的执行要放到 try...catch 中，不然错误捕获不到被抛出。(但是我不想改)
promise 对象里面不能返回自身

# 实现promise 的静态方法
## 1.resolve 方法
```

 <script>
   promiseA.__proto__.resolve = (value)=>{
      return new promiseA((resolve,reject)=>{
         resolve(value)
      })
   }
 </script>
```
## 2.reject 方法
```

 <script>
   promiseA.__proto__.reject = (value)=>{
      return new promiseA((resolve,reject)=>{
         reject(value)
      })
   }
 </script>
```
## 3 all 方法
```

 <script>
   promiseA.__proto__.all = (promise)=>{
     let arr = []
     return new promiseA((resolve,reject)=>{
       promise.map((promise)=>{
         promise.then((value)=>{
           arr.push(value)
          if (arr.length == promise.length) {
            resolve(arr);
          }
         },reject)
       })
     })
   }
 </script>
```
## race 方法 谁快先执行谁
```

 <script>
   promiseA.__proto__.race = (promise)=>{
     return new promiseA((resolve,reject)=>{
       promise.map((promise)=>{
         promise.then(resolve,reject)
       })
     })
   }
 </script>
 ```

 # 方法测试
 ```

  <script>
      promiseA.resolve('jj').then((value)=>{
        console.log(value)
      })

       promiseA.reject('aa').then(null,(value)=>{
        console.log(value)
      })

      let s = new promiseA((resolve)=>{
        resolve('我是傻逼')
      })

      let b = new promiseA((resolve,reject)=>{
        reject('对你是傻逼')
      })
      let v=[s,b]

      promiseA.all(v).then(value=>{
        console.log(value)
      },(err)=>{
        console.log(err )
      })

      let m = new promiseA ((resolve)=>{
        setTimeout((
        )=>{
          resolve('我最快')
        },100)
      })
      let n = new promiseA ((resolve)=>{
        setTimeout(()=>{
          resolve('我最慢')
        },1000)
      })
      let k = [m,n]
      promiseA.race(k).then((value)=>{
         console.log(value)
      })
      
  </script>
```

# 总结:"其实他妈的就是无限套娃"

<script>  
  for(var i = 0; i < 5; i++){
   function v (){
       setTimeout(()=>{
         console.log(i)
       })
     }
     v()
  }
    

</script>





