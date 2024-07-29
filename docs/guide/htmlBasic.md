# HTML基础



* [doctype(文档类型) 的作用是什么？✨](#doctype的作用是什么？✨)
* [这三种模式的区别是什么？(接上一问追问)](#这三种模式的区别是什么？)
* [HTML、XML 和 XHTML 有什么区别？](#html、xhtml、xml有什么区别)
* [什么是data-属性？](#什么是data-属性？)
* [你对HTML语义化的理解？✨](#你对html语义化的理解？✨)
* [HTML5与HTML4的不同之处](#html5与html4的不同之处)
* [有哪些常用的meta标签？](#有哪些常用的meta标签？)
* [src和href的区别？](#src和href的区别？)
* [知道img的srcset的作用是什么？（追问）](#知道img的srcset的作用是什么？（追问）)
* [还有哪一个标签能起到跟srcset相似作用？（追问）](#还有哪一个标签能起到跟srcset相似作用？（追问）)
* [script标签中defer和async的区别？✨](#script标签中defer和async的区别？✨)
* [有几种前端储存的方式？✨](#有几种前端储存的方式？✨)
* [这些方式的区别是什么？（追问）✨](#这些方式的区别是什么？（追问）✨)

本章是HTML考点的非重难点，因此我们采用简略回答的方式进行撰写，所以不会有太多详细的解释。

> 我们约定，每个问题后我们标记『✨』的为高频面试题

## doctype的作用是什么✨

在 HTML 文档中，`doctype`（文档类型声明）非常重要，它告诉浏览器该页面使用的是哪种版本的 HTML 或 XHTML。这很重要，因为不同的 HTML 版本有不同的规范和解析规则，而浏览器需要根据这些规则来正确地显示页面。

`doctype` 的主要作用包括：

1. **触发标准模式**：当浏览器遇到正确的 doctype 时，它会以“标准模式”来呈现页面，这意味着它会尽量遵循 W3C 标准来解析文档，并且会启用对 CSS 和 JavaScript 的现代支持。
2. **避免怪异模式**：如果没有正确的 doctype 或者使用了错误的 doctype，浏览器可能会进入“怪异模式”或“混杂模式”，这时它会使用一些向后兼容的方式来渲染页面，可能导致布局和样式的问题。

对于 HTML5，正确的 doctype 是：

```html
<!DOCTYPE html>
```

这个声明非常简洁，适用于所有 HTML5 文档。它告诉浏览器这是一个 HTML5 文档，并且应该按照 HTML5 的规范进行解析。

> IE8还有一种介乎于上述两者之间的近乎标准的模式，但是基本淘汰了。

## 这三种模式的区别是什么

标准模式、怪异模式（quirks mode）以及介于两者之间的近乎标准模式（almost standards mode），是浏览器在渲染 HTML 文档时采用的不同方式。这些模式影响着浏览器如何解析文档和渲染页面中的元素。下面是这三种模式的区别：

### 标准模式 (Standards Mode)

- **定义**: 当浏览器检测到正确的文档类型声明（doctype）时，它会进入标准模式。
- 特点:
  - 浏览器会尽可能地遵循 W3C 标准来解析文档。
  - 元素的盒模型（box model）、布局和渲染都会按照标准执行。
  - 支持最新的 CSS 和 JavaScript 特性。
- **示例 Doctype**: 对于 HTML5，正确的 doctype 是 `<!DOCTYPE html>`。

### 怪异模式 (Quirks Mode)

- **定义**: 如果文档缺少 doctype 或使用了一个不正确的 doctype，浏览器可能会进入怪异模式。
- 特点:
  - 浏览器会采用一些非标准的行为来解析文档，以兼容早期网页的设计。
  - 盒模型、布局和渲染规则会有所变化，通常是为了兼容旧的网页。
  - 可能导致页面布局和样式的不一致。
- **示例 Doctype**: 缺少 doctype 或使用如 `<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN" "http://www.w3.org/TR/REC-html40/loose.dtd">` 这样的过时 doctype 都可能导致怪异模式。

### 近乎标准模式 (Almost Standards Mode)

- **定义**: 当文档包含某些特定的错误或不规范的标记时，浏览器可能会进入这种模式。
- 特点:
  - 浏览器试图遵循标准，但在某些方面会退回到非标准行为。
  - 某些元素可能不会完全按照标准模式下的规则来渲染。
- **示例**: 例如，如果一个 HTML5 页面中包含了一些不符合标准的标签或属性，浏览器可能会尝试以近乎标准的方式解析这些内容。

### 总结

- **选择模式**: 使用正确的 doctype 可以确保浏览器以标准模式解析文档。
- **兼容性**: 在开发过程中，应尽量遵循标准以确保跨浏览器的一致性和兼容性。
- **调试**: 如果发现页面在不同浏览器中表现不一致，检查是否进入了怪异模式或近乎标准模式，并修正 doctype 或文档结构。

## HTML、XHTML、XML有什么区别

HTML、XHTML 和 XML 都是用于创建和传输数据的标记语言，但它们之间有一些重要的区别。下面是对这三种语言的基本介绍及其差异：

### HTML (HyperText Markup Language)

- **用途**：HTML 是一种用于创建网页的标准标记语言。它主要用于描述文档的结构和语义。

- **版本**：HTML 有几个版本，包括 HTML 4.01 和 HTML5。

- **语法灵活性**：HTML 的语法相对宽松，可以容忍一些错误和遗漏，例如未闭合的标签或大小写不一致。

- 示例：

  ```html
  <!DOCTYPE html>
  <html>
    <head>
      <title>My Page</title>
    </head>
    <body>
      <h1>Welcome to my page!</h1>
      <p>This is some text.</p>
    </body>
  </html>
  ```

### XHTML (Extensible HyperText Markup Language)

- **用途**：XHTML 是 HTML 的扩展版本，旨在结合 HTML 的表现力和 XML 的严格性。

- **版本**：XHTML 有多个版本，包括 XHTML 1.0 和 XHTML 1.1。

- **语法严格性**：XHTML 的语法更加严格，要求所有的标签必须关闭，属性值必须用引号括起来，且所有的标签和属性都必须是小写的。

- 示例：

  ```html
  <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
  <html xmlns="http://www.w3.org/1999/xhtml">
    <head>
      <title>My Page</title>
    </head>
    <body>
      <h1>Welcome to my page!</h1>
      <p>This is some text.</p>
    </body>
  </html>
  ```

### XML (eXtensible Markup Language)

- **用途**：XML 是一种用于存储和传输数据的语言，它强调数据的结构和内容，而不是展示。

- **语法严格性**：XML 的语法非常严格，不允许有任何语法错误，例如未闭合的标签、空格等。

- **自定义标签**：XML 允许使用自定义的标签和命名空间，使得它非常适合用来表示任何类型的数据。

- 示例：

  ```html
  <?xml version="1.0" encoding="UTF-8"?>
  <catalog>
    <book id="bk101">
      <author>Gambardella, Matthew</author>
      <title>XML Developer's Guide</title>
      <genre>Computer</genre>
      <price>44.95</price>
      <publish_date>2000-10-01</publish_date>
      <description>An in-depth look at creating applications with XML.</description>
    </book>
  </catalog>
  ```

### 主要区别

- **目的**：HTML 主要用于网页展示，XHTML 结合了 HTML 的易用性和 XML 的严格性，而 XML 主要用于数据交换和存储。
- **语法**：HTML 的语法较为宽松，XHTML 和 XML 的语法更为严格。
- **标签和属性**：HTML 中标签和属性可以大写或小写，而在 XHTML 和 XML 中通常都是小写，并且属性值必须用引号括起来。
- **结束标签**：HTML 中的结束标签是可选的，而在 XHTML 和 XML 中必须显式地关闭每个标签。
- **文档类型定义**：HTML 使用 DTD 来定义文档的结构，XHTML 和 XML 也可以使用 DTD 或 XML Schema 来定义文档的结构。

这些区别意味着 HTML 更适合用于构建网页，而 XHTML 和 XML 更适合用于数据交换和存储。

## 什么是data-属性

`data-` 属性是 HTML5 中引入的一种特殊类型的属性，用于在 HTML 元素上存储额外的数据信息。这些属性以 `data-` 前缀开始，后面跟着自定义的名字。`data-` 属性允许开发者将任意数量的键值对附加到 HTML 元素上，而不影响页面的渲染或布局。

### 使用场景

`data-` 属性通常用于以下几种情况：

1. **存储与元素相关联的数据**：这些数据可以是任何与元素相关的元数据或状态信息。
2. **JavaScript 交互**：可以通过 JavaScript 访问这些属性，以便动态更新页面的内容或行为。
3. **CSS 选择器**：虽然不常见，但也可以使用 CSS 选择器来根据 `data-` 属性选择元素。

### 示例

假设我们有一个按钮，我们需要存储按钮的状态信息，比如是否被点击过。

#### HTML 示例

```html
<button id="myButton" data-clicked="false">Click Me!</button>
```

#### JavaScript 示例

```js
document.getElementById('myButton').addEventListener('click', function() {
  this.dataset.clicked = 'true'; // 设置 data- 属性值
  console.log(this.dataset.clicked); // 输出 "true"
});
```

#### CSS 示例

```css
[data-clicked="true"] {
  background-color: yellow; // 当 data-clicked 为 "true" 时改变背景颜色
}
```

### 注意事项

- `data-` 属性名称必须由一个或多个单词组成，每个单词首字母小写。
- 属性名中不能包含连字符 `-` 后面的大写字母，例如 `data-my-Data` 是无效的。
- 在 JavaScript 中，可以通过 `element.dataset` 对象访问 `data-` 属性的值。例如，`element.dataset.clicked` 将返回 `"true"` 或 `"false"`。

> 前端框架出现之后，这种方法已经不流行了

## 你对HTML语义化的理解✨

HTML 语义化是指使用合适的 HTML 标签来表达页面内容的意义和结构，而不是仅仅为了布局和样式的目的。语义化的 HTML 有助于提高网页的可读性、可访问性和搜索引擎优化（SEO），同时也有助于更好地利用现代 Web 技术。

### 为什么重要？

1. **可访问性**：语义化的 HTML 使辅助技术（如屏幕阅读器）能够更好地解析内容，从而帮助视障用户理解页面结构。
2. **搜索引擎优化（SEO）**：搜索引擎能够更容易地理解页面内容，有助于提高网站的搜索排名。
3. **易于维护**：使用语义化标签可以使代码更清晰，便于团队协作和未来的代码维护。
4. **响应式设计**：语义化的 HTML 结构有助于实现更好的响应式设计，因为内容的逻辑结构不受设备尺寸的影响。

### 常见的语义化标签

- **`<header>`**：表示页面或区域的头部。
- **`<nav>`**：用于包含页面导航链接的部分。
- **`<main>`**：表示文档的主要内容，直接与文档主题相关。
- **`<article>`**：代表文档、页面或应用程序中的独立内容。
- **`<section>`**：代表文档中的一个独立部分，通常包含标题。
- **`<aside>`**：用于包含与页面主要内容相关的辅助信息。
- **`<footer>`**：表示页面或区域的底部。

### 示例

下面是一个简单的 HTML 语义化页面结构的例子：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document Title</title>
</head>
<body>
  <header>
    <h1>Page Title</h1>
    <nav>
      <ul>
        <li><a href="#home">Home</a></li>
        <li><a href="#about">About</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <section>
      <h2>About Us</h2>
      <p>This section provides information about our company.</p>
    </section>

    <article>
      <h2>Latest News</h2>
      <p>Here you can find the latest news articles.</p>
    </article>
  </main>

  <aside>
    <h3>Sidebar</h3>
    <p>This sidebar contains additional information and links.</p>
  </aside>

  <footer>
    <p>&copy; 2024 Company Name. All rights reserved.</p>
  </footer>
</body>
</html>
```

通过使用语义化标签，我们可以创建更加有意义、可访问和易于维护的 Web 页面。这不仅有助于提升用户体验，还能够改善网站的整体性能和 SEO 表现。

## HTML5与HTML4的不同之处

HTML5 相对于 HTML4（即 HTML 4.01）进行了许多改进和新增功能，以适应现代 Web 开发的需求。以下是 HTML5 与 HTML4 的一些主要不同之处：

### 新增的语义化标签

HTML5 引入了一系列新的语义化标签，以增强文档结构的清晰度和可读性。这些标签包括：

- `<article>`：表示文档、页面或应用程序中的独立内容。
- `<aside>`：用于包含与页面主要内容相关的辅助信息。
- `<details>`：创建一个可以展开和折叠的细节信息块。
- `<figcaption>`：为 `<figure>` 元素定义标题或说明文字。
- `<figure>`：用于表示媒体内容，如图像、图表或代码示例等。
- `<footer>`：表示页面或区域的底部。
- `<header>`：表示页面或区域的头部。
- `<main>`：表示文档的主要内容。
- `<mark>`：用于高亮文本。
- `<nav>`：用于包含页面导航链接。
- `<section>`：表示文档中的一个独立部分，通常带有标题。
- `<summary>`：用于 `<details>` 元素中，作为可展开内容的摘要。

### 新增的表单控件

HTML5 在表单方面引入了许多新特性，包括：

- `<input type="date">`：用于输入日期。
- `<input type="time">`：用于输入时间。
- `<input type="datetime-local">`：用于输入本地日期和时间。
- `<input type="month">`：用于输入月份和年份。
- `<input type="week">`：用于输入周数和年份。
- `<input type="range">`：用于输入范围滑块。
- `<input type="email">`：用于输入电子邮件地址。
- `<input type="url">`：用于输入 URL 地址。
- `<input type="search">`：用于输入搜索查询。
- `<input type="number">`：用于输入数字。

### 媒体播放

HTML5 添加了 `<audio>` 和 `<video>` 标签，用于直接在浏览器中嵌入音频和视频文件，无需额外插件。

- `<audio>`：用于嵌入音频文件。
- `<video>`：用于嵌入视频文件。

### 图形和绘图

- `<canvas>`：提供了一个用于绘制图形和动画的画布。
- `<svg>`：用于定义基于矢量图形的图像。

### 存储和离线应用

- `localStorage` 和 `sessionStorage`：提供了客户端持久化存储的能力。
- `<application cache>`：允许创建离线可用的应用程序。

### 多媒体和游戏

- `WebGL`：用于渲染 3D 图形。
- `Web Audio API`：用于处理音频。

### 其他改进

- 改进了表单验证，允许使用内置的验证机制。
- 增加了拖放功能（Drag and Drop）。
- 改善了对表单的 `<form>` 标签的支持。
- 删除了过时的标签，如 `<acronym>`、`<applet>`、`<basefont>`、`<big>`、`<center>`、`<dir>`、`<font>`、`<frame>`、`<frameset>`、`<noframes>`、`<strike>` 和 `<tt>` 等。

## 有哪些常用的meta标签

在 HTML 中，`<meta>` 标签用于提供关于 HTML 文档的元数据，这些元数据并不显示在页面上，但会被浏览器和其他 Web 服务所使用。下面是一些常用的 `<meta>` 标签及其用途：

1. **字符集**

   - 标签:

     ```
     <meta charset="UTF-8">
     ```

   - **用途**: 指定文档使用的字符编码。在 HTML5 中，这是必需的，并且通常放在文档的头部。

2. **视口设置**

   - 标签:

     ```
     <meta name="viewport" content="width=device-width, initial-scale=1">
     ```

   - **用途**: 控制网页在移动设备上的呈现方式，特别是缩放级别和初始宽度。

3. **作者信息**

   - 标签:

     ```
     <meta name="author" content="John Doe">
     ```

   - **用途**: 提供文档作者的信息。

4. **关键词**

   - 标签:

     ```
     <meta name="keywords" content="HTML, CSS, JavaScript">
     ```

   - **用途**: 提供与文档相关的关键词列表，但搜索引擎可能不重视此标签。

5. **描述**

   - 标签:

     ```
     <meta name="description" content="This is a short description of the page.">
     ```

   - **用途**: 提供文档的简短描述，这对搜索引擎优化（SEO）非常重要。

6. **兼容性**

   - 标签:

     ```
     <meta http-equiv="X-UA-Compatible" content="IE=edge">
     ```

   - **用途**: 设置 Internet Explorer 的渲染引擎模式，确保页面以最新版本的 IE 渲染。

7. **刷新页面**

   - 标签:

     ```
     <meta http-equiv="refresh" content="5; url=http://www.example.com">
     ```

   - **用途**: 自动刷新页面到指定 URL 或在指定时间后重新加载当前页面。

8. **Open Graph 协议**

   - 标签:

     ```
     <meta property="og:title" content="Page Title">
     <meta property="og:type" content="website">
     <meta property="og:url" content="http://www.example.com">
     <meta property="og:image" content="http://www.example.com/image.jpg">
     ```

   - **用途**: 提供社交媒体平台分享时使用的元数据，如 Facebook。

9. **Twitter Cards**

   - 标签:

     ```
     <meta name="twitter:card" content="summary_large_image">
     <meta name="twitter:site" content="@example">
     <meta name="twitter:title" content="Page Title">
     <meta name="twitter:description" content="This is a short description of the page.">
     <meta name="twitter:image" content="http://www.example.com/image.jpg">
     ```

   - **用途**: 提供 Twitter 分享时使用的元数据。

10. **Robots 指令**

    - 标签:

      ```
      <meta name="robots" content="noindex, nofollow">
      ```

    - **用途**: 指示搜索引擎如何处理页面，例如是否索引页面或跟踪页面上的链接。

11. **HTTP 状态码**

    - 标签:

      ```
      <meta http-equiv="status" content="404 Not Found">
      ```

    - **用途**: 设置 HTTP 状态码，用于服务器端重定向或错误页面。

12. **语言**

    - 标签:

      ```
      <meta http-equiv="Content-Language" content="en-US">
      ```

    - **用途**: 定义页面的主要语言。

## src和href的区别

`src` 和 `href` 是在 HTML 中经常使用的两个属性，它们分别用于不同的目的。下面我将详细介绍这两个属性的区别：

### `src` 属性

- **用途**：`src` 属性用于指定资源的 URL，通常是外部文件的 URL。

- **位置**：`src` 属性通常出现在 `<img>`, `<script>`, `<iframe>`, `<embed>`, `<object>`, `<source>` 和 `<track>` 等元素中。

- **行为**：这些元素会从指定的 URL 加载资源，并将其内容直接嵌入到文档中。

- 示例：

  ```html
  <img src="image.jpg" alt="A beautiful image">
  <script src="script.js"></script>
  ```

### `href` 属性

- **用途**：`href` 属性用于指定超链接的目标 URL 或引用其他资源的 URL。

- **位置**：`href` 属性最常用于 `<a>` 元素，但也用于 `<link>`, `<area>`, `<base>`, `<form>` 等元素中。

- 行为：

  - 对于 `<a>` 元素，它定义了链接的目标地址。
  - 对于 `<link>` 元素，它定义了引用的外部资源（如 CSS 文件）的位置。
  - 对于 `<form>` 元素，它定义了提交表单时的目标 URL。

- 示例：

  ```html
  <a href="https://www.example.com">Visit Example</a>
  <link rel="stylesheet" href="styles.css">
  ```

### 主要区别

- **加载资源 vs. 创建链接**：`src` 用于加载资源并将其内容直接嵌入到文档中，而 `href` 用于创建超链接或引用外部资源。
- **替换 vs. 跳转**：当 `src` 的值发生变化时，会替换现有的资源；而 `href` 的值变化通常不会立即影响页面，除非用户点击链接或表单被提交。
- **元素类型**：`src` 主要用于那些需要直接加载资源的元素，而 `href` 则用于需要创建链接或引用外部资源的元素。

### 总结

- **`src`** 用于加载并嵌入资源，如图片、脚本文件等。
- **`href`** 用于创建超链接或引用外部资源，如 CSS 样式表。

## img的srcset的作用是什么（追问）

`srcset` 属性是 HTML5 中引入的一个重要属性，它用于为 `<img>` 元素提供多个图像源选项，以适应不同的显示条件，如不同的分辨率、设备像素比（DPR）或屏幕尺寸。`srcset` 的主要目的是提高图像加载效率和优化用户体验。

### `srcset` 的基本用法

`srcset` 属性允许您指定多个图像源，每个源都可以具有不同的尺寸或分辨率。您可以为每个图像源指定一个 URL 和可选的描述符，这些描述符可以是图像的宽度、设备像素比 (`x`) 或视窗尺寸 (`vw`)。

**示例**

下面是一个使用 `srcset` 的基本示例：

```html
<img src="image-small.jpg"
     srcset="image-small.jpg 480w,
             image-medium.jpg 960w,
             image-large.jpg 1920w"
     alt="An example image">
```

在这个例子中，浏览器会根据当前视口的宽度选择最合适的图像来源。例如：

- 如果视口宽度小于 480px，浏览器会选择 `image-small.jpg`。
- 如果视口宽度在 480px 和 960px 之间，浏览器会选择 `image-medium.jpg`。
- 如果视口宽度大于 960px，浏览器会选择 `image-large.jpg`。

### 描述符

- **宽度描述符 (`w`)**：指定图像的宽度，单位是像素。浏览器会根据当前视口宽度选择最合适的图像。
- **设备像素比描述符 (`x`)**：指定图像的设备像素比。例如，`2x` 表示图像的分辨率是普通显示器的两倍。
- **视窗尺寸描述符 (`vw`)**：指定图像相对于视窗宽度的比例。例如，`30vw` 表示图像宽度为视窗宽度的 30%。

**示例**

下面是一个使用 `x` 描述符的示例：

```html
<img src="image-small.jpg"
     srcset="image-small.jpg 1x,
             image-medium.jpg 2x,
             image-large.jpg 3x"
     alt="An example image">
```

在这个例子中，浏览器会根据设备的像素密度选择最合适的图像：

- 如果设备像素比是 1x，浏览器会选择 `image-small.jpg`。
- 如果设备像素比是 2x，浏览器会选择 `image-medium.jpg`。
- 如果设备像素比是 3x，浏览器会选择 `image-large.jpg`。

### `sizes` 属性

除了 `srcset` 之外，还可以使用 `sizes` 属性来进一步控制图像的尺寸。`sizes` 属性定义了一个逗号分隔的列表，其中包含了视口宽度的媒体条件及其对应的图像宽度。

**示例**

下面是一个使用 `sizes` 属性的示例：

```html
<img src="image-small.jpg"
     srcset="image-small.jpg 480w,
             image-medium.jpg 960w,
             image-large.jpg 1920w"
     sizes="(max-width: 640px) 480px, (max-width: 1024px) 960px, 1920px"
     alt="An example image">
```

在这个例子中，`sizes` 属性定义了图像宽度在不同视口条件下的选择：

- 如果视口宽度小于等于 640px，浏览器会选择 480px 宽度的图像。
- 如果视口宽度小于等于 1024px，浏览器会选择 960px 宽度的图像。
- 如果视口宽度大于 1024px，浏览器会选择 1920px 宽度的图像。

## 还有哪一个标签能起到跟srcset相似作用（追问）

除了 `<img>` 元素中的 `srcset` 属性外，HTML5 还引入了 `<picture>` 元素，它提供了一种更灵活的方式来选择图像源。`<picture>` 元素允许您根据不同的条件（如设备像素比、视口宽度等）选择不同的图像源，类似于 `srcset`，但它提供了更多的控制和灵活性。

### `<picture>` 元素的用法

`<picture>` 元素通常与 `<source>` 和 `<img>` 元素一起使用。`<source>` 元素定义了不同的图像源及其条件，而 `<img>` 元素则提供了默认的图像源。

**示例**

下面是一个使用 `<picture>` 元素的示例：

```html
<picture>
  <source media="(min-width: 640px)" srcset="image-large.jpg 1920w">
  <source media="(min-width: 480px)" srcset="image-medium.jpg 960w">
  <source media="(min-width: 320px)" srcset="image-small.jpg 480w">
  <img src="image-default.jpg" alt="An example image">
</picture>
```

在这个例子中，`<picture>` 元素包含了三个 `<source>` 元素，每个元素都有一个 `media` 属性来定义图像源适用的条件，以及一个 `srcset` 属性来指定图像源。最后，`<img>` 元素定义了一个默认的图像源。

### 解析过程

当浏览器解析 `<picture>` 元素时，它会按顺序检查每个 `<source>` 元素，并根据当前视口条件选择第一个符合条件的 `<source>` 元素。如果没有任何 `<source>` 元素符合条件，则会使用 `<img>` 元素的 `src` 属性作为回退。

### 优势

- **更精细的控制**：`<picture>` 元素允许您根据不同的媒体查询选择图像，而不仅仅是基于像素比或宽度。
- **多重条件**：可以结合多个条件来选择图像，例如设备像素比和视口宽度。
- **兼容性**：即使浏览器不支持 `<picture>`，也会回退到 `<img>` 元素的 `src` 属性，确保内容仍然可以显示。

### 总结

`<picture>` 元素提供了一种强大的方法来选择合适的图像源，它与 `<img>` 元素中的 `srcset` 属性一起工作，提供了更高级别的灵活性和控制能力。这使得开发者可以根据用户的设备和屏幕尺寸提供最佳的图像质量，同时保持良好的性能和用户体验。

## script标签中defer和async的区别✨

`script`标签中的 defer 和 async 属性用于控制 JavaScript 脚本的加载和执行时机。这两个属性可以帮助优化页面加载性能，特别是在页面中有多个脚本文件时。下面是 defer 和 async 的区别：

### `async` 属性

- **含义**：当 `<script>` 标签包含 `async` 属性时，脚本会在下载完成后立即执行，无论其他脚本是否已经加载完成。

- **并行加载**：`async` 脚本可以在后台并行下载，这意味着它们不会阻塞页面的解析，也不会等待其他脚本完成下载。

- **执行顺序**：`async` 脚本不一定按照 HTML 中出现的顺序执行，而是按照它们加载完成的顺序执行。

- 示例：

  ```html
  <script async src="script1.js"></script>
  <script async src="script2.js"></script>
  ```

### `defer` 属性

- **含义**：当 `<script>` 标签包含 `defer` 属性时，脚本会在页面解析完成后，但在 `DOMContentLoaded` 事件触发之前执行。

- **顺序执行**：即使多个脚本都设置了 `defer` 属性，它们也会按照在 HTML 中出现的顺序依次执行。

- **并行加载**：与 `async` 类似，`defer` 脚本也可以在后台并行下载，不会阻塞页面的解析。

- 示例：

  ```html
  <script defer src="script1.js"></script>
  <script defer src="script2.js"></script>
  ```

![2019-06-13-07-13-42]( https://xiaomuzhu-image.oss-cn-beijing.aliyuncs.com/c84fdc0e47268832fa8914ab4d125002.png)

> 蓝色线代表网络读取，红色线代表执行时间，这俩都是针对脚本的；绿色线代表 HTML 解析

### 主要区别

- 执行时机：
  - `async`: 脚本一旦加载完成就会执行，可能与其他脚本的执行顺序不一致。
  - `defer`: 所有设置了 `defer` 的脚本将在文档解析完成之后、`DOMContentLoaded` 事件触发之前按照 HTML 中的顺序执行。
- 依赖关系：
  - `async`: 不保证脚本间的执行顺序，因此不适用于脚本之间有依赖关系的情况。
  - `defer`: 适用于脚本间有依赖关系的情况，因为它们会按照 HTML 中的顺序执行。

### 何时使用

- 使用 `async`：
  - 当脚本可以独立执行，不需要按照特定顺序执行时。
  - 当脚本加载速度对页面渲染没有直接影响时。
- 使用 `defer`：
  - 当脚本之间有依赖关系，需要按照特定顺序执行时。
  - 当脚本需要在文档解析完成后执行时。

### 注意事项

- 如果 `<script>` 标签同时包含了 `async` 和 `defer` 属性，大多数浏览器会忽略 `defer` 属性，仅保留 `async` 的行为。
- 对于不需要立即执行的脚本，使用 `defer` 可以帮助确保脚本按照预期的顺序执行，同时优化页面加载性能。
- 对于可以立即执行的脚本，使用 `async` 可以帮助加快页面渲染速度。

## 前端储存的方式有几种，有什么区别✨

前端存储是指在客户端（通常是浏览器）上存储数据的技术。这些技术允许 Web 应用程序将数据保存在用户的计算机上，以便在后续的页面加载或离线访问时使用。以下是几种常见的前端存储方式及其区别：

### 1. `localStorage`

- **持久性**：数据永久保存，除非用户清除浏览器缓存或手动删除。

- **容量**：通常每个域名有 5MB 至 10MB 的存储空间。

- **API**：提供了类似 JavaScript 对象的 API，可以使用 `setItem`, `getItem`, `removeItem` 和 `clear` 方法。

- 示例：

  ```js
  localStorage.setItem('key', 'value');
  console.log(localStorage.getItem('key'));
  ```

### 2. `sessionStorage`

- **持久性**：数据在浏览器会话期间保存，当浏览器窗口关闭时数据会被清除。

- **容量**：与 `localStorage` 类似，每个域名有 5MB 至 10MB 的存储空间。

- **API**：提供了与 `localStorage` 相同的 API。

- 示例：

  ```js
  sessionStorage.setItem('key', 'value');
  console.log(sessionStorage.getItem('key'));
  ```

### 3. `cookie`

- **持久性**：可以设置过期时间，如果没有设置过期时间，则在浏览器会话结束时清除。

- **容量**：每个域名最多 4KB。

- **传输**：每次 HTTP 请求都会携带 cookie 数据，这可能会增加网络负载。

- **API**：没有专门的 JavaScript API，需要使用字符串操作来管理。

- 示例：

  ```
  document.cookie = "key=value; expires=Fri, 31 Dec 2024 23:59:59 GMT";
  console.log(document.cookie);
  ```

### 4. `IndexedDB`

- **持久性**：数据永久保存，除非用户清除浏览器缓存或手动删除。

- **容量**：每个域名有较大的存储限制，通常为几百 MB 或更多。

- **API**：提供了复杂的数据库 API，支持事务、索引、多对象存储等功能。

- 示例：

  ```js
  let db;
  const request = indexedDB.open("myDB", 1);
  
  request.onsuccess = function(event) {
    db = request.result;
    console.log("Database opened successfully");
  };
  
  request.onupgradeneeded = function(event) {
    const db = event.target.result;
    const store = db.createObjectStore("store", { keyPath: "id" });
    store.createIndex("name", "name", { unique: false });
  };
  ```

### 5. `Web SQL`

- **持久性**：数据永久保存，除非用户清除浏览器缓存或手动删除。

- **容量**：每个数据库有 5MB 的存储空间。

- **API**：提供了一个 SQL 接口来操作数据库。

- **支持**：Web SQL 不再被推荐使用，并且只在少数浏览器中支持，如 Chrome 和 Safari。

- 示例：

  ```js
  if (window.openDatabase) {
    const db = openDatabase("myDB", "1.0", "Test DB", 5 * 1024 * 1024);
    db.transaction(function(tx) {
      tx.executeSql("CREATE TABLE IF NOT EXISTS test (id INTEGER PRIMARY KEY)");
      tx.executeSql("INSERT INTO test (id) VALUES (?)", [1]);
    });
  }
  ```

### 主要区别

- **容量**：`localStorage` 和 `sessionStorage` 的存储容量较大，而 `cookie` 的容量较小。
- **持久性**：`localStorage` 和 `IndexedDB` 持久保存数据，而 `sessionStorage` 在浏览器会话结束后清除数据。
- **传输**：`cookie` 会在每次 HTTP 请求中传输，可能会增加网络负载，而其他存储方式不会自动发送到服务器。
- **API**：`localStorage` 和 `sessionStorage` 提供了简单的键值对存储，而 `IndexedDB` 提供了更复杂的数据库功能。

### 选择建议

- 对于简单的数据存储和持久化需求，可以使用 `localStorage` 或 `sessionStorage`。
- 对于需要复杂数据结构和事务处理的应用程序，可以考虑使用 `IndexedDB`。
- 对于需要跨域共享数据或需要在服务器端访问的数据，可以使用 `cookie`。

---
参考链接：

1. [src与href](https://blog.csdn.net/Panda_m/article/details/78456358)
2. [语义化](https://www.zhihu.com/question/20455165)
3. [defer和async的区别](https://segmentfault.com/q/1010000000640869)
4. [响应式图片MDN](https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images)
5. [张鑫旭-srcset释义](https://www.zhangxinxu.com/wordpress/2014/10/responsive-images-srcset-size-w-descriptor/)
6. [picture元素-MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/picture)

---

 
