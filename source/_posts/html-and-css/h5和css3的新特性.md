# html5
## 1.语义化标签
| 标签 | 描述 |
| ------ | ----------- |
| header | 一般定义在文档的头部 |
| footer | 一般定义在文档区域底部 |
| nav | 一般定义文档的导航栏 |
| aside | 侧边内容 |
| section | 节点 |
| article | 文章 |
| details |详情 |
| summary |标题摘要 |
| dialog | 对话框 |
## 2.增强型表单
<table>
<thead>
<tr><th>input 的 type</th><th>描述</th></tr>
</thead>
<tbody>
<tr>
<td>color</td>
<td>主要用于选取颜色</td>
</tr>
<tr>
<td>date</td>
<td>从一个日期选择器选择一个日期</td>
</tr>
<tr>
<td>datetime</td>
<td>选择一个日期（UTC 时间）</td>
</tr>
<tr>
<td>email</td>
<td>包含 e-mail 地址的输入域</td>
</tr>
<tr>
<td>month</td>
<td>选择一个月份</td>
</tr>
<tr>
<td>number</td>
<td>数值的输入域</td>
</tr>
<tr>
<td>range</td>
<td>一定范围内数字值的输入域</td>
</tr>
<tr>
<td>search</td>
<td>用于搜索域</td>
</tr>
<tr>
<td>tel</td>
<td>定义输入电话号码字段</td>
</tr>
<tr>
<td>time</td>
<td>选择一个时间</td>
</tr>
<tr>
<td>url</td>
<td>URL 地址的输入域</td>
</tr>
<tr>
<td>week</td>
<td>选择周和年</td>
</tr>
</tbody>
</table>
## 2.也新增以下表单元素
<table>
<thead>
<tr><th>表单元素</th><th>描述</th></tr>
</thead>
<tbody>
<tr>
<td>datalist</td>
<td>元素规定输入域的选项列表，使用 input 元素的 list 属性与 datalist 元素的 id 绑定</td>
</tr>
<tr>
<td>keygen</td>
<td>提供一种验证用户的可靠方法，标签规定用于表单的密钥对生成器字段</td>
</tr>
<tr>
<td>output</td>
<td>用于不同类型的输出，比如计算或脚本输出</td>
</tr>
</tbody>
</table>
## html5 新事件
<table>
<thead>
<tr><th>事件</th><th>描述</th></tr>
</thead>
<tbody>
<tr>
<td>onresize</td>
<td>当调整窗口大小时运行脚本</td>
</tr>
<tr>
<td>ondrag</td>
<td>当拖动元素时运行脚本</td>
</tr>
<tr>
<td>onscroll</td>
<td>当滚动元素滚动元素的滚动条时运行脚本</td>
</tr>
<tr>
<td>onmousewheel</td>
<td>当转动鼠标滚轮时运行脚本</td>
</tr>
<tr>
<td>onerror</td>
<td>当错误发生时运行脚本</td>
</tr>
<tr>
<td>onplay</td>
<td>当媒介数据将要开始播放时运行脚本</td>
</tr>
<tr>
<td>onpause</td>
<td>当媒介数据暂停时运行脚本</td>
</tr>
</tbody>
</table>

1. 块级元素div、p、h1~h6、ul、ol、dl、li、dd、table、hr、blockquote、address、table、menu、pre，HTML5 新增的 header、section、aside、footer 等

2. 行内元素pan、img、a、lable、input、abbr（缩写）、em（强调）、big、cite（引用）、i（斜体）、q（短引用）、textarea、select、small、sub、sup，strong、u（下划线）、button

# css3 新特性
选择器
背景和边框
文本效果
2D/3D 转换
动画、过渡
多列布局
用户界面
## 1.选择器
1. :last-child /* 选择元素最后一个孩子 */
2. :first-child /* 选择元素第一个孩子 */
3. :nth-child(1) /* 按照第几个孩子给它设置样式 */
4. :nth-child(even) /* 按照偶数 */
5. :nth-child(odd)  /* 按照奇数 */
6. :disabled /* 选择每个禁用的E元素 */
7. :checked /* 选择每个被选中的E元素 */
8. :not(selector) /* 选择非 selector 元素的每个元素 */
9. ::selection /* 选择被用户选取的元素部分 */

## 2.背景和边框
## 3.文本属性
## transition 和 animation 一些动画方法
## 多列布局
1. column-count: 规定元素应该被分隔的列数
2. column-gap: 规定列之间的间隔
3. column-rule: 设置列之间的宽度、样式和颜色规则

## 用户界面
1. resize 属性规定是否可由用户调整元素尺寸。如果希望此属性生效，需要设置元素的 overflow 属性，值可以是 auto、hidden 或 scroll

2. box-sizing 属性可设置的值有 content-box、border-box 和 inherit
content-box 是W3C的标准盒模型，元素宽度 = 内容宽度 + padding + border：意思是 padding 和 border 会增加元素的宽度，以至于实际上的 width 大于原始设定的 width
border-box 是ie的怪异盒模型，元素宽度 = 设定的宽度，已经将 padding 和 border 包括进去了，比如有时候在元素基础上添加内距 padding 或 border 会将布局撑破，但是使用 border-box 就可以轻松完成
inherit：规定应从父元素继承 box-sizing 属性的值

3. outline-offset 属性对轮廓进行偏移，并在超出边框边缘的位置绘制轮廓