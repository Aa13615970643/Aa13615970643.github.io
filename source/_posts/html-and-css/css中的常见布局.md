title: 布局
date: 2022-2-6 23:30:09
categories:
- html-css
---
# 垂直居中布局
#### 方法一:最简单的flex 布局
<div class="page">
  <div class="box"></div>
</div>
<style>
  .page{
    width: 100px;
    height: 100px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: black;
  }
  .box{
    background-color: aqua;
    width: 50px;
    height: 50px;
  }
</style> 

```
<style>
  .page{
    width: 500px;
    height: 500px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: white;
  }
  .box{
    background-color: aqua;
    width: 100px;
    height: 100px;
  }
</style>
```

#### 方法二:父相自绝后，子分部向左向上移动本身宽度和高度的一半（也可以用 transform:translate(-50%,-50%)要知道具体的宽度和高度

```

<style>
   .page{
      width: 500px;
    height: 500px;
     position: relative;
     background-color: white;
   }
   .box{
     width: 100px;
     height: 100px;
     position: absolute;
     background-color: aqua;
     top: 50%;
     left: 50%;
     transform: translate(-50%,-50%);
   }
</style>

```
#### 方法三 ：  父向子绝，子元素所有定位为0，margin设置auto自适应。

```
 <style>
   .page{
     position: relative;
   }
   .box{
     position: absolute;
     top: 0;
     left: 0;
     bottom: 0;
     right: 0;
     margin: auto;
   }
 </style>
```


# 圣杯布局
<div class='header'>圣杯布局</div>
<div class="home">
 <div class="main">主体</div>
 <div class="left">左边</div>
 <div class="right">右边</div>
</div>
<div class='footer'>底部</div>
<style>
  body{
    min-width: 400px;
  }
  .header{
    background-color: blue;
  }
 .home{
   background-color: white;
   padding: 0px 100px 0px 100px;
 }
 .main{
   width: 100%;
   background-color: rgb(241, 241, 241);
   float: left;
 }
 .left{
   width: 100px;
   background-color: aqua;
   float: left;
   margin-left: -100%;
   position: relative;
   left: -100px;
 }
 .right{
   float: left;
   width: 100px;
   margin-left: -100px;
   background-color: rgb(137, 206, 81);
   position: relative;
   left: 100px;
 }
 .footer{
   background-color: blue;
   clear: both;
 }
</style>

```
<header>圣杯布局</header>
<div class="home">
 <div class="main">主体</div>
 <div class="left">左边</div>
 <div class="right">右边</div>
</div>
<footer>底部</footer>
<style>
  body{
    min-width: 400px;
  }
  header{
    background-color: blue;
  }
 .home{
   background-color: white;

 }
 .main{
   width: 100%;
   background-color: rgb(241, 241, 241);
   float: left;
 }
 .left{
   width: 100px;
   background-color: aqua;
   float: left;
   margin-left: -100%;
   position: relative;
   left: -100px;
 }
 .right{
   float: left;
   width: 100px;
   margin-left: -100px;
   background-color: rgb(137, 206, 81);
   position: relative;
   left: 100px;
 }
 footer{
   background-color: blue;
   clear: both;
 }
</style>

```


# 双飞翼布局
<div class='header'>双飞翼布局</div>
<div class="home2">
 <div class="main2">
    <div class="main-content2">dd</div>
  </div>
 <div class="left2">左边</div>
 <div class="right2">右边</div>
</div>
<div class='footer'>底部</div>
<style>
   footer{
   background-color: blue;
   clear: both;
 }
   .main-content2{
   margin: 0 100px;
 }
  .body{
    min-width: 400px;
  }
  .header{
    background-color: blue;
  }
 .home2{
   background-color: white;
 }
 .main2{
   width: 100%;
   background-color: rgb(241, 241, 241);
   float: left;
 }
 .left2{
   width: 100px;
   background-color: aqua;
   float: left;
   margin-left: -100%;
 }
 .right2{
   float: left;
   width: 100px;
   margin-left: -100px;
   background-color: rgb(137, 206, 81);

 }

</style>

# 总结：
双飞翼差别就是main 里面加个 div 好margin ， 双飞翼可以优化不用加div直接用怪异盒子然后padding。最简单的还是之间flex布局这布局用来学习用而已



