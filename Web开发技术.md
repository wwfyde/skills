# Web开发技术

该文档首要参考文档, MDN

[web开发技术-MDN](https://developer.mozilla.org/zh-CN/docs/Web)

web开发技术-Google

# 核心思想

web级别:布局, 配置, 视图, 路由, 组件, 状态, 工具utils

工程级别: 应用application, 源码source, 构建build, 生成distribute

# HTML

[MDN-HTML](https://developer.mozilla.org/zh-CN/docs/Web/HTML)

## section

## aside

应用场景: aside通常表现为侧边栏、说明、提示、引用、附加注释、广告等。

`<aside>` 标签定义 `<article>` 标签外的内容。

aside 的内容应该与附近的内容相关。

- 两种用法:
  - 在`article`标签内使用
  - 在 `article` 标签外使用





## table	

```html
<table>
    <thead name="table-head"></thead>
    <tbody name="table-body"></tbody>
    <tfoot name="table-foot"></tfoot>
  <tr name="table-row">
    <th name="table-header-cell">Month</th>
    <th name="table-header-cell">Savings</th>
  </tr>
  <tr>
    <td name="table-data-cell">January</td>
    <td>$100</td>
  </tr>
</table>
```

## column-count

column-width



## button

### submit

提交表单, 默认值, 所以点击时会刷新页面

### button



## 专题 - [高阶文字排版](https://developer.mozilla.org/zh-CN/docs/learn/HTML/Introduction_to_HTML/Advanced_text_formatting)

### 描述列表 description lists

文字描述
<dl>
  <dt>内心独白</dt><dd>戏剧中，某个角色对自己的内心活动或感受进行念白表演，这些台词只面向观众，而其他角色不会听到。</dd>
  <dt>语言独白</dt>
    <dd>戏剧中，某个角色把自己的想法直接进行念白表演，观众和其他角色都可以听到。</dd>
  <dt>旁白</dt>
    <dd>戏剧中，为渲染幽默或戏剧性效果而进行的场景之外的补充注释念白，只面向观众，内容一般都是角色的感受、想法、以及一些背景信息等。</dd>
</dl>

### 概要 - summary

    <details>
        <summary>这是概要</summary>
        <p>这是详情这是详情</p>
   </details>

# Web存储

[Web Storage API -MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Web_Storage_API)

Web Storage(Web 存储) 提供了一种方式, 可以让Web页面实现在客户端浏览器中以键值对的形式在本地存储数据. 

*作用*: 在客户端存储数据, 状态保持, 存储元信息, 传统方式采用 `Cookie`实现客户端存储

Web Storage 包含如下两种机制：

- `sessionStorage` 为每一个给定的源（given origin）维持一个独立的存储区域，该存储区域在页面会话期间可用（即只要浏览器处于打开状态，包括页面重新加载和恢复）。
- `localStorage` 同样的功能，但是在浏览器关闭，然后重新打开后数据仍然存在。

这两种机制是通过 [`Window.sessionStorage`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/sessionStorage) 和 [`Window.localStorage`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/localStorage) 属性使用（更确切的说，在支持的浏览器中 `Window` 对象实现了 `WindowLocalStorage` 和 `WindowSessionStorage` 对象并挂在其 `localStorage` 和 `sessionStorage` 属性下）—— 调用其中任一对象会创建 [`Storage`](https://developer.mozilla.org/zh-CN/docs/Web/API/Storage) 对象，通过 [`Storage`](https://developer.mozilla.org/zh-CN/docs/Web/API/Storage) 对象，可以设置、获取和移除数据项。对于每个源（origin）`sessionStorage` 和 `localStorage` 使用不同的 Storage 对象——独立运行和控制。

**注意：**从Firefox 45开始，当浏览器崩溃或重启时，每个源的存储大小将限制在10M，以避免因过度使用web storage引起的内存问题。

**注意：**若用户[禁用第三方cookie](https://support.mozilla.org/en-US/kb/disable-third-party-cookies)，那么将不允许来自第三方IFrames对Web Storage的访问。（从[Firefox 43](https://developer.mozilla.org/en-US/Firefox/Releases/43)版本开始实行）

**注意：**本地存储不同于mozStorage（Mozilla's XPCOM interfaces to SQLite）或[Session store API](https://developer.mozilla.org/en-US/docs/Session_store_API)（an [XPCOM](https://developer.mozilla.org/en-US/docs/XPCOM) storage utility for use by extensions）。

## localStorage

## sessionStorage



# CSS

[MDN-CSS](https://developer.mozilla.org/zh-CN/docs/Web/CSS)

display: display 属性规定元素应该生成的框的类型。

盒子模型 - 传统布局

容器模型 - 新式布局, 基于盒子模型

## 重要说明

```css
/* calss="ant-pro-page-header-wrap wide" */
.ant-pro-page-header-wrap.wide {
    max-width: 1200px;
    margin: 0 auto;
}

/* 添加并覆盖样式 */
        div {
            width: 400px;
            color: #FF0;
        }
        div {
            height: 400px;
        }
        div {
            color: white;
            background-color: black;
            margin: 0 auto;
        }
```



## CSS 优先级

[MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Specificity)



## display

## flex

## white-space - 空白处理方式

wrap 包裹到盒子里

| 值       | 描述                                                         |
| :------- | :----------------------------------------------------------- |
| normal   | 默认。空白会被浏览器忽略。                                   |
| pre      | 空白会被浏览器保留。其行为方式类似 HTML 中的 <pre> 标签。    |
| nowrap   | 文本不会换行，文本会在在同一行上继续，直到遇到 <br> 标签为止。 |
| pre-wrap | 保留空白符序列，但是正常地进行换行。                         |
| pre-line | 合并空白符序列，但是保留换行符。                             |
| inherit  | 规定应该从父元素继承 white-space 属性的值。                  |

## position

| 值                                                           | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [absolute](https://www.runoob.com/css/css-positioning.html#position-absolute) | 生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。 |
| [fixed](https://www.runoob.com/css/css-positioning.html#position-fixed) | 生成固定定位的元素，相对于*浏览器窗口*进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。 |
| [relative](https://www.runoob.com/css/css-positioning.html#position-relative) | 生成相对定位的元素，相对于其正常位置进行定位。因此，"left:20" 会向元素的 LEFT 位置添加 20 像素。 |
| [static](https://www.runoob.com/css/css-positioning.html#position-static) | 默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）。 |
| [sticky](https://www.runoob.com/css/css-positioning.html#position-sticky) | 粘性定位，该定位基于用户滚动的位置。它的行为就像 position:relative; 而当页面滚动超出目标区域时，它的表现就像 position:fixed;，它会固定在目标位置。**注意:** Internet Explorer, Edge 15 及更早 IE 版本不支持 sticky 定位。 Safari 需要使用 -webkit- prefix (查看以下实例)。 |
| inherit                                                      | 规定应该从父元素继承 position 属性的值。                     |
| initial                                                      | 设置该属性为默认值，详情查看 [CSS initial 关键字](https://www.runoob.com/cssref/css-initial.html)。 |

### static - 默认, 没有定位, 正常的文档流中, 方向和z-index 无效

### relative - 相对于默认位置的定位, 偏移, 不会脱离文档流

### absolute - 相对于已有定位的父元素(除了static)

### fixed - 相对于浏览器窗口

相对于窗口居中, 

margin: auto;

margin: 0 auto; 左右居中

margin: auto 0; 上下居中

### sticky - 超出目标区域后, 使用固定定位



## float

## clear

*作用对象*: 浮动的对象

清除浮动, 使脱离的文档流, 回到文档流, 后面的元素就会排列到该元素的背后

单向清除浮动, 浮动内容的单向回到文档流, 单向空间可用

| 值      | 描述                                  |
| :------ | :------------------------------------ |
| left    | 在左侧不允许浮动元素。                |
| right   | 在右侧不允许浮动元素。                |
| both    | 在左右两侧均不允许浮动元素。          |
| none    | 默认值。允许浮动元素出现在两侧。      |
| inherit | 规定应该从父元素继承 clear 属性的值。 |

## 伪类与伪元素

### 伪类 - [L](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Pseudo-classes)

CSS **伪类** 是添加到选择器的关键字，指定要选择的元素的特殊状态。例如，[`:hover`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:hover) 可被用于在用户将鼠标悬停在按钮上时改变按钮的颜色。

```css
/* 所有用户指针悬停的按钮 */
button:hover {
  color: blue;
}
```

伪类连同伪元素一起，他们允许你不仅仅是根据文档 DOM 树中的内容对元素应用样式，而且还允许你根据诸如像导航历史这样的外部因素来应用样式（例如 [`:visited`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:visited)），同样的，可以根据内容的状态（例如在一些表单元素上的 [`:checked`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:checked)），或者鼠标的位置（例如 [`:hover`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:hover) 让你知道是否鼠标在一个元素上悬浮）来应用样式。

**注意：** 与伪类相反，[`pseudo-elements`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/pseudo-elements) 可被用于为一个元素的 *特定部分* 应用样式。

*一个是修饰元素, 一个是修饰类*

### 伪元素 - [L](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Pseudo-elements)

伪元素是一个附加至选择器末的关键词，允许你对被选择元素的特定部分修改样式。下例中的 [`::first-line`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::first-line) 伪元素可改变段落首行文字的样式。

```css
/* 每一个 <p> 元素的第一行。 */
p::first-line {
  color: blue;
  text-transform: uppercase;
}
```

### 区别

伪类与伪元素，傻傻分不清楚。

### **伪类(pseudo-classes)**

官方定义:

> The pseudo-class concept is introduced to permit selection based on information that lies outside of the document tree or that cannot be expressed using the other simple selectors.

其核心就是用来选择那些不能够被普通选择器选择的文档之外的元素，比如:hover。

### **伪元素(Pseudo-elements)**

官方定义:

> Pseudo-elements create abstractions about the document tree beyond those specified by the document language. For instance, document languages do not offer mechanisms to access the first letter or first line of an element’s content. Pseudo-elements allow authors to refer to this otherwise inaccessible information. Pseudo-elements may also provide authors a way to refer to content that does not exist in the source document.

其核心就是需要创建通常不存在于文档中的元素，比如::before。

看了它们的定义应该对它们之间的异同有所了解了吧，呵呵 🙃🙃🙃...

### **伪类与伪元素的区别**

- 表示方法

  CSS2 中伪类、伪元素都是以单冒号`:`表示，CSS2.1 后规定伪类用单冒号表示，伪元素用双冒号`::`表示，浏览器同样接受 CSS2 时代已经存在的伪元素(:before, :after, :first-line, :first-letter 等)的单冒号写法。对于 CSS2 之后所有新增的伪元素(如::selection)，应该采用双冒号的写法。但是因为兼容性问题，大部分还是用的单冒号。

- 定义不同

  **伪类即假的类，通常可以添加类来达到效果，伪元素即假元素，需要通过添加元素才能达到效果。**来看下面的例子

  **例 1:将一行字符串的首字母变成红色**

  现在不用伪元素应该如何实现？用 CSS slector 选择？想了一晚上也没想出来，既然没法选择也就没法添加一个类来改变首字母的颜色。

  ```
  <p>I am snow</p>
  复制代码
  ```

  添加元素试试，如下，创建一个元素 span 将首字母包裹起来，进而改变其颜色，成功了。这里，关键点在于我们创建了新的元素达到了`::first-letter`的作用，且不能通过添加其他类来实现这一效果，因此将`::first-letter`叫做伪元素而不是伪类。

  ```
    <p><span style={{ color: red }}>I<span/> am snow</p>
  复制代码
  ```

  **例 2: 如下要将 I am snow 这句话变为红色**

  很简单用`:first-child`，同样添加一个类试试，显然很容易达到同样效果，我们并没有创建新的元素只是添加了一个类`.red-line`，因此将`:first-child`叫做伪类而不是伪元素，尽管它和`::first-letter`在语义上十分相似。

  ```
  div:first-child {
   color: red;
  }
  或
  .red-line {
     color: red;
  }
  
  <div class='red-line'>
   <p>I am snow</p>
  <div>
  复制代码
  ```

### **结论**

- 伪类和伪元素都是用来表示文档树以外的"元素"。
- 伪类和伪元素分别用单冒号`:`和双冒号`::`来表示。
- 伪类和伪元素的区别，最关键的点在于如果没有伪元素(或伪类)，是否需要添加元素才能达到目的，如果是则是伪元素，反之则是伪类。

关于常用的伪类与伪元素选择器可以查看[CSS选择器](https://juejin.im/post/5c99d0eee51d4510df61601a)一文。


作者：林晨熙
链接：https://juejin.im/post/5ca19f176fb9a05e711b2132
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

## `::before` - [伪元素](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::before)



CSS中，**`::before`** 创建一个[伪元素](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements)，其将成为匹配选中的元素的第一个子元素。常通过 [`content`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/content) 属性来为一个元素添加修饰性的内容。此元素默认为行内元素。

```
/* Add a heart before links */
a::before {
  content: "♥";
}
```

**注意:** 由`::before` 和`::after` 生成的伪元素 [包含在元素格式框内](https://www.w3.org/TR/CSS2/generate.html#before-after-content)， 因此不能应用在[替换元素上](https://developer.mozilla.org/en-US/docs/Web/CSS/Replaced_element)， 比如[`<img>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/img) 或 [`<br>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/br) 元素。

## :root - 根元素

**`:root`** 这个 CSS [伪类](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Pseudo-classes)匹配文档树的根元素。对于 HTML 来说，**`:root`** 表示 [``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/html) 元素，除了[优先级](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Specificity)更高之外，与 `html` 选择器相同。



## input

### autocomplete

`autocomplet="off"` 关闭表单历史记录

`autocomplete="on"` 默认, 打开表单记录



## box-sizing

[MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-sizing)

[CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) 中的 **`box-sizing`** 属性定义了 [user agent](https://developer.mozilla.org/zh-CN/docs/Glossary/User_agent) 应该如何计算一个元素的总宽度和总高度。

在 [CSS 盒子模型](https://developer.mozilla.org/en-US/docs/CSS/Box_model)的默认定义里，你对一个元素所设置的 [`width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/width) 与 [`height`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/height) 只会应用到这个元素的内容区。如果这个元素有任何的 [`border`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border) 或 [`padding`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding) ，绘制到屏幕上时的盒子宽度和高度会加上设置的边框和内边距值。这意味着当你调整一个元素的宽度和高度时需要时刻注意到这个元素的边框和内边距。当我们实现响应式布局时，这个特点尤其烦人。

box-sizing 属性可以被用来调整这些表现:

- `content-box` 是默认值。如果你设置一个元素的宽为100px，那么这个元素的内容区会有100px 宽，并且任何边框和内边距的宽度都会被增加到最后绘制出来的元素宽度中。
- `border-box` 告诉浏览器：你想要设置的边框和内边距的值是包含在width内的。也就是说，如果你将一个元素的width设为100px，那么这100px会包含它的border和padding，内容区的实际宽度是width减去(border + padding)的值。大多数情况下，这使得我们更容易地设定一个元素的宽高。

## font-size

[MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-size)

**`font-size`** [CSS](https://developer.mozilla.org/zh-CN/docs/CSS) 属性指定字体的大小。因为该属性的值会被用于计算em和ex长度单位，定义该值可能改变其他元素的大小。	

```css
/* <absolute-size>，绝对大小值 */
font-size: xx-small;
font-size: x-small;
font-size: small;
font-size: medium;
font-size: large;
font-size: x-large;
font-size: xx-large;

/* <relative-size>，相对大小值 */
font-size: larger;
font-size: smaller;

/* <length>，长度值 */
font-size: 12px;
font-size: 0.8em;

/* <percentage>，百分比值 */
font-size: 80%;

/* 继承父元素*/
font-size: inherit;
```



# CSS

## layout-布局

### 盒子模型

[MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)

## 常见问题

盒子尺寸 : content + border + padding (不包含 margin)

### grid system 栅格

![img](https://wwfyde.oss-cn-hangzhou.aliyuncs.com/images/20210427103641.png)

## 工作原理

布局的栅格化系统，我们是基于行（row）和列（col）来定义信息区块的外部框架，以保证页面的每个区域能够稳健地排布起来。下面简单介绍一下它的工作原理：

- 通过`row`在水平方向建立一组`column`（简写col）
- 你的内容应当放置于`col`内，并且，只有`col`可以作为`row`的直接元素
- 栅格系统中的列是指 1 到 24 的值来表示其跨越的范围。例如，三个等宽的列可以使用 `<a-col :span="8" />` 来创建
- 如果一个`row`中的`col`总和超过 24，那么多余的`col`会作为一个整体另起一行排列

### 



## 最佳实践

一般建议 1-4 个栅格即可

1, 1:1, 1:1:1 , 2:1, 1:3



### 传统布局

[参考链接](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

布局的传统解决方案, 基于 盒装模型 , 依赖 `display` + `position` + `float` 属性,

缺陷是无法满足 垂直居中等布局

### Flex 布局

> flexible box - 弹性布局 - 用来为盒状模型提供最大的灵活性。

该模型更加强调, 父子关系, 所以显得比传统布局更加灵活,  

[参考链接](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

[A Complete Guide of Flexible](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

[参考链接](https://scotch.io/tutorials/a-visual-guide-to-css3-flexbox-properties)

我们的栅格化系统支持 Flex 布局，允许子元素在父节点内的水平对齐方式 - 居左、居中、居右、等宽排列、分散排列。子元素与子元素之间，支持顶部对齐、垂直居中对齐、底部对齐的方式。同时，支持使用 order 来定义元素的排列顺序。

Flex 布局是基于 24 栅格来定义每一个『盒子』的宽度，但不拘泥于栅格。

```css
.container {
    display: flex;  // 将容器设置为行内布局
    display: -webkit-flex;  /* Safari 支持 */
    display: inline-flex;  //行内元素的 flex布局
}
```

**设置为弹性布局后, 子元素的 `float` `clear` 和 `vertical-align` 属性都将失效. **

## 基本概念

采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。

![img](https://wwfyde.oss-cn-hangzhou.aliyuncs.com/images/20210427103654.png)

容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做`main start`，结束位置叫做`main end`；交叉轴的开始位置叫做`cross start`，结束位置叫做`cross end`。

项目默认沿主轴排列。单个项目占据的主轴空间叫做`main size`，占据的交叉轴空间叫做`cross size`。

## 容器属性

以下6个属性设置在容器上。

- flex-direction: 
- flex-wrap: 
- flex-flow
- justify-content
- align-items
- align-content

### flex-direction属性

`flex-direction`属性决定主轴的方向（即项目的排列方向）。

> ```css
> .box {
> flex-direction: row | row-reverse | column | column-reverse;
> }
> ```

- row（默认值）：主轴为水平方向，起点在左端。
- row-reverse：主轴为水平方向，起点在右端。
- column：主轴为垂直方向，起点在上沿。
- column-reverse：主轴为垂直方向，起点在下沿。

### flex-wrap属性

默认情况下，项目都排在一条线（又称"轴线"）上。`flex-wrap`属性定义，如果一条轴线排不下，如何换行。

![img](https://wwfyde.oss-cn-hangzhou.aliyuncs.com/images/20210427103658.png)

> ```css
> .box{
> flex-wrap: nowrap | wrap | wrap-reverse;
> }
> ```

它可能取三个值。

（1）`nowrap`（默认）：不换行。

![img](https://wwfyde.oss-cn-hangzhou.aliyuncs.com/images/20210427103725.png)

（2）`wrap`：换行，第一行在上方。

![img](https://wwfyde.oss-cn-hangzhou.aliyuncs.com/images/20210427103716.jpg)

（3）`wrap-reverse`：换行，第一行在下方。

![img](https://wwfyde.oss-cn-hangzhou.aliyuncs.com/images/20210427103729.jpg)

### flex-flow

`flex-flow`属性是`flex-direction`属性和`flex-wrap`属性的简写形式，默认值为`row nowrap`。

> ```css
> .box {
> flex-flow: <flex-direction> || <flex-wrap>;
> }
> ```

### justify-content属性

`justify-content`属性定义了项目在主轴上的对齐方式。

> ```css
> .box {
> justify-content: flex-start | flex-end | center | space-between | space-around;
> }
> ```

![img](https://wwfyde.oss-cn-hangzhou.aliyuncs.com/images/20210427103734.png)

它可能取5个值，具体对齐方式与轴的方向有关。下面假设主轴为从左到右。

> - `flex-start`（默认值）：左对齐
> - `flex-end`：右对齐
> - `center`： 居中
> - `space-between`：两端对齐，项目之间的间隔都相等。
> - `space-around`：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

### align-items属性

align-items 属性定义flex子项在flex容器的当前行的侧轴（纵轴）方向上的对齐方式。

**提示：**使用每个弹性对象元素的 align-self 属性可重写 align-items 属性。

`align-items`属性定义项目在交叉轴上如何对齐。

> ```css
> .box {
> align-items: flex-start | flex-end | center | baseline | stretch;
> }
> ```

| 值         | 描述                                                         |
| :--------- | :----------------------------------------------------------- |
| stretch    | 默认值。元素被拉伸以适应容器。如果指定侧轴大小的属性值为'auto'，则其值会使项目的边距盒的尺寸尽可能接近所在行的尺寸，但同时会遵照'min/max-width/height'属性的限制。 |
| center     | 元素位于容器的中心。弹性盒子元素在该行的侧轴（纵轴）上居中放置。（如果该行的尺寸小于弹性盒子元素的尺寸，则会向两个方向溢出相同的长度）。 |
| flex-start | 元素位于容器的开头。弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴起始边界。 |
| flex-end   | 元素位于容器的结尾。弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴结束边界。 |
| baseline   | 元素位于容器的基线上。如弹性盒子元素的行内轴与侧轴为同一条，则该值与'flex-start'等效。其它情况下，该值将参与基线对齐。 |
| initial    | 设置该属性为它的默认值。请参阅 [*initial*](https://www.runoob.com/cssref/css-initial.html)。 |
| inherit    | 从父元素继承该属性。请参阅 [*inherit*](https://www.runoob.com/cssref/css-inherit.html)。 |

![img](https://wwfyde.oss-cn-hangzhou.aliyuncs.com/images/20210427103740.png)

它可能取5个值。具体的对齐方式与交叉轴的方向有关，下面假设交叉轴从上到下。

> - `flex-start`：交叉轴的起点对齐。
> - `flex-end`：交叉轴的终点对齐。
> - `center`：交叉轴的中点对齐。
> - `baseline`: 项目的第一行文字的基线对齐。
> - `stretch`（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。

### align-content属性

`align-content`属性定义了两根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

同时指定了宽度和高度才会生效, 解决垂直方向的对齐方式. 

默认是伸展(空白空间, 平均分配为间隔)

> ```css
> .box {
> align-content: flex-start | flex-end | center | space-between | space-around | stretch;
> }
> ```

| 值            | 描述                                                         |
| :------------ | :----------------------------------------------------------- |
| stretch       | 默认值。元素被拉伸以适应容器。各行将会伸展以占用剩余的空间。如果剩余的空间是负数，该值等效于'flex-start'。在其它情况下，剩余空间被所有行平分，以扩大它们的侧轴尺寸。 |
| center        | 元素位于容器的中心。各行向弹性盒容器的中间位置堆叠。各行两两紧靠住同时在弹性盒容器中居中对齐，保持弹性盒容器的侧轴起始内容边界和第一行之间的距离与该容器的侧轴结束内容边界与第最后一行之间的距离相等。（如果剩下的空间是负数，则各行会向两个方向溢出的相等距离。） |
| flex-start    | 元素位于容器的开头。各行向弹性盒容器的起始位置堆叠。弹性盒容器中第一行的侧轴起始边界紧靠住该弹性盒容器的侧轴起始边界，之后的每一行都紧靠住前面一行。 |
| flex-end      | 元素位于容器的结尾。各行向弹性盒容器的结束位置堆叠。弹性盒容器中最后一行的侧轴起结束界紧靠住该弹性盒容器的侧轴结束边界，之后的每一行都紧靠住前面一行。 |
| space-between | 元素位于各行之间留有空白的容器内。各行在弹性盒容器中平均分布。如果剩余的空间是负数或弹性盒容器中只有一行，该值等效于'flex-start'。在其它情况下，第一行的侧轴起始边界紧靠住弹性盒容器的侧轴起始内容边界，最后一行的侧轴结束边界紧靠住弹性盒容器的侧轴结束内容边界，剩余的行则按一定方式在弹性盒窗口中排列，以保持两两之间的空间相等。 |
| space-around  | 元素位于各行之前、之间、之后都留有空白的容器内。各行在弹性盒容器中平均分布，两端保留子元素与子元素之间间距大小的一半。如果剩余的空间是负数或弹性盒容器中只有一行，该值等效于'center'。在其它情况下，各行会按一定方式在弹性盒容器中排列，以保持两两之间的空间相等，同时第一行前面及最后一行后面的空间是其他空间的一半。 |
| initial       | 设置该属性为它的默认值。请参阅 [*initial*](https://www.runoob.com/cssref/css-initial.html)。 |
| inherit       | 从父元素继承该属性。请参阅 [*inherit*](https://www.runoob.com/cssref/css-inherit.html)。 |

![img](https://wwfyde.oss-cn-hangzhou.aliyuncs.com/images/20210427103747.png)

该属性可能取6个值。

> - `flex-start`：与交叉轴的起点对齐。
> - `flex-end`：与交叉轴的终点对齐。
> - `center`：与交叉轴的中点对齐。
> - `space-between`：与交叉轴两端对齐，轴线之间的间隔平均分布。
> - `space-around`：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
> - `stretch`（默认值）：轴线占满整个交叉轴。

## 项目属性 - item

以下6个属性设置在项目上。

- `order`
- `flex-grow`
- `flex-shrink`
- `flex-basis`
- `flex`
- `align-self`

### order属性

`order`属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。

控制item在容器中的排雷

> ```css
> .item {
> order: <integer>;
> }
> ```

![img](https://wwfyde.oss-cn-hangzhou.aliyuncs.com/images/20210427103752.png)

### flex-grow属性

放大属性, 填充剩余空间.

`flex-grow`属性定义项目的放大比例，默认为`0`，即如果存在剩余空间，也不放大。

> ```css
> .item {
> flex-grow: <number>; /* default 0 */
> }
> ```

![img](https://wwfyde.oss-cn-hangzhou.aliyuncs.com/images/20210427103758.png)

如果所有项目的`flex-grow`属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的`flex-grow`属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。

### flex-shrink属性

> 如果空间不足, 缩小该item

`flex-shrink`属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。

> ```css
> .item {
> flex-shrink: <number>; /* default 1 */
> }
> ```

![img](https://wwfyde.oss-cn-hangzhou.aliyuncs.com/images/20210427103802.png)

如果所有项目的`flex-shrink`属性都为1，当空间不足时，都将等比例缩小。如果一个项目的`flex-shrink`属性为0，其他项目都为1，则空间不足时，前者不缩小。

负值对该属性无效。

### flex-basis属性

> 基础空间: 设置项目占用空间

`flex-basis`属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为`auto`，即项目的本来大小。

> ```css
> .item {
> flex-basis: <length> | auto; /* default auto */
> }
> ```

它可以设为跟`width`或`height`属性一样的值（比如350px），则项目将占据固定空间。

### flex属性

`flex`属性是`flex-grow`, `flex-shrink` 和 `flex-basis`的简写，默认值为`0 1 auto`。后两个属性可选。

> ```css
> .item {
> flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
> }
> ```

该属性有两个快捷值：`auto` (`1 1 auto`) 和 none (`0 0 auto`)。

建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

### align-self属性

align-self 属性定义flex子项单独在侧轴（纵轴）方向上的对齐方式。

**注意：**align-self 属性可重写灵活容器的 align-items 属性。

`align-self`属性允许单个项目有与其他项目不一样的对齐方式，可覆盖`align-items`属性。默认值为`auto`，表示继承父元素的`align-items`属性，如果没有父元素，则等同于`stretch`。

> ```css
> .item {
> align-self: auto | flex-start | flex-end | center | baseline | stretch;
> }
> ```

![img](https://wwfyde.oss-cn-hangzhou.aliyuncs.com/images/20210427103807.jpg)

该属性可能取6个值，除了auto，其他都与align-items属性完全一致。





# 响应式布局

> 参考 极客时间 - Vue开发实践 - 37丨实现一个可动态改变的页面布局

需求 : 

# 单位

[MDN](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Values_and_units)

[参考文档- 第三方](https://www.cnblogs.com/theblogs/p/10516098.html)

em : element

px : pixel

rem : root element



## px

px就是pixel像素的缩写，相对长度单位，网页设计常用的基本单位。像素px是相对于显示器屏幕分辨率而言的

## em

```html
em = 希望得到的像素大小 / 父元素字体像素大小
```

em是相对长度单位。相对于当前对象内文本的字体尺寸（**参考物是父元素的font-size**）

如当前父元素的字体尺寸未设置，则相对于浏览器的默认字体尺寸

特点：

  　　1. em的值并不是固定的；

  　　2. em会继承父级元素的字体大小

## rem

**rem**

rem是CSS3新增的一个相对单位，rem是相对于HTML根元素的字体大小（font-size）来计算的长度单位

如果你没有设置html的字体大小，就会以浏览器默认字体大小，一般是16px

```
html{font-size: 62.5%}  /* 10 ÷ 16 × 100% = 62.5% */

body{font-size: 1.4rem;} /* 1.4 × 10px = 14px *//*在根元素中定义了一个基本字体大小为62.5%（也就是10px。设置这个值主要方便计算，如果没有设置，将是以“16px”为基准 ）*/
```

优点是，只需要设置根目录的大小就可以把整个页面的成比例的调好

rem兼容性：除了IE8及更早版本外，所有浏览器均已支持rem

em与rem的区别：

　　rem是相对于根元素（html）的字体大小，而em是相对于其父元素的字体大小

两者使用规则：

- 如果这个属性根据它的font-size进行测量，则使用em``
- 其他的一切事物属性均使用rem

## %

其他单位：

**%**（百分比）

一般来说就是相对于父元素

1、对于普通定位元素就是我们理解的父元素

2、对于position: absolute;的元素是相对于已定位的父元素

3、对于position: fixed;的元素是相对于ViewPort（可视窗口）

## **vw、vh**

vw、vh、vmax、vmin这四个单位都是基于视口

vw是相对视口（viewport）的宽度而定的，长度等于视口宽度的`1/100`

假如浏览器的宽度为200px，那么1vw就等于2px（200px/100）

vh是相对视口（viewport）的高度而定的，长度等于视口高度的`1/100`

假如浏览器的高度为500px，那么1vh就等于5px（500px/100）

vmin和`vmax`是相对于视口的高度和宽度两者之间的`最小值`或`最大值`

```
/*
如果浏览器的高为300px、宽为500px，那么1vmin就是3px，1vmax就是5px；如果浏览器的高为800px，宽为1080px，那么1vmin也是8px，1vmax也是10.8px
*/
```

## **vm**

css3新单位，相对于视口的宽度或高度中较小的那个

其中最小的那个被均分为100单位的vm

比如：浏览器高度900px，宽度1200px，取最小的浏览器高度，1 vm = 900px/100 = 9 px

缺点：兼容性差

## 常见问题

1、假如使用em来设置文字大小要注意什么？

注意父元素的字体大小，因为em是根据父元素的大小来设置的。

比如同样是1.5em，要是父元素是20，那1.5em就是30px.要是父元素是30px,1.5em就是45px（特别是在多重div嵌套里面更要注意）

2、pc pt ch一般用在什么场景？

这些我们网页设计基本上用不到，在排版上会有用处

3、如何使 1rem=10px

在设置HTML{font-size：62.5%；}即可

4、如果父元素没有指定高度，那么子元素的百分比的高度是多少？

会按照子元素的实际高度，设置百分比则没有效果

# CSS - 最佳实践

> - 阿里技术 - [CSS布局技巧](https://mp.weixin.qq.com/s/9f4UaZWzYSJB_ZdwhS3A3A)

# DOM

# HTTP

[MDN-HTTP](https://developer.mozilla.org/zh-CN/docs/Web/HTTP)

## GET or POST

使用 `POST` 的情况

无法使用缓存文件(更新服务器上的文件或数据库)

向服务器发送大量数据(POST没有数据量限制)

发送包含未知字符的用户输入时, `POST` 比 `GET` 更稳定也更可靠

# JavaScript



## Ajax/axios

运行原理: Ajax 相当于浏览器发送请求与接收响应的代理人，以实现在不影响用户浏览页面的情况下，局部更新页面数据，从而提高用户体验。

在真实的项目中，服务器端大多数情况下会以 JSON 对象作为响应数据的格式。当客户端拿到响应数据时，要将 JSON 数据和 HTML 字符串进行拼接，然后将拼接的结果展示在页面中。

### 应用场景

1.页面上拉加载更多数据

2.列表数据无刷新分页

3.表单项离开焦点数据验证

4.搜索框提示文字下拉列表

## 常用接口

setInterval()

setTimeout()



# Nodejs