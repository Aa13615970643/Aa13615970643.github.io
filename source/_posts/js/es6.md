# 箭头函数
定义: 没有对象原型 ，箭头函数不绑定this，会捕获其所在的上下文的this值，作为自己的this值（所以this指向不是调用它的人，而是用调用它的人的this） , 写法简洁
# set
定义:'可以存储任何类型的为一值'相对于数组它的速度更快用于性能优化
## 1.增
```

<script>
    const add = new Set();
    add.add('value')
</script>
```
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
 ```

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
 ```

 
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

 # map(可迭代对象)
 定义:对象保存键值对的方式,并且能记住键的原始传入顺序，任何值任何类型都可以作为 一个键或者一个值
 描述:'一个Map对象在迭代时会根据对象中元素的插入顺序来进行 — 一个  for...of 循环在每次迭代后会返回一个形式为[key，value]的数组。'
 ## 和object 的区别
 <table class="standard-table">
 <thead>
  <tr>
   <th scope="row"></th>
   <th scope="col">Map</th>
   <th scope="col">Object</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <th scope="row">意外的键</th>
   <td><code>Map</code> 默认情况不包含任何键。只包含显式插入的键。</td>
   <td>
    <p>一个 <code>Object</code> 有一个原型, 原型链上的键名有可能和你自己在对象上的设置的键名产生冲突。</p>

    <div class="note notecard" id="sect3">
    <p><strong>备注：</strong>虽然 ES5 开始可以用 <code>Object.create(null)</code> 来创建一个没有原型的对象，但是这种用法不太常见。</p>
    </div>
   </td>
  </tr>
  <tr>
   <th scope="row">键的类型</th>
   <td>一个 <code>Map</code>的键可以是<strong>任意值</strong>，包括函数、对象或任意基本类型。</td>
   <td>一个<code>Object</code> 的键必须是一个 <a href="/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String"><code>String</code></a> 或是<a href="/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol"><code>Symbol</code></a>。</td>
  </tr>
  <tr>
   <th scope="row">键的顺序</th>
   <td>
    <p><code>Map</code> 中的 key 是有序的。因此，当迭代的时候，一个 <code>Map</code> 对象以插入的顺序返回键值。</p>
   </td>
   <td>
    <p>一个 <code>Object</code> 的键是无序的</p>

    <div class="note notecard" id="sect4">
    <p><strong>备注：</strong>自ECMAScript 2015规范以来，对象<em>确实</em>保留了字符串和Symbol键的创建顺序； 因此，在只有字符串键的对象上进行迭代将按插入顺序产生键。</p>
    </div>
   </td>
  </tr>
  <tr>
   <th scope="row">Size</th>
   <td>&nbsp;<code>Map</code> 的键值对个数可以轻易地通过<a href="/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Map/size"><code>size</code></a> 属性获取</td>
   <td><code>Object</code> 的键值对个数只能手动计算</td>
  </tr>
  <tr>
   <th scope="row">迭代</th>
   <td><code>Map</code> 是 <a href="/en-US/docs/Web/JavaScript/Reference/Iteration_protocols">iterable</a> 的，所以可以直接被迭代。</td>
   <td>迭代一个<code>Object</code>需要以某种方式获取它的键然后才能迭代。</td>
  </tr>
  <tr>
   <th scope="row">性能</th>
   <td>
    <p>在频繁增删键值对的场景下表现更好。</p>
   </td>
   <td>
    <p>在频繁添加和删除键值对的场景下未作出优化。</p>
   </td>
  </tr>
 </tbody>
</table>

 ## 增
 ```
let myMap = new Map();

let keyObj = {};
let keyFunc = function() {};
let keyString = 'a string';

// 添加键
myMap.set(keyString, "和键'a string'关联的值");
myMap.set(keyObj, "和键keyObj关联的值");
myMap.set(keyFunc, "和键keyFunc关联的值");

myMap.size; // 3
 ```
 ## 取值
 ```
 // 读取值
myMap.get(keyString);    // "和键'a string'关联的值"
myMap.get(keyObj);       // "和键keyObj关联的值"
myMap.get(keyFunc);      // "和键keyFunc关联的值"

myMap.get('a string');   // "和键'a string'关联的值"
                         // 因为keyString === 'a string'
myMap.get({});           // undefined, 因为keyObj !== {}
myMap.get(function() {}); // undefined, 因为keyFunc !== function () {}
```

实例方法和 set 类似就 增值 取值有点不一样
# weakmap
 和weakset 类似它是键只能是对象 也是弱引用

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
