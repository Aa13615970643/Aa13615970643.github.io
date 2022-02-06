title: Categories
date: 2013-12-24 23:30:09
categories:
- Foo
- Bar
- Baz
---

# 盒子模型和BFC
### 1.什么是盒子模型
在html中所有的元素都是一个盒子,这个盒子由内容（content）宽度
边框（border）（with）内边距（padding） 外边距（marign）组成
### 2.盒子模型的类型
#### 1.标准的盒子模型：一个盒子的总宽度：with+border+padding+margin
#### 2.怪异的盒子模型：一个盒子的总宽度：with+margin
### 3.盒子之间的转换
1. 使用怪异盒子：box-sizing：border-box
2. 使用标准盒子：box-sizing：content-box
3. box-sizing:inherit; 规定应从父元素继承 box-sizing 属性的值。
# BFC
### 1.双边距（边距重叠）
#### 1.父子关系边距重叠
<div class='a'>
    <div class="b"></div>
</div>

<style>
.a{
  width: 200px;
  height: 200px;
  background-color: aqua;
}
.b{
  width: 100px;
  height: 100px;
  background-color: white;
  margin-top: 50px;
}
</style>
```
  <div class='a'>
    <div class="b"></div>
</div>

<style>
.c{
  width: 200px;
  height: 200px;
  background-color: aqua;
}
.d{
  width: 100px;
  height: 100px;
  background-color: black; 
}
</style>
```
我们可以看到上面的代码在没有BFC的情况下子元素的margin 被父元素继承了
解决的方法就是让它的父元素变成BFC overflow:hidden
<div class='c'>
    <div class="d"></div>
</div>

<style>
.c{
  width: 200px;
  height: 200px;
  background-color: aqua;
  overflow: hidden;
}
.d{
  width: 100px;
  height: 100px;
  background-color: white;
  margin-top: 50px;
}
</style>
```
<div class='c'>
    <div class="d"></div>
</div>

<style>
.c{
  width: 200px;
  height: 200px;
  background-color: aqua;
  overflow: hidden;
}
.d{
  width: 100px;
  height: 100px;
  background-color: white;
  margin-top: 50px;
}
</style>
```
这样就没有问题了
#### 2.兄弟关系关系边距重叠
  <style type="text/css">
            .fat {
                background-color: #ccc;
            }
            .fat .child-one {
                width: 100px;
                height: 100px;
                margin-bottom: 50px;
                background-color: #f00;
            }

            .fat .child-two {
                width: 100px;
                height: 100px;
                margin-top: 50px;
                background-color: #345890;
            }
        </style>
   <section class="fat">
        <div class="child-one"></div>
        <div class="child-two"></div>
    </section>

```
 <style type="text/css">
            .fat {
                background-color: #ccc;
            }
            .fat .child-one {
                width: 100px;
                height: 100px;
                margin-bottom: 50px;
                background-color: #f00;
            }

            .fat .child-two {
                width: 100px;
                height: 100px;
                margin-top: 50px;
                background-color: #345890;
            }
        </style>
   <section class="fat">
        <div class="child-one"></div>
        <div class="child-two"></div>
    </section>
```
 这样的话下面的margin-top就无效了
 解决方法：可通过添加空元素或伪类元素，设置overflow:hidden;解决margin重叠问题
   <style type="text/css">
            .fat {
                background-color: #ccc;
            }
            .fat .child-one {
                width: 100px;
                height: 100px;
                margin-bottom: 50px;
                background-color: #f00;
            }

            .fat .child-two {
                width: 100px;
                height: 100px;
                margin-top: 50px;
                background-color: #345890;
            }
        </style>
   <section class="fat">
        <div class="child-one"></div>
         <div style="overflow: hidden;"></div>
        <div class="child-two"></div>
    </section>

```
 <style type="text/css">
            .fat {
                background-color: #ccc;
            }
            .fat .child-one {
                width: 100px;
                height: 100px;
                margin-bottom: 50px;
                background-color: #f00;
            }

            .fat .child-two {
                width: 100px;
                height: 100px;
                margin-top: 50px;
                background-color: #345890;
            }
        </style>
   <section class="fat">
        <div class="child-one"></div>
        <div style="overflow: hidden;"></div>
        <div class="child-two"></div>
    </section>
```
### 2.什么是BFC 呢
BFC就是块级格式化上下文，保证是一个独立的布局环境不受外部影响，也不影响外部
### 3.如何出发BFC
```
<style>
  v{
    overflow: hidden;
    overflow: auto;
    float: right;
    float: left;
    position: absolute;
    position: fixed;
    display: inline-block/ table-cell/ table-caption/ flex/ inline-flex
  }
</style>
