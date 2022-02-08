title: flex布局
date: 2022-2-6 23:30:09
categories:
- html-css
---
# flex
## 定义在爸爸
1.flex-direction 设置主轴的属性有：横轴 纵轴 反横轴 反纵轴
2.justify-content  主要设置主轴的对其方式：向前 向后 剧中 平均 2边靠底平均
3.align-items 设置副轴的对其方式：同上（3） baseline：如弹性盒子元素的行内轴与侧轴为同一条，则该值与'flex-start'等效。其它情况下，该值将参与基线对齐。
stretch：如果指定侧轴大小的属性值为'auto'，则其值会使项目的边距盒

的尺寸尽可能接近所在行的尺寸，但同时会遵照'min/max-width/height'属性的限制
4.flex-warp 是否换行： 默认不 warp 换 还有个反转换
5.align-content：和items 区别适合多行 items 单行
## 定义子儿子
6.align-self：他们都是定义在爸爸上你是定义在儿子上的
[ flex-grow ]：定义弹性盒子元素的扩展比率。
[ flex-shrink ]：定义弹性盒子元素的收缩比率。
[ flex-basis ]：定义弹性盒子元素的默认基准值
flex：1 上面3个属性的集合
order 排序顺序值越小排越前面
