title: apply-bind-call
date: 2022-2-8 23:30:09
categories:
- js 手写篇
---

# 手写call
call() 方法在使用一个指定的 this 值和若干个指定的参数值的前提下调用某个函数或方法。

```
<script>
   var foo ={
     value:'我是傻逼'
   }
   function bar(){
     console.log(this.value)
   }
   bar.call(foo)
</script>
```
上面函数bar改变this 指向 指向的是对象foo
上面页可以写成这种形式
## 第一次模拟call
```
<script>
  var foo={
    value:"我是傻逼",
    bar:function(){
      console.log(this.value)
    }
  }
  foo.bar()
</script>
```
这样的话this指向的就是foo对象
但是直接在对象里面添加一个方法明显是不行的
## 第二次模拟 call

```
<script>
var foo={
  value:'你看我像傻子吗'  
}
Function.prototype.call2 = function(val){
    val.fn = this
    val.fn()
    delete val.fn
}
function bar(){
  console.log(this.value)
}
bar.call2(foo)
</script>
```

这样我们在函数的原型对象上定义了一个方法call2方法中的this指向的是调用它的函数bar ，把this的值也就是bar函数赋值给传入的对象的一个方法，因此我们就改变了this的指向然后执行call.fn 然后 再删除，这样就实现了改变this的指向
但是这样远远不够
call 函数还能给定参数执行函数
## 第三次模拟
```

<script>
   let foo ={
     value:"我看你像傻逼"
   }
 Function.prototype.call2 = function(val){
   let args = [...arguments].slice(1)
    val.fn = this
   return val.fn(...args)
}
function bar(name,content){
  console.log(this.value)
  console.log(`${name}:${content}?`)
}
 bar.call2(foo,'我','难道你不是傻逼吗',)
</script>
```
这样就可以传参了,我用es6中的拓展语法简化了操作这样就完成了80%
接下来完善其他功能
## 第四次模拟

<script>
   let value='jjjj'
   let foo ={
     value:"我看你像傻逼"
   }
 Function.prototype.call2 = function(val){
     var val = val||window;
     val.fn = this
     let args = [...arguments].slice(1)
     let result = val.fn(...args)
     delete val.fn
     return result
}
function bar(name,content){
  console.log(this.value)
  console.log(`${name}:${content}?`)
}
bar.call2(null)
</script>

如果为空this 指向window

# call 和apply bind的区别
call 接收参数形式是列表参数
apply 接收参数形式是数组 函数立即执行
bind 传的参数和apply 一样但是它会返回一个函数 要手动执行


