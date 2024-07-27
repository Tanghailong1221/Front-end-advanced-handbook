# CSS基础



* [CSS选择器的优先级是怎样的？✨](#css选择器的优先级是怎样的？✨)
* [link和@import的区别？](#link和@import的区别？)
* [有哪些方式（CSS）可以隐藏页面元素？](#有哪些方式（CSS）可以隐藏页面元素？)
* [em\px\rem区别？](#em\px\rem区别？)
* [块级元素水平居中的方法？](#块级元素水平居中的方法？)
* [CSS有几种定位方式？](#css有几种定位方式？)
* [如何理解z-index？✨](#如何理解z-index？✨)
* [如何理解层叠上下文？✨](#如何理解层叠上下文？✨)
* [清除浮动有哪些方法？](#清除浮动有哪些方法？)
* [你对css-sprites的理解](#你对css-sprites的理解，好处是什么？)
* [你对媒体查询的理解？](#你对媒体查询的理解？)
* [你对盒模型的理解？✨](#你对盒模型的理解✨)
* [标准盒模型和怪异盒模型有什么区别？✨](#标准盒模型和怪异盒模型有什么区别？✨)
* [谈谈对BFC(Block Formatting Context)的理解？ ✨](#谈谈对bfc的理解✨)
* [为什么有时候人们用translate来改变位置而不是定位？](#为什么有时候人们用translate来改变位置而不是定位？)
* [伪类和伪元素的区别是什么？](#伪类和伪元素的区别是什么？)
* [你对flex的理解？✨](#你对flex的理解？✨)
* [关于CSS的动画与过渡问题](#关于css的动画与过渡问题)

本章是CSS考点的非重难点，因此我们采用简略回答的方式进行撰写，所以不会有太多详细的解释。

> 我们约定，每个问题后我们标记『✨』的为高频面试题

## CSS选择器的优先级是怎样的✨

### CSS选择器的优先级是：

**内联 > ID选择器 > 类选择器 > 标签选择器**

CSS选择器的优先级（或称权重）决定了当多个规则应用到同一个元素时，哪个规则会最终生效。优先级是由选择器的不同类型决定的，并且可以通过以下规则来计算：

1. **内联样式**：直接在HTML元素中使用`style`属性定义样式。每个内联样式都有1000的优先级点数。
   - 例如: `<p style="color: red;">Hello</p>`
2. **ID选择器**：以`#`开头的选择器。每个ID选择器有100的优先级点数。
   - 例如: `#myId { color: blue; }`
3. **类选择器**、**属性选择器**和**伪类选择器**：这些选择器各有10的优先级点数。
   - 例如: `.myClass`, `[type="text"]`, `:hover`
4. **类型选择器**和**伪元素选择器**：这些选择器各有1的优先级点数。
   - 例如: `div`, `::before`, `::after`
5. **通配符选择器**、**子代选择器**、**相邻兄弟选择器**等：这些选择器不增加优先级点数，即优先级点数为0。
   - 例如: `*{marigin:6px;}`, `>`, `+`
6. **继承**：继承的样式没有优先级。
7. **!important**：可以在声明后面加上`!important`来提高优先级，使其高于其他所有规则（除了其他的`!important`声明），但仍然低于内联样式。
   - 例如: `#myId { color: blue !important; }`

### 计算示例：

- `#id .class p` 的优先级是 `100 + 10 + 1 = 111`
- `.class p` 的优先级是 `10 + 1 = 11`
- `p` 的优先级是 `1`

如果两个选择器具有相同的优先级点数，则按照它们在CSS文件中的顺序来确定哪一个规则生效：后来者居上。

此外，浏览器通常会将作者样式表的优先级设置得比用户代理样式表高，而用户代理样式表又比用户样式表低。

## link和@import的区别

`<link>` 和 `@import` 都是用来在HTML文档中引入外部CSS文件的方法，但它们之间存在一些重要的区别。下面将从以下七个方面进行区分：

1. **位置**:
   - `<link>` 标签通常放在HTML文档的`<head>`部分。可以在文档的任何位置使用，但通常推荐放在`<head>`标签内，以确保样式在页面加载时已经可用。
   - `@import` 规则必须放在CSS文件的顶部，但在`<style>`标签内部也可以使用。在HTML文档中，`@import` 规则只能通过嵌入式`<style>`标签使用，并且同样需要位于顶部。
2. 类型
   * `<link>` 属于XHTML标签。
   * `@import` 是CSS提供的，表示导入外部样式表。
3. **语法**:
   - `<link rel="stylesheet" href="styles.css">`
   - `@import url('styles.css');`
4. **并行加载**:
   - `<link>` 标签支持并行加载，这意味着浏览器可以同时加载多个资源，提高了性能。
   - `@import` 不支持并行加载，这意味着它会阻塞后续资源的加载直到当前资源加载完成。
5. **媒体查询**:
   - `<link>` 可以使用`media`属性来指定CSS文件应该在哪些设备或屏幕尺寸下加载。
   - `@import`可以使用媒体查询来控制何时导入文件，但需要将媒体查询放在`@import`规则之后。
6. **优先级**:
   - `<link>` 标签引入的样式具有较高的优先级，尤其是在与`@import`冲突的情况下。
   - `@import` 引入的样式优先级较低。
7. **兼容性**:
   - `<link>` 标签被所有现代浏览器广泛支持，并且被认为是更标准的做法。
   - `@import` 在大多数现代浏览器中也得到支持，但只在IE 5以上才能识别。
8. **错误处理**:
   - 如果CSS文件无法加载，页面仍会正常显示，只是缺少了该样式文件中的样式。
   - 如果`@import` 规则引用的CSS文件无法加载，那么整个包含`@import`的样式表将不会被应用。

### 总结

- `<link>` 更适合用于HTML文档中引入外部样式表，因为它提供了更好的性能和兼容性。
- `@import` 更适合用于一个样式表中引入另一个样式表，尤其是当你希望将样式分割成多个文件时。

* 当使用javascript控制dom去改变样式的时候，只能使用link标签，因为@import不是dom可以控制的。

## 有哪些方式（CSS）可以隐藏页面元素

在CSS中，有多种方法可以用来隐藏页面上的元素。以下是几种常用的方法：

1. **`display: none;`**

   - 这种方法完全从页面布局中移除元素，就好像它不存在一样。

   - 示例:

     ```css
     .hidden {
         display: none;
     }
     ```

2. **`visibility: hidden;`**

   - 元素仍然占据空间，但其内容不可见。

   - 示例:

     ```css
     .hidden {
         visibility: hidden;
     }
     ```

3. **`opacity: 0;`**

   - 元素透明度为0，但仍占据空间。

   - 示例:

     ```css
     .hidden {
         opacity: 0;
     }
     ```

4. **`position: absolute;` 与 `left: -9999px;` 或 `transform: translateX(-9999px);`**

   - 将元素移动到视口之外，使其不可见。

   - 示例:

     ```css
     .hidden {
         position: absolute;
         left: -9999px;
     }
     ```

   - 或者:

     ```css
     .hidden {
         transform: translateX(-9999px);
     }
     ```

5. **`height: 0; width: 0; overflow: hidden;`**

   - 将元素的高度和宽度设为0，并隐藏溢出的内容。

   - 示例:

     ```css
     .hidden {
         height: 0;
         width: 0;
         overflow: hidden;
     }
     ```

6. **`clip: rect(0, 0, 0, 0);`**

   - 使用`clip`属性裁剪元素，使其不可见。

   - 示例:

     ```css
     .hidden {
         clip: rect(0, 0, 0, 0);
     }
     ```

7. **`transform: scale(0);`**

   - 通过缩放元素到0大小来隐藏它。

   - 示例:

     ```css
     .hidden {
         transform: scale(0);
     }
     ```

8. **`filter: blur(10px);`**

   - 使用模糊滤镜使元素变得难以辨认。

   - 示例:

     ```css
     .hidden {
         filter: blur(10px);
     }
     ```

9. **`pointer-events: none;`**

   - 这个属性可以阻止用户与元素交互，但元素本身仍然可见。

   - 示例:

     ```css
     .hidden {
         pointer-events: none;
     }
     ```

10. **`content: '';`** (对于伪元素)

    - 对于`::before`和`::after`伪元素，可以将其内容设为空字符串。

    - 示例:

      ```css
      .hidden::before {
          content: '';
      }
      ```

每种方法都有其适用场景和限制。例如，如果你想让一个元素完全消失并且不占据任何空间，`display: none;` 是最好的选择。如果你想保持元素的位置但使其不可见，可以考虑使用`visibility: hidden;`。

## display:none和visibility:hidden的区别

`display: none;` 和 `visibility: hidden;` 都可以用来隐藏页面上的元素，但它们之间有一些关键的区别：

### `display: none;`

- **效果**:

  - 当使用 `display: none;` 时，元素不会在页面布局中占据任何空间。
  - 该元素及其子元素都不会渲染，就好像它们不存在于文档流中一样。

- **示例**:

  ```
  .hidden {
      display: none;
  }
  ```

- **用途**:

  - 常用于完全隐藏一个元素或一组元素，而不影响页面布局。
  - 适用于动态隐藏/显示元素的情况，例如响应用户交互时。

- **对子元素的影响**:

  - 子元素也不会被渲染。

### `visibility: hidden;`

- **效果**:

  - 当使用 `visibility: hidden;` 时，元素仍然占据其在页面布局中的空间，但内容不可见。
  - 该元素的子元素仍然会被渲染，并且保留它们的空间。

- **示例**:

  ```
  .hidden {
      visibility: hidden;
  }
  ```

- **用途**:

  - 常用于临时隐藏元素，但希望保留其空间的情况。
  - 适用于需要保留元素占位符的场景，例如动画或过渡效果。

- **对子元素的影响**:

  - 子元素仍然会被渲染，并占据它们应有的空间。

### 总结

- **布局影响**:
  - `display: none;` 完全移除了元素及其子元素，不占据任何空间。
  - `visibility: hidden;` 保留了元素及其子元素的空间，但内容不可见。
- **可访问性**:
  - 使用 `display: none;` 的元素对辅助技术（如屏幕阅读器）不可见。
  - 使用 `visibility: hidden;` 的元素对辅助技术仍然是可见的，这可能有助于保持可访问性。
- **重绘和重排**:
  - `display: none;` 会导致页面重新布局。
  - `visibility: hidden;` 只会导致重绘，但不会导致重排。
- **动画和过渡**:
  - `visibility: hidden;` 更适合用于需要动画或过渡效果的场景。
  - `display: none;` 不适合用于动画，因为元素从文档流中完全移除后无法进行平滑过渡。

## em\px\rem区别

`em`, `px`, 和 `rem` 是CSS中常用的长度单位，它们分别代表不同的含义和应用场景。下面是这些单位之间的主要区别：

### em (em)

- **定义**:

  - `em` 是一个相对单位，表示相对于当前元素的字体大小。
  - 如果应用于字体大小，`em` 的值等于当前元素的字体大小。
  - 如果应用于其他属性（如宽度、高度等），`em` 的值等于当前元素父元素的字体大小。

- **示例**:

  ```css
  /* 设置字体大小为父元素字体大小的两倍 */
  p {
      font-size: 2em;
  }
  /* 设置宽度为父元素字体大小的两倍 */
  div {
      width: 2em;
  }
  ```

- **特点**:

  - `em` 单位使得元素的尺寸随上下文变化，因此非常适合响应式设计。
  - `em` 单位可能会导致复杂的计算，特别是当嵌套多个元素时。

### px (pixel)

- **定义**:

  - `px` 表示像素，是一个绝对单位。
  - `px` 单位的值在不同设备上可能有所不同，但通常表示设备上物理像素的数量。

- **示例**:

  ```css
  /* 设置字体大小为16像素 */
  body {
  	font-size: 16px;
  }
  /* 设置宽度为200像素 */
  div {
      width: 200px;
  }
  ```

- **特点**:

  - `px` 单位提供精确控制，适用于不需要响应式调整的固定尺寸设计。
  - `px` 单位在不同设备和分辨率上可能会导致不同的视觉效果。

### rem (root em)

- **定义**:

  - `rem` 是CSS3新加属性
  - `rem` 是一个相对单位，表示相对于根元素（通常是 `<html>`）的字体大小，浏览器默认字体是16px。
  - `rem` 的值始终等于根元素的字体大小。

- **示例**:

  ```css
  /* 设置根元素字体大小为16像素 */
  html {
      font-size: 16px;
  }
  /* 设置字体大小为根元素字体大小的两倍 */
  p {
      font-size: 2rem;
  }
  /* 设置宽度为根元素字体大小的两倍 */
  div {
      width: 2rem;
  }
  ```

- **特点**:

  - `rem` 单位使得元素的尺寸在整个文档中保持一致，因为它们都相对于同一个基准（根元素）。
  - `rem` 单位非常适合全局性的响应式设计，因为它避免了嵌套元素的复杂计算问题。

### 总结

- **`em`**: 相对于当前元素或父元素的字体大小。
- **`px`**: 绝对单位，表示像素数量。
- **`rem`**: 相对于根元素（通常是 `<html>`）的字体大小。

在实际应用中，选择哪种单位取决于你的设计需求和希望达到的效果。如果你需要元素尺寸随着字体大小的变化而变化，那么 `em` 或 `rem` 是更好的选择。如果你需要精确控制尺寸，那么 `px` 可能更适合。

## 常见的替换元素和非替换元素

在CSS中，元素可以分为替换元素（replaced elements）和非替换元素（non-replaced elements）。这两类元素的行为和样式有所不同，了解它们的区别可以帮助更好地控制页面布局和样式。

### 替换元素 (Replaced Elements)

替换元素是指那些由外部资源替换其内容的元素，这些元素的内容不由文档树中的子元素决定，而是由外部资源（如图片、视频、音频文件等）提供。

### 常见的替换元素包括：

- `<img>`: 图像元素
- `<iframe>`: 内联框架
- `<object>`: 通用的内嵌对象容器
- `<embed>`: 内嵌对象
- `<canvas>`: 用于绘制图形的 HTML5 元素
- `<video>`: 视频播放器
- `<audio>`: 音频播放器

### 非替换元素 (Non-Replaced Elements)

非替换元素是指那些其内容由文档树中的子元素提供的元素。这些元素的内容通常由文本或其他非替换元素组成。

### 常见的非替换元素包括：

- `<p>`: 段落
- `<div>`: 通用容器
- `<span>`: 内联容器
- `<ul>` 和 `<ol>`: 无序和有序列表
- `<li>`: 列表项
- `<a>`: 锚点链接
- `<button>`: 按钮
- `<input>`: 输入字段
- `<textarea>`: 多行文本输入
- `<label>`: 标签
- `<table>`: 表格
- `<tr>`: 表格行
- `<td>` 和 `<th>`: 表格单元格
- `<form>`: 表单

### 替换元素的特点

- 替换元素通常有自己的固有尺寸，例如图片的宽度和高度。
- 替换元素的尺寸可以被显式地设置，但通常情况下，它们会保持其原始比例。
- 替换元素的尺寸可以使用`width`和`height`属性来控制。

### 非替换元素的特点

- 非替换元素的尺寸通常由内容和周围元素的样式决定。
- 非替换元素可以根据内容自动调整尺寸，除非显式设置了宽度和高度。
- 非替换元素的尺寸可以通过`min-width`、`max-width`、`min-height`和`max-height`等属性来控制。

### 实际应用

- 替换元素通常用于展示多媒体内容，如图像和视频。
- 非替换元素用于构建页面结构和布局，如段落、列表和表单。

## 行内元素有哪些？块级元素有哪些？空元素有哪些？

CSS规范规定，每个元素都有display属性，确定该元素的类型，每个元素都有默认的display值。

如div的display默认值为“block”，则为“块级”元素；span默认display属性值为“inline”，是“行内”元素，也可以使用这个属性修改元素的类型。

### （1）行内元素`inline`：

行内元素不会在其前后产生换行效果，不能设置宽高，并且它们只占据必要的宽度，不会独占一行。行内元素可以与其他行内元素并排显示在同一行上。

一些常见的行内元素包括：

* `<a>`: 锚点链接
* `<span>`: 用于样式化或添加类的通用内联容器
* `<img>`: 图像
* `<input>`: 表单输入字段
* `<button>`: 按钮
* `<label>`: 表单标签
* `<select>`: 下拉列表
* `<textarea>`: 多行文本输入
* `<strong>`: 强调重要性
* `<em>`: 强调语气

### （2）块级元素` block`：

块级元素默认会自动换行，在新的行上开始，并且占据整个可用宽度。块级元素可以包含其他块级元素或行内元素。

一些常见的块级元素包括：

* `<div>`: 通用容器
* `<p>`: 段落
* `<h1>` 至 `<h6>`: 标题
* `<aside>`: 侧边栏
* `<footer>`: 页面底部
* `<header>`: 页面头部
* `<main>`: 主要内容
* `<ul>`: 无序列表
* `<li>`: 列表项
* `<dl>`: 定义列表
* `<dt>`: 定义术语
* `<dd>`: 定义描述

### （3）常见的空元素：

空元素是指那些没有闭合标签的元素。它们不能包含任何内容，只能包含属性。

一些常见的空元素包括：

- `<br>`: 换行
- `<hr>`: 水平分割线
- `<img>`: 图像
- `<input>`: 输入字段
- `<link>`: 链接到样式表
- `<meta>`: 元数据

### （4）行内块元素` inline-block`：

行内块元素同时具有块元素和行内元素的特点

① 和相邻行内元素（行内块）在一行上，但是他们之间会有空白缝隙。一行可以显示多个（行内元素特点）。
② 默认宽度就是它本身内容的宽度（行内元素特点）。
③ 高度，行高、外边距以及内边距都可以控制（块级元素特点）

常见的行内块元素包括：

* `<img>`: 图像

* `<input>`: 表单输入字段

## 块级元素水平居中的方法

> 如果使用Hack的话，水平居中的方法非常多，我们只介绍主流的，奇葩的见拓展阅读

`margin:0 auto`方法

```css
  .center{
      height: 200px;
      width:200px;
      margin:0 auto;
      border:1px solid red;
  }
  <div class="center">水平居中</div>
```

flex布局，目前主流方法

```css
  .center{
      display:flex;
      justify-content:center;
  }
  <div class="center">
      <div class="flex-div">1</div>
      <div class="flex-div">2</div>
  </div>
```

table方法

```css
  .center{
      display:table;
      margin:0 auto;
      border:1px solid red;
  }
  <div class="center">水平居中</div>
```

还有一些通过position+(margin|transform)等方法的不一样列举了，非重点没必要。

> 拓展阅读: [16种方法实现水平居中垂直居中](https://louiszhai.github.io/2016/03/12/css-center/)

## CSS有几种定位方式

* static: 默认值。正常文档流定位，此时 top, right, bottom, left 和 z-index 属性无效，块级元素从上往下纵向排布，行级元素从左向右排列。

* relative：相对定位，此时的『相对』是相对于正常文档流的位置。

* absolute：相对于最近的非 static 定位祖先元素的偏移，来确定元素位置，比如一个绝对定位元素它的父级、和祖父级元素都为relative，它会相对他的父级而产生偏移。

* fixed：（老IE不支持）生成绝对定位的元素，指定元素相对于屏幕视口（viewport）的位置来指定元素位置。元素的位置在屏幕滚动时不会改变，比如那种回到顶部的按钮一般都是用此定位方式。

* sticky：粘性定位，特性近似于relative和fixed的合体，其在实际应用中的近似效果就是IOS通讯录滚动的时候的『顶屁股』。

> 文字描述很难理解，可以直接看代码
<p class="codepen" data-height="300" data-theme-id="33015" data-default-tab="css,result" data-user="xiaomuzhu" data-slug-hash="bPVNxj" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="bPVNxj">
  <span>See the Pen <a href="https://codepen.io/xiaomuzhu/pen/bPVNxj/">
  bPVNxj</a> by Iwobi (<a href="https://codepen.io/xiaomuzhu">@xiaomuzhu</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

##  position:absolute和float属性的异同

### `position: absolute;`

- **定义**:
  - `position: absolute;` 使得元素脱离正常的文档流，并相对于最近的非静态定位祖先元素（即设置了 `position: relative;`, `position: absolute;`, 或 `position: fixed;` 的祖先元素）进行定位。
  - 如果没有这样的祖先元素，则相对于初始包含块（通常是 `<html>` 元素）进行定位。
- **特点**:
  - 元素可以使用 `top`, `right`, `bottom`, 和 `left` 属性来精确地定位。
  - 绝对定位的元素不再占据原来的空间，即它们不会影响其他元素的位置。
  - 绝对定位的元素可以在页面上自由移动，即使页面滚动也不受影响。
  - 绝对定位的元素可以与其他定位元素重叠。

### `float`

- **定义**:
  - `float` 属性可以将元素移到其容器的一侧，通常用于创建多列布局或让文本环绕图片。
  - `float` 的值可以是 `left` 或 `right`。
- **特点**:
  - 浮动元素仍然占据其原来的空间，但它会被移动到容器的一侧，而其他内容会围绕它流动。
  - 浮动元素可能会导致其父元素的高度塌陷，即父元素的高度不足以包裹浮动的子元素。
  - 浮动元素可以通过使用 `clear` 属性来控制其他元素与它的相互作用。
  - 浮动元素仍然参与文档流，会影响其他元素的位置。

### 异同点

- 共同点：对内联元素设置`float`和`absolute`属性，可以让元素脱离文档流，并且可以设置其宽高。
- 不同点：`float`仍会占据位置，`absolute`会覆盖文档流中的其他元素。

## 如何理解z-index✨

`z-index` 属性是CSS中的一个重要概念，用于控制元素在堆叠顺序中的位置。当页面上有多个重叠的元素时，`z-index` 可以确定哪个元素位于最前面，哪个元素位于后面。理解 `z-index` 的工作原理对于创建复杂的页面布局至关重要。CSS 中的z-index属性控制重叠元素的垂直叠加顺序，默认元素的z-index为0，我们可以修改z-index来控制元素的图层位置，而且z-index只能影响设置了position值的元素。

### `z-index` 的基本概念

- **定义**:
  - `z-index` 属性定义了一个元素在堆叠顺序中的位置。它决定了元素在Z轴（垂直于屏幕的方向）上的层次。
- **取值**:
  - `z-index` 可以接受整数值，正值会使元素向前移动，负值会使元素向后移动。
  - 如果不设置 `z-index`，或者设置为 `auto`，元素将按照它们在HTML文档中的出现顺序堆叠。
- **适用范围**:
  - `z-index` 只对具有定位属性（`position`）的元素有效。这些定位属性包括 `relative`, `absolute`, `fixed`, 或 `sticky`。
  - 如果元素的 `position` 属性设置为 `static`（这是默认值），则 `z-index` 不会产生效果。

我们可以把视图上的元素认为是一摞书的层叠，而人眼是俯视的视角，设置z-index的位置，就如同设置某一本书在这摞书中的位置。

* 顶部: 最接近观察者
* ...
 * 3 层
 * 2 层
 * 1 层
 * 0 层 默认层
 * -1 层
 * -2 层
 * -3 层
* ...
* 底层: 距离观察者最远

![2019-06-14-02-19-16]( https://xiaomuzhu-image.oss-cn-beijing.aliyuncs.com/282998fe2501b87e23af0fba61d9077e.png)

> 可以结合这个例子理解z-index

<p class="codepen" data-height="300" data-theme-id="33015" data-default-tab="css,result" data-user="xiaomuzhu" data-slug-hash="xowqjG" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="xowqjG">
  <span>See the Pen <a href="https://codepen.io/xiaomuzhu/pen/xowqjG/">
  xowqjG</a> by Iwobi (<a href="https://codepen.io/xiaomuzhu">@xiaomuzhu</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## 如何理解堆叠上下文✨

在CSS中，“堆叠上下文”（Stacking Context）是一个重要的概念，它定义了页面上元素的堆叠顺序，即哪些元素在哪些元素之上。堆叠上下文决定了元素如何在Z轴（垂直于屏幕的方向）上排列。理解堆叠上下文对于控制页面布局和元素的可见性至关重要。

### 堆叠上下文的定义

堆叠上下文是一个逻辑概念，它由具有特定属性的元素创建。当一个元素创建了一个新的堆叠上下文时，该元素及其所有子元素形成一个堆叠组，它们之间的堆叠顺序是独立于页面上其他元素的。

### 创建堆叠上下文的条件

以下情况会创建新的堆叠上下文：

1. **根元素** (`<html>`): 根元素总是创建一个堆叠上下文。
2. **绝对定位的元素** (`position: absolute;` 或 `position: fixed;`)，如果它们的 `z-index` 不是 `auto`（即设置了非零的 `z-index` 值）。
3. **相对定位的元素** (`position: relative;`)，如果它们的 `z-index` 不是 `auto`（即设置了非零的 `z-index` 值）。
4. **元素设置了 `opacity` 且值小于 1**。
5. **元素设置了 `mix-blend-mode`**。
6. **元素设置了 `isolation: isolate;`**。
7. **元素设置了 `transform` 属性**。
8. **元素设置了 `filter` 属性**。
9. **元素设置了 `mask` 属性**。
10. **元素设置了 `clip-path` 属性**。
11. **元素设置了 `perspective` 属性**。
12. **元素设置了 `contain: layout;` 或 `contain: paint;`**。
13. **`display: flex;` 或 `display: grid;` 的容器**，如果它们的 `z-index` 不是 `auto`（即设置了非零的 `z-index` 值）。
14. **内联元素** 和 **表格单元格** 也会创建堆叠上下文。

### 堆叠上下文的作用

1. **控制子元素的堆叠顺序**:
   - 当一个元素创建了新的堆叠上下文时，它将控制其所有子元素的堆叠顺序。
   - 子元素的堆叠顺序可以通过各自的 `z-index` 属性来控制。
2. **隔离子元素**:
   - 创建堆叠上下文的元素将隔离其子元素，使得子元素不会影响外部元素的堆叠顺序。
3. **解决 `z-index` 冲突**:
   - 当两个元素具有相同的 `z-index` 时，它们将按照HTML文档中的顺序堆叠。
   - 如果两个元素处于不同的堆叠上下文中，父堆叠上下文中的元素将位于子堆叠上下文中的元素之上。

> 拓展阅读：[层叠上下文-张鑫旭](https://www.zhangxinxu.com/wordpress/2016/01/understand-css-stacking-context-order-z-index/)

## 清除浮动有哪些方法

### 1. 使用 `clear` 属性

`clear` 属性可以用来清除元素周围的浮动元素。它可以接受以下值：

- **`clear: left;`** - 清除左侧的浮动元素。
- **`clear: right;`** - 清除右侧的浮动元素。
- **`clear: both;`** - 同时清除左侧和右侧的浮动元素。
- **`clear: none;`** - 不清除任何浮动元素。

**示例**

```css
/* 清除两侧的浮动元素 */
.clear-both {
    clear: both;
}
```

```html
<div style="float: left;">Floating Element</div>
<div class="clear-both">This element will clear the floating element above it.</div>
```

### 2. 使用伪元素 `:before` 或 `:after`

可以使用伪元素 `:before` 或 `:after` 来插入一个不可见的元素，并设置 `clear: both;` 来清除浮动。

**示例**

```css
.container:after {
    content: "";
    display: block;
    clear: both;
}
/* 或者使用 :before */
.container:before {
    content: "";
    display: table;
}
.container:after {
    content: "";
    display: table;
    clear: both;
}
```

```html
<div class="container">
    <div style="float: left;">Floating Element</div>
    <p>This text will be cleared of the floating element above it.</p>
</div>
```

### 3. 使用 `overflow` 属性

设置一个元素的 `overflow` 属性为 `auto` 或 `hidden` 可以自动清除该元素内的所有浮动。

**示例**

```css
.container {
    overflow: auto;
}
```

```html
<div class="container">
    <div style="float: left;">Floating Element</div>
    <p>This text will be cleared of the floating element above it.</p>
</div>
```

### 4. 使用 Flexbox

在Flexbox布局中，浮动是不需要的，因为Flexbox本身就处理了元素的布局和对齐。

**示例**

```css
.container {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
}

/* 或者使用 flex-wrap */
.container {
    display: flex;
    flex-wrap: wrap;
}
```

```html
<div class="container">
    <div>Floating Element 1</div>
    <div>Floating Element 2</div>
    <p>This text is part of the flex container and does not need to be cleared.</p>
</div>
```

### 5. 使用 Grid

在Grid布局中，浮动同样不是必需的，因为Grid布局本身就是为复杂的布局设计的。

**示例**

```css
.container {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 10px;
}
```

```html
<div class="container">
    <div>Floating Element 1</div>
    <div>Floating Element 2</div>
    <p>This text is part of the grid container and does not need to be cleared.</p>
</div>
```

### 6. 使用 `display: flow-root;`

`display: flow-root;` 是CSS3中引入的一个新属性值，用于清除浮动，它会创建一个新的块级格式化上下文。

**示例**

```css
.container {
    display: flow-root;
}
```

```html
<div class="container">
    <div style="float: left;">Floating Element</div>
    <p>This text will be cleared of the floating element above it.</p>
</div>
```

### 选择最佳方法

- **简单布局**:
  - 使用 `clear` 属性或伪元素方法比较合适。
- **复杂布局**:
  - 使用 Flexbox 或 Grid 可以更轻松地管理布局。
- **兼容性**:
  - 使用 `overflow` 属性或伪元素方法可以在大多数浏览器中工作良好。
- **现代布局**:
  - 使用 `display: flow-root;` 可以提供更好的控制和兼容性。

> 在flex已经成为布局主流之后，浮动这种东西越来越少见了，毕竟它的副作用太大

## 对css sprites的理解，好处是什么

CSS Sprites（CSS精灵图）是一种优化Web页面性能的技术，它将多个小图像合并到一个大的图像文件中，并通过CSS来显示所需的特定部分。这种技术可以减少HTTP请求次数，从而提高网页加载速度。

### CSS Sprites 的工作原理

1. 合并图像:
   - 将多个小图像合并到一个大图像文件中。
2. 使用CSS定位:
   - 通过CSS的 `background-image` 和 `background-position` 属性来显示图像文件中的特定部分。
   - 使用 `background-position` 来指定显示图像的坐标位置。

**示例**

假设我们有一个包含三个小图像的精灵图文件 `sprites.png`，我们可以这样使用它：

```css
/* 设置背景图像 */
.image1 {
    background-image: url('sprites.png');
    width: 32px;
    height: 32px;
    /* 设置背景位置，显示第一个图像 */
    background-position: 0 0;
}

.image2 {
    background-image: url('sprites.png');
    width: 32px;
    height: 32px;
    /* 设置背景位置，显示第二个图像 */
    background-position: -32px 0;
}

.image3 {
    background-image: url('sprites.png');
    width: 32px;
    height: 32px;
    /* 设置背景位置，显示第三个图像 */
    background-position: -64px 0;
}
```

```html
<div class="image1"></div>
<div class="image2"></div>
<div class="image3"></div>
```

### CSS Sprites 的好处

1. **减少HTTP请求**:
   - 最显著的好处是减少了HTTP请求次数，从而加快了页面加载速度。
   - 每次HTTP请求都会消耗时间和带宽，所以减少请求次数可以极大地提高性能。
2. **缓存效率**:
   - 由于所有图像都在一个文件中，浏览器只需要下载一次这个文件，然后就可以多次使用，提高了缓存效率。
3. **易于管理和维护**:
   - 所有图像都集中在一个文件中，便于管理和更新。
4. **节省服务器资源**:
   - 减少HTTP请求可以减轻服务器的压力，特别是在高流量网站上。
5. **提高用户体验**:
   - 页面加载更快，用户等待的时间更短，提高了整体用户体验。

### CSS Sprites 的不足：

* CSS Sprite维护成本较高，如果页面背景有少许改动，一般就要改这张合并的图片
* 加载速度优势在http2开启后荡然无存，HTTP2多路复用，多张图片也可以重复利用一个连接通道搞定

### 注意事项

1. **尺寸和位置计算**:
   - 必须精确计算每个图像在精灵图中的位置，以确保正确显示。
2. **浏览器兼容性**:
   - 虽然现代浏览器普遍支持CSS Sprites，但在一些较旧的浏览器中可能需要额外的兼容性考虑。
3. **动态内容**:
   - 如果图像需要动态更改，使用CSS Sprites可能会变得复杂，因为需要更新精灵图文件和相关的CSS。
4. **可访问性和SEO**:
   - CSS Sprites不适用于需要替代文本的图像，因为它们是作为背景图像使用的。

## 对媒体查询的理解

媒体查询（Media Queries）是CSS3中引入的一个重要功能，它允许开发者根据不同的设备特性（如屏幕尺寸、分辨率、方向等）来应用不同的样式规则。媒体查询使得CSS布局能够适应各种屏幕尺寸和设备类型，是响应式设计的核心组成部分。

### 媒体查询的基本语法

媒体查询的基本语法包括一个媒体类型（可选）和一个或多个表达式。表达式用于检测设备的特性，并基于这些特性来应用相应的样式。

**语法结构**

```css
@media [not] [media-type] and (expression) {
    /* CSS rules */
}
```

- **`[not]`** (可选): 表示是否否定后面的媒体类型。
- **`[media-type]`** (可选): 指定媒体类型，如 `screen`、`print` 等。
- **`(expression)`**: 表达式，用于检测设备特性。

### 常见的媒体特性

以下是一些常见的媒体特性及其含义：

- **`width`**: 屏幕宽度或视口宽度。
- **`height`**: 屏幕高度或视口高度。
- **`orientation`**: 设备的方向，可以是 `portrait`（纵向）或 `landscape`（横向）。
- **`aspect-ratio`**: 屏幕的宽高比。
- **`resolution`**: 屏幕的分辨率，可以是 `dpi`、`dpcm` 或 `dppx`。
- **`color`**: 屏幕的最大颜色数量。
- **`color-index`**: 屏幕的最大颜色索引数量。
- **`monochrome`**: 屏幕的最大灰度级别。
- **`scan`**: 屏幕的扫描模式，可以是 `progressive` 或 `interlace`。
- **`grid`**: 屏幕的网格类型，可以是 `normal` 或 `compact`。

**示例**

假设我们要为不同的屏幕尺寸定义不同的样式，可以使用如下媒体查询：

```css
/* 默认样式 */
body {
    background-color: #f4f4f4;
    font-size: 16px;
}

/* 当屏幕宽度小于600px时 */
@media screen and (max-width: 600px) {
    body {
        background-color: #ddd;
        font-size: 14px;
    }
}

/* 当屏幕宽度大于等于600px且小于900px时 */
@media screen and (min-width: 600px) and (max-width: 900px) {
    body {
        background-color: #bbb;
        font-size: 15px;
    }
}

/* 当屏幕宽度大于等于900px时 */
@media screen and (min-width: 900px) {
    body {
        background-color: #aaa;
        font-size: 16px;
    }
}
```

### 使用场景

- **响应式设计**:
  - 媒体查询是实现响应式设计的关键，可以根据不同的屏幕尺寸和设备特性来调整布局和样式。
- **适应不同设备**:
  - 可以针对不同的设备类型（如手机、平板电脑、桌面显示器）应用不同的样式。
- **打印样式**:
  - 可以使用 `@media print` 来定义打印时的样式规则。

### 总结

- **媒体查询** 允许开发者根据不同的设备特性来应用不同的样式规则。
- **语法** 包括一个可选的媒体类型和一个或多个表达式。
- **常见的媒体特性** 包括宽度、高度、方向等。
- **响应式设计** 是媒体查询的主要应用场景之一。

> 拓展阅读：[深入理解CSS Media媒体查询](https://www.cnblogs.com/xiaohuochai/p/5848612.html)

## 介绍一下box-sizing属性

`box-sizing` 属性是CSS中用于控制元素框模型的一种方式。它定义了元素的宽度和高度是否包括内边距（padding）和边框（border），这对于布局和尺寸控制非常重要。`box-sizing` 属性有以下几个值：

1. **`content-box`** (默认值):
   - 这是传统的CSS盒模型。
   - 元素的总宽度和总高度仅由 `width` 和 `height` 属性定义。
   - 内边距（padding）和边框（border）会额外增加元素的总宽度和总高度。
2. **`border-box`**:
   - 这是另一种盒模型，常用于现代布局。
   - 元素的总宽度和总高度由 `width` 和 `height` 属性定义，包括内边距和边框。
   - 这意味着如果给元素设置了内边距或边框，这些值不会增加元素的实际宽度和高度。
3. **`inherit`**:
   - 使元素继承其父元素的 `box-sizing` 值。

### 举个栗子

假设我们有一个元素，我们想要设置宽度为 `300px`，内边距为 `10px`，边框为 `5px` 宽。

#### 使用 `content-box`:

```css
.box-content {
    width: 300px;
    padding: 10px;
    border: 5px solid black;
    box-sizing: content-box;
}
```

在这种情况下，元素的实际宽度将是 `300px + 2 * 10px + 2 * 5px = 330px`（左右各加上内边距和边框的宽度）。

#### 使用 `border-box`:

```css
.box-border {
    width: 300px;
    padding: 10px;
    border: 5px solid black;
    box-sizing: border-box;
}
```

在这种情况下，元素的实际宽度将是 `300px`，即使设置了内边距和边框。内边距和边框将从 `300px` 的宽度中扣除。

### 为什么使用 `border-box`?

- **简化布局**:
  - 使用 `border-box` 可以简化布局，因为你可以直接设置元素的总宽度和总高度，而无需担心内边距和边框的额外宽度。
- **易于响应式设计**:
  - 在响应式设计中，使用 `border-box` 可以更容易地控制元素的尺寸，确保在不同屏幕尺寸下元素的尺寸保持一致。
- **避免意外的尺寸变化**:
  - 使用 `border-box` 可以防止因添加内边距和边框而导致的意外尺寸变化。

### 默认值和浏览器兼容性

- 在CSS3之前，默认的盒模型是 `content-box`。
- 在CSS3中引入了 `box-sizing` 属性，允许设置为 `border-box`。
- 为了向后兼容，大多数浏览器默认使用 `content-box`，但在某些情况下，可以通过设置 `box-sizing: border-box;` 来更改元素的盒模型。

### 使用示例

```css
/* 设置所有元素的盒模型为 border-box */
* {
    box-sizing: border-box;
}

/* 或者针对特定元素设置 */
.container {
    width: 300px;
    padding: 10px;
    border: 5px solid black;
    box-sizing: border-box;
}
```

### 总结

- `box-sizing` 属性允许你控制元素的盒模型。
- `content-box` 是传统的盒模型，其中宽度和高度不包括内边距和边框。
- `border-box` 是现代盒模型，其中宽度和高度包括内边距和边框。
- 使用 `border-box` 可以简化布局并避免尺寸变化的问题。

通过设置 `box-sizing` 属性，你可以更好地控制元素的尺寸和布局，特别是在响应式设计中。

**标准浏览器下，按照W3C规范对盒模型解析，一旦修改了元素的边框或内距，就会影响元素的盒子尺寸，就不得不重新计算元素的盒子尺寸，从而影响整个页面的布局。**

## 对盒模型的理解✨

盒模型（Box Model）是CSS中描述元素布局和尺寸的基础概念。盒模型定义了元素在页面上所占空间的各个组成部分，包括内容区域、内边距、边框和外边距。理解盒模型对于控制元素的尺寸和布局至关重要。

### 盒模型的组成部分

盒模型通常由以下四个部分组成：

1. **内容区域** (`content`):
   - 内容区域是元素内容所在的区域，其大小由 `width` 和 `height` 属性定义。
   - 这是元素中实际文本或图像所在的部分。
2. **内边距** (`padding`):
   - 内边距是内容区域和边框之间的空白区域。
   - 它可以使用 `padding` 属性来设置，可以是单个值或四个不同的值（上、右、下、左）。
3. **边框** (`border`):
   - 边框是围绕内容区域和内边距的线或区域。
   - 它可以使用 `border` 属性来设置，包括 `border-width`, `border-style`, 和 `border-color`。
4. **外边距** (`margin`):
   - 外边距是边框之外的空白区域。
   - 它可以使用 `margin` 属性来设置，同样可以是单个值或四个不同的值（上、右、下、左）。

![2019-06-14-04-15-49]( https://xiaomuzhu-image.oss-cn-beijing.aliyuncs.com/14650bf5fbb24066cea1dc1714d52a5b.png)

### 盒模型的两种类型

CSS提供了两种类型的盒模型：

1. **Content Box** (传统盒模型):
   - 在 Content Box 模型中，元素的总宽度和总高度仅由 `width` 和 `height` 属性定义。
   - 内边距和边框会额外增加元素的总宽度和总高度。
   - 这是传统的CSS盒模型。
2. **Border Box** (现代盒模型):
   - 在 Border Box 模型中，元素的总宽度和总高度由 `width` 和 `height` 属性定义，包括内边距和边框。
   - 这意味着如果给元素设置了内边距或边框，这些值不会增加元素的实际宽度和高度。
   - `box-sizing` 属性用于启用 Border Box 模型。

### 示例

假设我们有一个元素，我们想要设置宽度为 `300px`，内边距为 `10px`，边框为 `5px` 宽。

#### 使用 Content Box 模型:

```css
.box-content {
    width: 300px;
    padding: 10px;
    border: 5px solid black;
    box-sizing: content-box;
}
```

在这种情况下，元素的实际宽度将是 `300px + 2 * 10px + 2 * 5px = 330px`（左右各加上内边距和边框的宽度）。

#### 使用 Border Box 模型:

```css
.box-border {
    width: 300px;
    padding: 10px;
    border: 5px solid black;
    box-sizing: border-box;
}
```

在这种情况下，元素的实际宽度将是 `300px`，即使设置了内边距和边框。内边距和边框将从 `300px` 的宽度中扣除。

### 使用 `box-sizing`

`box-sizing` 属性可以用于控制元素采用哪种盒模型。

**示例**

```css
/* 设置所有元素的盒模型为 border-box */
* {
    box-sizing: border-box;
}

/* 或者针对特定元素设置 */
.container {
    width: 300px;
    padding: 10px;
    border: 5px solid black;
    box-sizing: border-box;
}
```

### 总结

- **盒模型** 描述了元素在页面上的尺寸和布局。
- **Content Box** 是传统的盒模型，其中宽度和高度不包括内边距和边框。
- **Border Box** 是现代盒模型，其中宽度和高度包括内边距和边框。
- `box-sizing` 属性可以用于控制元素采用哪种盒模型。
- 使用 Border Box 可以简化布局并避免尺寸变化的问题。

通过设置 `box-sizing` 属性，你可以更好地控制元素的尺寸和布局，特别是在响应式设计中。

## 标准盒模型和怪异盒模型有什么区别✨

在W3C标准下，我们定义元素的width值即为盒模型中的content的宽度值，height值即为盒模型中的content的高度值。

因此，标准盒模型下：
> 元素的宽度 = margin-left + border-left + padding-left + width + padding-right + border-right + margin-right

![2019-06-14-04-25-26]( https://xiaomuzhu-image.oss-cn-beijing.aliyuncs.com/232580766e15853d521a4c0bf6a5c794.png)

而IE怪异盒模型（IE8以下）width的宽度并不是content的宽度，而是border-left + padding-left + content的宽度值 + padding-right + border-right之和，height同理。

在怪异盒模型下：

> 元素占据的宽度 = margin-left + width + margin-right

![2019-06-14-04-25-04]( https://xiaomuzhu-image.oss-cn-beijing.aliyuncs.com/e427c6d19ea6be1359bd0177d7a5b7a3.png)

虽然现代浏览器默认使用W3C的标准盒模型，但是在不少情况下怪异盒模型更好用，于是W3C在css3中加入`box-sizing`。

```css
box-sizing: content-box // 标准盒模型
box-sizing: border-box // 怪异盒模型
box-sizing: padding-box // 火狐的私有模型，没人用
```

> 此演示来源于拓展阅读文章

<p class="codepen" data-height="300" data-theme-id="33015" data-default-tab="js,result" data-user="xiaomuzhu" data-slug-hash="LKpyzz" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="LKpyzz">
  <span>See the Pen <a href="https://codepen.io/xiaomuzhu/pen/LKpyzz/">
  LKpyzz</a> by Iwobi (<a href="https://codepen.io/xiaomuzhu">@xiaomuzhu</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

> 拓展阅读：[深入理解盒模型](https://www.cnblogs.com/xiaohuochai/p/5202597.html)

## 谈谈对BFC的理解✨

BFC（Block Formatting Context，块格式化上下文）是CSS中的一种概念，它定义了块级元素如何在页面上布局以及它们如何与其他元素交互。理解BFC对于控制页面布局和解决一些布局问题非常重要。

**书面解释**：BFC(Block Formatting Context，块格式化上下文)这几个英文拆解

* Box: CSS布局的基本单位，Box 是 CSS 布局的对象和基本单位， 直观点来说，就是一个页面是由很多个 Box 组成的，实际就是上个问题说的盒模型

* Formatting context：块级上下文格式化，它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系和相互作用

### BFC 的定义

BFC 是一个独立的渲染区域，其中的元素按照一定的规则进行布局。当一个元素创建了一个BFC时，它将控制其内部元素的布局，并且这些内部元素不会影响到外部元素的布局。

### 创建 BFC 的条件

以下情况会创建一个新的 BFC：

1. **根元素** (`<html>`): 根元素总是创建一个BFC。
2. **浮动元素** (`float` 不为 `none` 的元素)。
3. **绝对定位的元素** (`position: absolute;` 或 `position: fixed;`)。
4. **相对定位的元素** (`position: relative;`)，如果设置了 `z-index` 且值不是 `auto`。
5. **`overflow` 不为 `visible` 的元素** (`overflow: hidden;`, `overflow: scroll;`, `overflow: auto;`)。
6. **`display: flex;` 或 `display: grid;` 的容器**。
7. **`display: inline-block;` 或 `display: table-cell;` 的元素**。
8. **`display: run-in;` 的元素**。
9. **`display: contents;` 的元素**。
10. **`display: flow-root;` 的元素**。
11. **`contain: layout;` 或 `contain: paint;` 的元素**。
12. **`isolation: isolate;` 的元素**。

### BFC 的布局规则

1. **元素边缘不会与浮动元素重叠**:
   - BFC内部的元素不会与外部的浮动元素重叠。
2. **垂直边距折叠**:
   - BFC内部的相邻块级元素的垂直外边距会发生折叠。
3. **清除浮动**:
   - BFC内部的元素会自动清除浮动。
4. **包含浮动元素**:
   - BFC可以包含浮动元素，并且可以正确地计算高度以包裹这些元素。
5. **独立的布局**:
   - BFC内部的布局不受外部元素的影响，同样也不会影响外部元素的布局。
6. **独立的垂直定位**:
   - BFC内部元素的垂直定位不会受到外部元素的影响。
7. **独立的堆叠上下文**:
   - 创建BFC的元素会创建一个新的堆叠上下文，这意味着它会控制内部元素的堆叠顺序。

### 作用是什么？

#### 防止margin发生重叠

<p class="codepen" data-height="300" data-theme-id="33015" data-default-tab="html,result" data-user="xiaomuzhu" data-slug-hash="NZGjYQ" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="NZGjYQ">
  <span>See the Pen <a href="https://codepen.io/xiaomuzhu/pen/NZGjYQ/">
  NZGjYQ</a> by Iwobi (<a href="https://codepen.io/xiaomuzhu">@xiaomuzhu</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

#### 两栏布局，防止文字环绕等

<p class="codepen" data-height="300" data-theme-id="33015" data-default-tab="css,result" data-user="xiaomuzhu" data-slug-hash="XLmRPM" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="XLmRPM">
  <span>See the Pen <a href="https://codepen.io/xiaomuzhu/pen/XLmRPM/">
  XLmRPM</a> by Iwobi (<a href="https://codepen.io/xiaomuzhu">@xiaomuzhu</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

#### 防止元素塌陷

<p class="codepen" data-height="300" data-theme-id="33015" data-default-tab="js,result" data-user="xiaomuzhu" data-slug-hash="VJvbEd" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="VJvbEd">
  <span>See the Pen <a href="https://codepen.io/xiaomuzhu/pen/VJvbEd/">
  VJvbEd</a> by Iwobi (<a href="https://codepen.io/xiaomuzhu">@xiaomuzhu</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

**总结**
BFC 是一个独立的布局区域，其中元素按照特定的规则进行布局。
创建BFC 的条件包括浮动元素、绝对定位元素、设置了 overflow 的元素等。
BFC 的布局规则 包括清除浮动、独立的布局、垂直边距折叠等。
使用BFC 可以帮助解决一些常见的布局问题，如清除浮动、避免元素重叠等。

> > 拓展阅读：[深入理解BFC](https://www.cnblogs.com/xiaohuochai/p/5248536.html)

## 为什么有时候人们用translate来改变位置而不是定位？

translate()是transform的一个值。改变transform或opacity不会触发浏览器重新布局（reflow）或重绘（repaint），只会触发复合（compositions）。而改变绝对定位会触发重新布局，进而触发重绘和复合。transform使浏览器为元素创建一个 GPU 图层，但改变绝对定位会使用到 CPU。 因此translate()更高效，可以缩短平滑动画的绘制时间。

而translate改变位置时，元素依然会占据其原始空间，绝对定位就不会发生这种情况。

**transform的优势：**

- **性能优势** 和 **硬件加速** 使得 `transform` 成为创建动画效果的好选择。
- **简化布局代码** 和 **平滑动画** 使得 `transform` 在创建动态布局时更为方便。
- **相对于自身移动** 和 **不影响文档流** 使得 `transform` 更加灵活。

> 拓展阅读:[CSS3 3D transform变换-张鑫旭](https://www.zhangxinxu.com/wordpress/2012/09/css3-3d-transform-perspective-animate-transition/)

## 伪类和伪元素的区别是什么？

伪类和伪元素都是 CSS 中用于添加特殊样式规则的选择器，但它们之间有一些重要的区别。

### 伪类 (Pseudo-classes)

伪类是用来表示元素的某种状态或特定情况的特殊选择器。它们通常以 `:` 开头（在 CSS3 中有时使用双冒号 `::`），后面跟着伪类的名称。伪类不向文档树添加任何额外的节点，而是用来描述元素的当前状态或者交互状态。

#### 例子

- `:hover`: 当用户将鼠标悬停在元素上时应用样式。
- `:active`: 当元素被激活（例如鼠标点击时）时应用样式。
- `:first-child`: 选择作为其父元素的第一个子元素的元素。
- `:nth-child(n)`: 选择其父元素的第 n 个子元素。
- `:visited`: 对已经访问过的链接应用样式。
- `:focus`: 当元素获得焦点时应用样式。

#### 用途

- **状态相关的样式**: 为不同的交互状态（如鼠标悬停、点击等）定义样式。
- **结构相关的样式**: 选择文档中的特定元素（如第一个子元素、偶数行等）。

### 伪元素 (Pseudo-elements)

伪元素则用于选择并设置元素的内容或装饰性部分，而不是元素本身的状态。伪元素也以 `::` 开头（CSS3 规范中），后面跟着伪元素的名称。它们允许你修改元素的部分内容，如插入内容或者添加装饰。

#### 例子

- `::before`: 在元素的内容之前插入内容。
- `::after`: 在元素的内容之后插入内容。
- `::first-letter`: 选择元素的第一个字母。
- `::first-line`: 选择元素的第一行内容。

#### 用途

- **内容注入**: 在元素前后添加文本或符号。
- **装饰**: 添加装饰性的图标、背景或其他视觉元素。
- **修饰文本**: 修改第一行或第一个字母的样式。

### 比较

- **目的**:
  - **伪类**: 描述元素的状态或上下文。
  - **伪元素**: 描述元素的特定部分或插入内容。
- **语法**:
  - **伪类**: 单冒号 `:pseudo-class`。
  - **伪元素**: 双冒号 `::pseudo-element`。注意，在一些老版本的浏览器中仍然可以使用单冒号形式。
- **作用范围**:
  - **伪类**: 影响整个元素。
  - **伪元素**: 影响元素的一部分。

### 示例

#### 伪类示例

```css
a:hover {
    color: red;
}
```

#### 伪元素示例

```css
p::first-letter {
    font-size: 2em;
    font-weight: bold;
}

/* 向每个段落前添加一个图标 */
p::before {
	content: "★";
    color: blue;
}
```

> 拓展阅读：[伪类与伪元素](http://www.alloyteam.com/2016/05/summary-of-pseudo-classes-and-pseudo-elements/)

## 你对flex的理解？✨

Flexbox（Flexible Box Layout Module）是CSS中的一种布局模式，它提供了一种灵活的方式来布局元素，尤其是当涉及到不确定的或动态的尺寸时。Flexbox 可以大大简化复杂的布局任务，并且在响应式设计中非常有用。

### Flexbox 的基本概念

Flexbox 通过将一组元素放入一个容器中来工作，这个容器被称为 Flex Container。容器中的每个子元素称为 Flex Item。

### Flex Container

- **定义**:
  - 一个元素成为 Flex Container 的方法是在其上设置 `display: flex;` 或 `display: inline-flex;`。
- **属性**:
  - **`display: flex;`**: 创建一个块级的 Flex Container。
  - **`display: inline-flex;`**: 创建一个行内级的 Flex Container。

### Flex Items

- **定义**:
  - Flex Container 的直接子元素称为 Flex Items。
- **默认行为**:
  - Flex Items 默认沿主轴排列。
  - 主轴的方向取决于容器的方向。

### Flex Direction

- **定义**:
  - `flex-direction` 属性定义了 Flex Items 的排列方向。
- **取值**:
  - **`row`**: Flex Items 从左到右排列。
  - **`row-reverse`**: Flex Items 从右到左排列。
  - **`column`**: Flex Items 从上到下排列。
  - **`column-reverse`**: Flex Items 从下到上排列。

### Flex Wrap

- **定义**:
  - `flex-wrap` 属性定义了 Flex Items 是否应该换行。
- **取值**:
  - **`nowrap`**: 默认值，不允许 Flex Items 换行。
  - **`wrap`**: 允许 Flex Items 换行，第一行在上方。
  - **`wrap-reverse`**: 允许 Flex Items 换行，第一行在下方。

### Justify Content

- **定义**:
  - `justify-content` 属性定义了 Flex Items 在主轴上的对齐方式。
- **取值**:
  - **`flex-start`**: Flex Items 靠近起点对齐。
  - **`flex-end`**: Flex Items 靠近终点对齐。
  - **`center`**: Flex Items 居中对齐。
  - **`space-between`**: Flex Items 两端对齐，项目之间的间隔相等。
  - **`space-around`**: 每个项目两侧的间隔相等。

### Align Items

- **定义**:
  - `align-items` 属性定义了 Flex Items 在交叉轴上的对齐方式。
- **取值**:
  - **`stretch`**: 默认值，拉伸 Flex Items 以填充容器的剩余空间。
  - **`flex-start`**: Flex Items 靠近起点对齐。
  - **`flex-end`**: Flex Items 靠近终点对齐。
  - **`center`**: Flex Items 居中对齐。
  - **`baseline`**: Flex Items 的基线对齐。

### Align Content

- **定义**:
  - `align-content` 属性定义了多行 Flex Items 在交叉轴上的对齐方式。
- **取值**:
  - **`stretch`**: 默认值，拉伸 Flex Items 以填充容器的剩余空间。
  - **`flex-start`**: Flex Items 靠近起点对齐。
  - **`flex-end`**: Flex Items 靠近终点对齐。
  - **`center`**: Flex Items 居中对齐。
  - **`space-between`**: Flex Items 两端对齐，项目之间的间隔相等。
  - **`space-around`**: 每个项目两侧的间隔相等。

### Flex Grow and Shrink

- **定义**:
  - `flex-grow` 和 `flex-shrink` 属性定义了 Flex Items 如何在容器中扩展或收缩。
- **取值**:
  - **`flex-grow`**: 定义 Flex Item 在可用空间中扩展的比例。
  - **`flex-shrink`**: 定义 Flex Item 在空间不足时收缩的比例。

### Flex Basis

- **定义**:
  - `flex-basis` 属性定义了 Flex Item 的默认尺寸。
- **取值**:
  - 可以是一个长度值（如 `100px`）、百分比（如 `20%`）或关键字 `auto`。

### 示例

假设我们有一个容器，里面包含三个子元素，我们想要它们在容器中均匀分布，并且能够在容器中扩展。

```css
.container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: lightblue;
    padding: 10px;
    height: 100px;
}

.item {
    flex-grow: 1;
    flex-shrink: 1;
    flex-basis: 0;
    background-color: lightgreen;
    padding: 10px;
    margin: 5px;
}
```

```html
<div class="container">
    <div class="item">Item 1</div>
    <div class="item">Item 2</div>
    <div class="item">Item 3</div>
</div>
```

在这个示例中，`.container` 是 Flex Container，`.item` 是 Flex Items。通过设置 `flex-grow: 1;` 和 `flex-shrink: 1;`，Flex Items 可以在容器中均匀地扩展和收缩。

**总结**

- **Flexbox** 是一种强大的布局模式，可以让你轻松地创建响应式的布局。
- **Flex Container** 和 **Flex Items** 是 Flexbox 的核心概念。
- **属性** 如 `flex-direction`, `flex-wrap`, `justify-content`, `align-items`, `align-content`, `flex-grow`, `flex-shrink`, 和 `flex-basis` 控制着 Flex Items 的布局和尺寸。

> 具体用法移步阮一峰的[flex语法](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)、[flex实战](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)，讲得非常通俗易懂，而且我们一两句话说不清楚。

## 什么是FOUC（无样式内容闪烁）？你如何来避免FOUC？

FOUC（Flash of Unstyled Content，无样式内容闪烁）是指在网页加载过程中，由于CSS文件未能及时加载而短暂显示未样式化的页面内容的现象。这通常发生在浏览器开始解析HTML文档并在DOM（Document Object Model）构建完成之前就开始渲染页面时。

### FOUC 发生的原因

1. CSS 文件加载延迟:
   - 如果CSS文件较大或者网络连接慢，可能导致CSS文件加载时间较长。
2. 异步加载CSS:
   - 如果使用了异步加载CSS文件的技术，可能会导致样式延迟应用。
3. CSS 文件路径错误:
   - 如果CSS文件的路径错误或文件不存在，页面将无法应用样式。
4. 浏览器缓存问题:
   - 如果浏览器缓存出现问题，可能会导致CSS文件未能正确加载。

### 如何避免 FOUC

为了避免 FOUC，可以采取以下措施：

1. **内联关键CSS**:

   - 将最重要的CSS内联到HTML文档中，确保页面立即呈现基本样式。
   - 可以使用 `style` 标签将关键样式放置在 `<head>` 部分。

   ```css
   <style>
       /* 内联关键样式 */
       body { background-color: #fff; }
       h1 { color: #333; }
   </style>
   ```

2. **使用 `<link rel="preload">`**:

   - 使用 `rel="preload"` 提前加载关键CSS文件，确保浏览器优先加载这些文件。
   - 可以将此标签放在 `<head>` 部分，以确保CSS尽快加载。

   ```html
   <link rel="preload" href="styles.css" as="style" onload="this.onload=null;this.rel='stylesheet'">
   ```

3. **将CSS放在 `<head>` 的最后**:

   - 确保 `<link rel="stylesheet">` 标签尽可能靠近 `<head>` 的结束标签，这样CSS文件会在文档解析完成之前加载。

   ```html
   <head>
       ...
       <link rel="stylesheet" href="styles.css">
   </head>
   ```

4. **使用媒体查询加载关键CSS**:

   - 可以使用媒体查询来仅加载关键CSS，然后在页面加载完成后通过JavaScript加载完整的样式表。

   ```css
   @media all and (min-width: 0) {
       /* 关键样式 */
       body { background-color: #fff; }
       h1 { color: #333; }
   }
   ```

5. **使用 `<noscript>` 标签**:

   - 如果JavaScript被禁用，可以使用 `<noscript>` 标签来加载关键CSS。

   ```html
   <noscript>
       <style>
           /* 关键样式 */
           body { background-color: #fff; }
           h1 { color: #333; }
       </style>
   </noscript>
   ```

6. **使用 `media="all"`**:

   - 确保 `<link>` 标签的 `media` 属性设置为 `"all"`，以确保CSS文件立即加载。

   ```html
   <link rel="stylesheet" href="styles.css" media="all">
   ```

7. **优化CSS文件**:

   - 减小CSS文件的大小，例如通过压缩和删除不必要的样式。
   - 使用CSS预处理器（如Sass或Less）来组织和优化CSS。

8. **使用 `async` 或 `defer` 属性**:

   - 对于依赖于CSS的JavaScript文件，可以使用 `async` 或 `defer` 属性来确保它们在文档解析完成后加载。

### 示例

结合上述方法，可以创建一个简单的示例来避免 FOUC：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Example Page</title>
    <style>
        /* 内联关键样式 */
        body { background-color: #fff; }
        h1 { color: #333; }
    </style>
    <link rel="preload" href="styles.css" as="style" onload="this.onload=null;this.rel='stylesheet'">
</head>
<body>
    <h1>Welcome to My Site</h1>
    <p>This is an example page.</p>
    <!-- 页面内容 -->
</body>
</html>
```

在这个示例中，我们首先内联了关键样式，然后使用 `rel="preload"` 来提前加载CSS文件。

### 总结

- **FOUC** 是指在网页加载过程中短暂显示未样式化内容的现象。
- **避免 FOUC** 的方法包括内联关键CSS、使用 `rel="preload"`、优化CSS文件等。
- **最佳实践** 是确保页面的关键样式能够快速加载，以提供良好的用户体验。

## CSS的动画与过渡的理解

CSS 动画和过渡是用于为网页元素添加动态效果的重要特性。它们允许网页设计师和开发者以更加流畅和自然的方式改变元素的外观和行为。下面是关于 CSS 动画和过渡的基本概念及其使用方法的概述。

### CSS 过渡 (Transitions)

过渡是一种简单的方式，可以让 CSS 属性在一定时间内平滑地从一个值变化到另一个值。过渡适用于当元素的样式突然改变时，比如当用户悬停或点击元素时。过渡可以应用于多个 CSS 属性，并且可以独立控制每个属性的变化方式。

#### 基本语法

过渡效果可以通过设置以下四个属性来定义：

- `transition-property`: 指定要应用过渡效果的 CSS 属性。
- `transition-duration`: 设置过渡完成所需的时间。
- `transition-timing-function`: 定义过渡的加速度曲线。
- `transition-delay`: 设置过渡开始之前的延迟时间。

例如，要使一个按钮在被悬停时颜色发生变化，我们可以这样写：

```css
button {
    background-color: blue;
    transition-property: background-color;
    transition-duration: 1s;
    transition-timing-function: ease-in-out;
    transition-delay: 0s;
}

button:hover {
    background-color: red;
}
```

简写形式：

```css
button {
    background-color: blue;
    transition: background-color 1s ease-in-out 0s;
}

button:hover {
    background-color: red;
}
```

### CSS 动画 (Animations)

动画允许更复杂的视觉效果，可以定义一系列关键帧来控制元素随时间的变化。动画不仅可以在特定事件（如悬停）触发时播放，还可以自动播放。

#### 基本语法

动画由两部分组成：

- **关键帧**: 使用 `@keyframes` 规则定义动画序列。
- **动画属性**: 应用于元素上的属性，用于控制动画的行为。

例如，创建一个旋转动画：

```css
@keyframes spin {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
}

div {
    width: 100px;
    height: 100px;
    background-color: red;
    animation-name: spin;
    animation-duration: 2s;
    animation-iteration-count: infinite;
    animation-timing-function: linear;
}
```

简写形式：

```css
@keyframes spin {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
}

div {
    width: 100px;
    height: 100px;
    background-color: red;
    animation: spin 2s linear infinite;
}
```

#### 主要属性

- `animation-name`: 指定动画名称。
- `animation-duration`: 动画执行一次所需的时间。
- `animation-timing-function`: 控制动画的速度曲线。
- `animation-delay`: 动画开始前的延迟时间。
- `animation-iteration-count`: 动画播放次数，`infinite` 表示无限循环。
- `animation-direction`: 动画是否反向播放。
- `animation-fill-mode`: 动画结束后元素的状态。
- `animation-play-state`: 动画是否暂停或运行。

### 总结

- **过渡** 适合于简单的状态变化，如颜色改变或尺寸缩放。
- **动画** 更适合于复杂的效果，如旋转、移动和变形等。
- **关键帧** 允许精确控制动画中的每一个步骤。

在实际开发中，过渡通常用于响应用户的交互动作，而动画则常用于自动播放的场景或更复杂的视觉效果。

> 参考资料：
>
> [深入理解CSS动画animation](https://www.cnblogs.com/xiaohuochai/p/5391663.html)
>
> [深入理解CSS过渡transition](https://www.cnblogs.com/xiaohuochai/p/5347930.html)

