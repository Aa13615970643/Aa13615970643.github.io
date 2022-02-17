# 箭头函数
定义: 没有对象原型 ，箭头函数不绑定this，会捕获其所在的上下文的this值，作为自己的this值（所以this指向不是调用它的人，而是用调用它的人的this） , 写法简洁
# set
定义:'可以存储任何类型的为一值'相对于数组它的速度更快用于性能优化
## 1.增
<script>
    const add = new Set();
    add.add('value')
</script>
## 2.删除
1.删除指定
```

 <script>
    const setDelete = new Set([1,2,3,4,5,6]);
    setDelete.delete(1)
 </script>
 ```
 2.删除全部
 ```

 <script>
    const setClear = new Set([1,2,3,4,5,6]);
    setClear.clear()
 </script>
 ```
 ## 3.查询
 ```

 <script>
    const setHas = new Set([1,2,3,4,5,6]);
    setHas.has(1)
 </script>
 ```

 ## 4.遍历方法
  <script>
    const set= new Set(['fsdfs',['sdds','dfafds'],3,4,5,6]);
    set.add('ss')
/*     set.forEach((value,set)=>{
      console.log(value)
      console.log(set)
    }) */
    console.log(set)
    var ii = set.values()
    console.log(ii)
    console.log(ii.next().value)
    console.log(ii.next().value)
    console.log(ii.next().value)
    console.log(ii.next().value)
    console.log(ii.next().value)
    console.log(ii.next().value)
    /* 返回一个新的迭代器对象，该对象包含Set对象中的按插入顺序排列的所有元素的值的[value, value]数组。为了使这个方法和Map对象保持相似， 每个值的键和值相等。 */
     console.log(set.values())
     /* 与values()方法相同，返回一个新的迭代器对象，该对象包含Set对象中的按插入顺序排列的所有元素的值。 */
   const oo = [1,1,1,5,5,5]
   console.dir(oo)
 </script>

 
 迭代器对象 next()就可以访问到值了(按顺序手动取值,取一个迭代对象少一个)

 # weakset 
 区别:'它是弱引用类型只能用add 引用类型添加 ,方法和set差不多 遍历方法不能用'
 用途:'主要用来保存对象'
 弱引用：'当对象被引用的时候这个对象就会被标记1 又被别的引用的时候+1 ,但是被弱引用的时候不会加一所以当对象没有被引用了正常来说就报错了但是weakset看着有但实际没有,过段时间就自己清楚了'
 我的理解:'普通的要依靠垃圾回收机制算法回收，weakset只能用引用对象他会自己回收'
 
 ```

 <script>
   const bb = new WeakSet()
   bb.add({name:'55'})
   console.log(bb)
   setTimeout(() => {
     console.log(bb)
   }, 10000);
   
 </script>
```
 # 迭代器和生成器
 ## 内置可迭代对象
String、Array、TypedArray、Map 和 Set 都是内置可迭代对象，因为它们的原型对象都拥有一个 Symbol.iterator 方法。用了之后可以返回一个
迭代器对象就可以用next()
## 生成器
 函数加* 
 变量加yield
 async 就是生成器的语法糖

 # class 修饰器@
 其实就是混入

 # 解构赋值
 # let const
 sda

 # proxy
 对对象get 和 set

 #symbol 唯一值

 # promise

 # class

 # 添加了一些类型的方法
 数组from 可迭代对象 为数组 转数组
 Array.of
 方法用于将一组值，转换为数组。
```

Array.of(3, 11, 8) // [3,11,8]
Array.of(3) // [3]
Array.of(3).length // 1
```
includes() 查找有true
find 查找 返回回调有值
 对象 assgin 对象合并 浅拷贝
