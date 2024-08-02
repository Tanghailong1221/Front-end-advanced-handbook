# JavaScript基础



终于到了大家最擅长的JavaScript部分，相比于HTML和CSS笔者写起JavaScript要顺手很多，虽然前端有三剑客的说法，但是实际应用中基本就是JavaScript为绝对主导，尤其是在工程化的今天。

所以JavaScript才是前端基础面试中的重中之重，在这部分我们会加入一个新的部分就是原理性的解释。

比如，我们会有一个面试问题『解释下变量提升？』，在本章下我们会有一个简短的解释，但是不会解释原理性的东西，因为『简短的解释』是给面试官听的，『原理性的』是给自己解释的，原理性的解释会在相关问题下连接到其他各个原理性详解的章节。

再说一下为什么会有『原理详解』这一part，本项目并不仅想作为面试季帮助大家突击的一个清单，更想做的是帮助大家梳理前端的各个知识点，并把知识点讲透彻，这才是真正对每个开发者有成长的事情。

此外，如果不懂原理，很容易被较真的面试官追问，一下就原形毕露了，所以如果你不懂原理，建议阅读原理部分，如果你已经懂了，可以看简答部分作为梳理即可。

> 我们约定，每个问题后我们标记『✨』的为高频面试题

## 本章索引

- 1. js基础
    - [谈谈你对原型链的理解？ ✨](#谈谈你对原型链的理解？✨)
    - [如何判断是否是数组？](#如何判断是否是数组？)
    - [ES6模块与CommonJS模块有什么区别？](#ES6模块与CommonJS模块有什么区别？)
    - [聊一聊如何在JavaScript中实现不可变对象？](#聊一聊如何在JavaScript中实现不可变对象？)
    - [JavaScript的参数是按照什么方式传递的？](#JavaScript的参数是按照什么方式传递的？)
    - [js有哪些类型?](#js有哪些类型？)
    - [为什么会有BigInt的提案？](#为什么会有BigInt的提案？)
    - [null与undefined的区别是什么？](#null与undefined的区别是什么？)
    - [0.1+0.2为什么不等于0.3？](#0.1+0.2为什么不等于0.3？)
    - [类型转换的规则有哪些？](#类型转换的规则有哪些？)
    - [类型转换的原理是什么？](#类型转换的原理是什么？)
- 2. js机制
    - [解释下变量提升？✨](#解释下变量提升？✨)
    - [一段JavaScript代码是如何执行的？✨](#一段JavaScript代码是如何执行的？✨)
    - [JavaScript的作用域链理解吗？✨](#JavaScript的作用域链理解吗？✨)
    - [谈一谈你对this的了解？✨](#谈一谈你对this的了解？✨)
    - [箭头函数的this指向哪里？✨](#那么箭头函数的this指向哪里？✨)
    - [理解闭包吗？✨](#理解闭包吗？✨)
- 3. js内存
    - [讲讲JavaScript垃圾回收是怎么做的？](#讲讲JavaScript垃圾回收是怎么做的？)
    - [JavaScript的基本类型和复杂类型是储存在哪里的？](#JavaScript的基本类型和复杂类型是储存在哪里的？)
- 4. 异步
    - [async/await 是什么？](#async/await是什么？)
    - [async/await 相比于Promise的优势？](#async/await相比于Promise的优势？)

## JS的数据类型有哪些

JavaScript 的数据类型可以分为两大类：原始类型（也称为基本类型）和引用类型（复合类型）。下面我将详细介绍这两类数据类型：

### 原始类型 (Primitive Types)

原始类型是不可变的数据类型，意味着它们的值不能被更改。JavaScript 中的原始类型包括：

1. **`number`**
   - 包括整数和浮点数。
   - 示例：`42`, `3.14`, `-7`
2. **`string`**
   - 用于表示文本字符串。
   - 示例：`"Hello, world!"`, `'single quotes'`, `"double quotes"`
3. **`boolean`**
   - 二进制逻辑值，只有两个可能的值：`true` 和 `false`。
   - 示例：`true`, `false`
4. **`null`**
   - 特殊的空值，表示没有任何对象值。
   - 示例：`null`
5. **`undefined`**
   - 表示一个变量已经声明但还没有被赋值的情况。
   - 示例：`let x; console.log(x); // undefined`
6. **`symbol`**
   - 一种新的原始类型，从 ES6 开始引入，用于创建唯一的标识符。
   - 示例：`Symbol()`, `Symbol('foo')`
7. **`bigint`**
   - 从 ES10 开始引入的一种新的原始类型，用于表示任意大小的整数。
   - 示例：`9007199254740991n`, `BigInt(123)`

### 引用类型 (Reference Types)

引用类型通常是对象类型的别称，它们存储的是指向实际数据的引用。当赋值或传递这些类型的值时，实际上是复制了这个引用，而不是实际的数据。JavaScript 中的引用类型包括：

1. **`object`**
   - 对象是一种复杂的数据结构，可以包含键值对形式的属性。
   - 示例：`{name: 'Alice', age: 25}`
2. **`array`**
   - 数组是一种特殊的对象类型，用于存储有序的值列表。
   - 示例：`[1, 2, 3]`
3. **`function`**
   - 函数也是对象，并且可以作为值来处理。
   - 示例：`function add(a, b) { return a + b; }`
4. **`date`**, **`regexp`**, **`error`** 等内置对象类型
   - 这些是特定用途的对象类型，例如日期对象、正则表达式对象和错误对象。

### 特殊值

还有一些特殊的非原始类型值，虽然它们不是基础类型的一部分，但在JavaScript中经常使用：

- **`NaN`** (Not-a-Number)
  - 表示不是一个有效的数字。
  - 示例：`0 / 0`, `NaN`
- **`Infinity`** 和 **`-Infinity`**
  - 表示无穷大和负无穷大。
  - 示例：`1 / 0`, `-1 / 0`

这些特殊值的行为类似于 `number` 类型，但在某些数学运算中具有特定的意义。

**总结**

- **原始类型** 是不可变的，而 **引用类型** 是可变的。
- **原始类型** 存储具体的值，而 **引用类型** 存储指向值的引用。
- **原始类型** 和 **引用类型** 之间的转换可以通过类型转换函数（如 `Number()`, `String()` 等）实现。

## undefined 的三种情况

在JavaScript中，`undefined` 是一个原始数据类型，通常表示一个变量已经被声明但是还没有被赋值。`undefined` 还可以出现在其他几种情况下。下面我会详细介绍与 `undefined` 相关的三种常见情况：

### 1. 变量声明但未赋值

当你声明了一个变量但没有给它赋任何值时，它的默认值就是 `undefined`。

#### 示例代码：

```js
let x;
console.log(x); // 输出: undefined
```

### 2. 函数没有返回值

如果你定义了一个函数但没有明确地使用 `return` 语句返回一个值，那么该函数将返回 `undefined`。

#### 示例代码：

```js
function greet(name) {
    console.log("Hello, " + name);
}

const result = greet("John");
console.log(result); // 输出: undefined
```

在这个例子中，`greet` 函数执行了打印操作，但没有返回任何值，所以 `result` 的值是 `undefined`。

### 3. 对象属性不存在

当你尝试访问一个对象上不存在的属性时，该属性的值会被认为是 `undefined`。

#### 示例代码：

```js
const person = {
    name: "Alice",
    age: 25
};

console.log(person.height); // 输出: undefined
```

在这个例子中，`person` 对象没有 `height` 属性，因此 `person.height` 的值为 `undefined`。

总结一下，`undefined` 在 JavaScript 中主要用作以下几种情况的指示：

- 一个变量被声明但尚未赋值。
- 一个函数没有返回任何值。
- 访问对象中的一个不存在的属性。

## 对象模型 BOM 里常用的至少4个对象

浏览器对象模型 (BOM) 是一个提供了浏览器窗口和相关功能的 API。BOM 并不是 ECMAScript 标准的一部分，而是由浏览器厂商自己实现的一套 API。BOM 提供了一些核心对象，允许开发者控制浏览器窗口并与其交互。以下是 BOM 中一些常用的对象：

### 1. `window` 对象

`window` 对象是所有 BOM 对象的顶级容器，代表浏览器窗口本身。几乎所有的 BOM 对象都可以通过 `window` 访问到。一些常见的属性和方法包括：

- 属性:
  - `location`: 获取或设置当前页面的 URL。
  - `history`: 访问浏览器的历史记录。
  - `document`: 访问当前窗口的文档对象。
  - `screen`: 访问屏幕尺寸信息。
  - `navigator`: 访问浏览器信息。
  - `innerWidth`/`innerHeight`: 获取窗口的可视区域尺寸。
  - `outerWidth`/`outerHeight`: 获取窗口的整个尺寸（包括工具栏）。
  - `pageXOffset`/`pageYOffset`: 滚动条的位置。
- 方法:
  - `alert(message)`: 显示警告框。
  - `confirm(message)`: 显示确认对话框。
  - `prompt(message[, default])`: 显示提示输入对话框。
  - `open(url, target, features)`: 打开新窗口。
  - `close()`: 关闭当前窗口。
  - `resizeTo(width, height)`: 调整窗口大小。
  - `resizeBy(width, height)`: 调整窗口大小。
  - `moveTo(x, y)`: 移动窗口位置。
  - `moveBy(x, y)`: 移动窗口位置。
  - `setTimeout(callback, delay[, ...arguments])`: 设置延时调用。
  - `clearTimeout(timeoutID)`: 清除延时调用。
  - `setInterval(callback, delay[, ...arguments])`: 设置周期性调用。
  - `clearInterval(intervalID)`: 清除周期性调用。

### 2. `document` 对象

`document` 对象代表当前加载在浏览器窗口中的 HTML 文档。它允许脚本与网页的内容进行交互。`document` 实际上是一个 `window` 对象的属性，但在这里我们单独列出是因为它非常常用。

- **属性**:
  - `body`: 获取文档的 `<body>` 元素。
  - `title`: 获取或设置文档标题。
  - `referrer`: 获取前一个页面的 URL。
  - `URL`: 当前文档的 URL。
  - `domain`: 当前文档的域名。
  - `cookie`: 当前文档的 cookie 字符串。
  - `lastModified`: 最后一次修改文档的时间。
- **方法**:
  - `getElementById(id)`: 通过 ID 获取元素。
  - `getElementsByClassName(className)`: 通过类名获取元素集合。
  - `getElementsByTagName(tagName)`: 通过标签名获取元素集合。
  - `querySelector(selector)`: 通过 CSS 选择器获取第一个匹配的元素。
  - `querySelectorAll(selector)`: 通过 CSS 选择器获取所有匹配的元素。
  - `createElement(tagName)`: 创建一个新的元素节点。
  - `createTextNode(text)`: 创建一个新的文本节点。
  - `write(html)`: 将 HTML 写入文档流。
  - `writeln(html)`: 将 HTML 写入文档流并在末尾添加换行符。

### 3. `location` 对象

`location` 对象提供有关当前文档 URL 的信息，并允许改变当前文档的地址。

- **属性**:
  - `href`: 当前文档的完整 URL。
  - `protocol`: 协议（如 http:// 或 https://）。
  - `host`: 主机名加上端口号。
  - `hostname`: 仅主机名。
  - `port`: 端口号。
  - `pathname`: 当前文档的路径。
  - `search`: 查询字符串。
  - `hash`: 锚点。
- **方法**:
  - `assign(url)`: 加载指定的 URL。
  - `reload([forceGet])`: 刷新当前文档。
  - `replace(url)`: 替换当前文档的历史记录项。

### 4. `history` 对象

`history` 对象提供了浏览器历史记录的功能。

- **属性**:
  - `length`: 浏览器历史记录条目的数量。
- **方法**:
  - `back()`: 返回上一页。
  - `forward()`: 前往下一页。
  - `go([delta])`: 前往指定的页面。

### 5. `navigator` 对象

`navigator` 对象提供了有关用户浏览器的信息。

- 属性:
  - `appName`: 浏览器名称。
  - `appVersion`: 浏览器版本信息。
  - `platform`: 用户的操作系统平台。
  - `userAgent`: 用户代理字符串。
  - `language`: 用户首选语言。
  - `languages`: 用户首选语言列表。

## document load 和 document ready 的区别

`document load` 和 `document ready` 是两个不同的概念，它们分别描述了文档加载的不同阶段。理解这两个概念的区别对于编写高效的 JavaScript 代码非常重要。

### 1. `document load` (Load Event)

`load` 事件是在文档及其所有依赖资源（如图片、样式表、脚本等）完全加载完毕后触发的。这意味着页面上的所有资源都已经下载完成并且可用。

- **特点**:

  - 确保所有资源都已加载完毕。
  - 适用于需要等待所有资源加载完成才能运行的代码。
  - 由于需要等待所有资源加载，可能会导致延迟。

- **示例**:

  ```js
  window.addEventListener('load', function() {
      console.log('Document and all resources have been loaded.');
  });
  ```

### 2. `document ready` (Ready State)

`document ready` 不是一个正式的事件，而是指文档已经准备好可以被查询和操作的状态。在 jQuery 中，`$(document).ready()` 方法是常用的处理文档准备好的方式。

- **特点**:

  - DOM（文档对象模型）已经加载完成，可以开始操作页面元素。
  - 不需要等待所有资源加载完毕。
  - 更快地执行 JavaScript 代码，提高用户体验。

- **示例** (使用 jQuery):

  ```js
  $(document).ready(function() {
      console.log('DOM is ready to be manipulated.');
  });
  ```

或者简写为:

```js
$(function() {
    console.log('DOM is ready to be manipulated.');
});
```

### 总结

- **`document load`**:
  - 等待所有资源加载完毕。
  - 适用于依赖于页面所有资源加载完成的场景。
- **`document ready`**:
  - DOM 加载完成后即可执行。
  - 更适合大多数场景，因为它提高了应用程序的响应速度。

### 注意事项

- 如果你的代码只需要操作 DOM 而不需要等待图像或其他资源加载完成，那么使用 `document ready` 是更好的选择。
- 如果你的代码需要等到所有资源都加载完成，比如处理复杂的图像处理或依赖于特定资源的存在，那么应该等待 `document load` 事件。

## 普通事件绑定和事件流绑定有啥区别

在JavaScript中，事件绑定指的是将一个事件处理程序与一个DOM元素关联起来的过程。根据事件绑定的方式不同，我们可以将其大致分为两类：**普通事件绑定**和**事件流绑定**。下面是这两种绑定方式的详细说明及其区别。

### 1. 普通事件绑定 (Standard Event Binding)

普通事件绑定是最常见的事件绑定方式，它直接将事件处理器与特定的DOM元素绑定在一起。当事件发生时，事件处理器会被调用。

#### 特点：

- 事件处理器直接绑定到目标元素上。
- 通常使用 `element.addEventListener` 或者 `element.onclick = function` 这样的方式绑定。
- 事件处理器只能在目标元素上触发。

#### 示例代码：

```js
// 使用 addEventListener
button.addEventListener('click', function(event) {
    console.log('Button was clicked!');
});

// 使用 onclick 属性
button.onclick = function(event) {
    console.log('Button was clicked!');
};
```

### 2. 事件流绑定 (Event Delegation or Event Bubbling)

事件流绑定利用了事件冒泡的机制，将事件处理器绑定到一个父元素上，而不是直接绑定到目标元素上。这样做的好处是可以处理动态生成的子元素的事件，而无需为每个子元素单独绑定事件处理器。

#### 特点：

- 事件处理器绑定到父元素上。
- 利用了事件冒泡机制，在事件冒泡过程中捕获事件。
- 可以处理动态生成的子元素的事件。

#### 示例代码：

```js
// 使用 addEventListener 并在父元素上监听
parentElement.addEventListener('click', function(event) {
    if (event.target.matches('.child-element')) {
        console.log('Child element was clicked!');
    }
});
```

### 比较与区别

- **直接绑定 vs 事件委托**:
  - 直接绑定将事件处理器直接绑定到目标元素上。
  - 事件委托将事件处理器绑定到父元素上，通过事件冒泡机制来处理子元素的事件。
- **性能**:
  - 直接绑定可能需要为多个元素分别绑定事件处理器，如果元素很多，这可能会导致性能问题。
  - 事件委托只需要一个事件处理器，减少了内存占用和事件处理器的数量，从而提高性能。
- **灵活性**:
  - 直接绑定适用于静态页面，其中元素在页面加载时就已经存在。
  - 事件委托适用于动态页面，特别是当页面元素动态生成或频繁变化时。
- **代码维护**:
  - 直接绑定可能需要为每个元素维护单独的事件处理器。
  - 事件委托通常只需要一个事件处理器，简化了代码维护。

### 总结

选择哪种事件绑定方式取决于具体的应用场景。如果页面元素较少且不经常变化，使用普通的事件绑定方式就足够了。但如果页面元素很多或经常动态生成，则使用事件流绑定（事件委托）可以显著提高代码的效率和可维护性。

## 如何阻止事件冒泡和默认事件

在JavaScript中，阻止事件冒泡和默认行为是事件处理中的两个常见需求。下面我将分别解释如何实现这两点：

### 阻止事件冒泡

事件冒泡是指事件从最深的节点开始向上冒泡，直到到达文档根节点。这意味着一个事件可以被多个元素监听并响应。如果你不想让事件继续向上冒泡，可以使用 `stopPropagation()` 方法。

#### 示例代码：

```js
document.getElementById('myButton').addEventListener('click', function(event) {
    event.stopPropagation(); // 阻止事件冒泡
    console.log('Button clicked');
});

document.getElementById('myDiv').addEventListener('click', function(event) {
    console.log('Div clicked');
});
```

在这个例子中，当按钮被点击时，点击事件不会冒泡到包含它的 `div` 元素，因此 `Div clicked` 不会被输出。

### 阻止默认行为

阻止默认行为是指取消浏览器对某些事件的默认处理方式。例如，点击链接会跳转到新的页面，提交表单会重新加载页面等。你可以使用 `preventDefault()` 方法来阻止这些默认行为。

#### 示例代码：

```js
document.getElementById('myLink').addEventListener('click', function(event) {
    event.preventDefault(); // 阻止链接的默认行为
    console.log('Link clicked but not navigated');
});
```

在这个例子中，点击链接时控制台会输出 `Link clicked but not navigated`，但页面不会跳转到链接指向的URL。

### 使用 `return false`

除了使用 `preventDefault()` 和 `stopPropagation()` 外，还可以使用 `return false` 的方式同时阻止事件冒泡和默认行为。这是因为返回 `false` 通常意味着取消默认行为并且停止事件传播。

#### 示例代码：

```js
document.getElementById('myForm').addEventListener('submit', function(event) {
   	 console.log('Form submitted');
    return false; // 阻止默认行为并且停止事件传播
});
```

在这个例子中，当表单被提交时，控制台会输出 `Form submitted`，但页面不会重新加载。

### 注意事项

- 使用 `event.preventDefault()` 和 `event.stopPropagation()` 需要确保事件处理函数中使用了 `event` 参数。
- 如果事件处理函数是匿名函数或者箭头函数，那么 `this` 关键字将会指向全局对象（浏览器中通常是 `window`）。如果需要访问元素本身，可以使用 `event.currentTarget`。
- 如果使用 `return false` 的方式，注意它会同时阻止默认行为和冒泡，所以在某些情况下可能不需要这么做。

## 解释下变量提升✨

变量提升（hoisting）是JavaScript中一个重要的特性，它影响着变量声明的解析过程。变量提升并不是真正地将变量移动到作用域的顶部，而是一种语法糖，用来描述JavaScript引擎在编译阶段如何处理变量声明。

### 变量提升的基本概念

变量提升意味着变量声明会被提前到作用域的顶部，但这只包括变量的声明部分，而不包括初始化部分。也就是说，变量会被声明，但如果没有显式地初始化，它们会被赋予默认值 `undefined`。

### 例子

让我们来看几个例子来更好地理解变量提升的概念。

#### 1. 变量声明提升

```js
console.log(x); // 输出: undefined
var x = 5;
```

在这个例子中，尽管 `x` 的赋值发生在变量使用之后，但由于变量提升的作用，`x` 的声明被提升到了作用域的顶部。因此，这段代码实际上相当于下面的形式：

```js
var x; // 声明被提升
console.log(x); // 输出: undefined
x = 5; // 初始化
```

#### 2. 函数声明提升

函数声明也会被提升，这意味着可以在声明之前调用函数。

```js
console.log(greet("Alice")); // 输出: Hello, Alice!

function greet(name) {
    return "Hello, " + name + "!";
}
```

实际上，这段代码会被解释器处理为如下形式：

```js
function greet(name) {
    return "Hello, " + name + "!";
}

console.log(greet("Alice")); // 输出: Hello, Alice!
```

#### 3. 函数表达式不提升

函数表达式的赋值不会被提升，只有变量声明会被提升。

```js
console.log(greet("Bob")); // 输出: TypeError: greet is not a function

var greet = function(name) {
    return "Hello, " + name + "!";
};
```

这段代码实际上会被解释器处理为如下形式：

```js
var greet; // 变量声明被提升
console.log(greet("Bob")); // 输出: TypeError: greet is not a function
greet = function(name) {
    return "Hello, " + name + "!";
};
```

### 注意事项

- **变量提升只涉及声明**：变量的初始化部分不会被提升。
- **函数声明会被完全提升**：不仅声明会被提升，函数体也会被提升。
- **函数表达式只提升变量声明**：函数表达式的赋值部分不会被提升。
- **`let` 和 `const` 的提升行为**：虽然 `let` 和 `const` 也会提升声明，但它们处于暂时性死区（TDZ），即在声明之前不能被访问。

> 原理详解请移步,[预解释与变量提升](hoisting.md)

## 一段JavaScript代码是如何执行的✨

JavaScript代码的执行过程涉及到多个步骤，包括编译、执行、作用域解析、垃圾回收等。下面我将详细解释这些步骤以及它们如何共同作用来执行JavaScript代码。

### 1. 编译

在JavaScript代码被执行之前，JavaScript引擎首先会对代码进行预处理和编译。这个过程包括解析源代码并构建抽象语法树（Abstract Syntax Tree, AST）。AST是一个表示代码结构的树形数据结构，它使得JavaScript引擎能够更容易地理解和执行代码。

### 2. 执行上下文创建

JavaScript引擎创建一个执行上下文（Execution Context）来跟踪代码的执行状态。执行上下文有两种主要类型：全局执行上下文和函数执行上下文。

- **全局执行上下文**：这是程序启动时创建的第一个执行上下文，它包含全局变量和全局函数。
- **函数执行上下文**：每当一个函数被调用时都会创建一个新的函数执行上下文。

### 3. 作用域链

每个执行上下文都有一个作用域链（Scope Chain），它是一个指向作用域的链表，用于解析变量和函数的标识符。作用域链的头部始终是当前执行上下文的局部作用域，后面跟着父级作用域，最后是全局作用域。

### 4. 变量提升

在执行上下文创建的过程中，JavaScript引擎会进行变量提升。这意味着所有变量和函数声明都会被提升到当前作用域的顶部，但只有声明会被提升，初始化部分不会被提升。

### 5. 代码执行

一旦执行上下文和作用域链建立好，JavaScript引擎就会按照顺序执行代码。代码执行时，引擎会逐行读取和执行语句。

### 6. 变量和函数的解析

在执行过程中，如果遇到变量或函数的引用，JavaScript引擎会沿着作用域链查找相应的定义。如果在当前作用域找不到，引擎将继续向上查找，直到找到定义或到达全局作用域。

### 7. 函数调用

当遇到函数调用时，JavaScript引擎会创建一个新的函数执行上下文，并将其压入执行上下文栈。然后，函数内部的代码开始执行，直到函数返回。

### 8. 垃圾回收

JavaScript引擎使用自动垃圾回收机制来管理内存。当不再需要某个变量或对象时，它们会被标记为可回收，最终由垃圾回收器释放内存。

### 9. 异步事件处理

JavaScript是单线程的，但支持异步编程模式，如回调函数、Promises 和 async/await。异步操作通常使用事件循环机制来处理，它们会在适当的时机被加入到任务队列中，并在主线程空闲时执行。

### 10. 事件循环

事件循环是JavaScript中处理异步操作的核心机制。它不断地检查是否有待处理的任务，如果有，则从任务队列中取出任务并执行。事件循环确保JavaScript能够处理异步事件而不会阻塞主线程。

### 示例代码执行流程

假设我们有以下简单的JavaScript代码：

```js
console.log("Start");

function greet(name) {
    console.log("Hello, " + name + "!");
}

greet("Alice");

console.log("End");
```

### 执行流程分析

1. **编译**：
   - JavaScript引擎解析代码并构建AST。
   - 创建全局执行上下文。
2. **变量提升**：
   - 变量 `greet` 的声明被提升到全局作用域的顶部。
   - 函数 `greet` 的声明被提升。
3. **执行**：
   - 执行 `console.log("Start");`，输出 "Start"。
   - 调用 `greet("Alice")`
     - 创建一个新的函数执行上下文。
     - 在函数作用域中，参数 `name` 被赋值为 "Alice"。
     - 执行 `console.log("Hello, " + name + "!");`，输出 "Hello, Alice!"。
     - 函数执行上下文被销毁。
   - 执行 `console.log("End");`，输出 "End"。

> 此部分涉及概念较多，请移步[JavaScript执行机制](mechanism)

## 讲讲对闭包的理解与使用场景✨

### 闭包是什么

MDN的解释：闭包是函数和声明该函数的词法环境的组合。

按照我的理解就是：闭包 =『函数』和『函数体内可访问的变量总和』

### 闭包的定义

闭包是由函数及其相关的引用环境组合而成的一个实体。简单来说，当一个函数能够记住并访问在其外部定义的变量时，就形成了一个闭包。这些变量不会因为外部函数执行结束而被垃圾回收。

### 闭包的组成

闭包由三部分组成：

1. **函数**：一个函数体。
2. **引用环境**：函数体内部引用的所有外部变量。
3. **作用域链**：用于解析变量的链表。

### 闭包的工作原理

当一个函数被定义在一个外层函数内部时，它可以访问外层函数的局部变量、参数以及其他定义在外层函数内的函数。当外层函数执行完毕后，内层函数仍然可以访问这些变量，即使这些变量原本应该随着外层函数的执行结束而被销毁。

### 闭包的作用

闭包最大的作用就是隐藏变量，闭包的一大特性就是**内部函数总是可以访问其所在的外部函数中声明的参数和变量，即使在其外部函数被返回（寿命终结）了之后**。基于此特性，JavaScript可以实现私有变量、特权变量、储存变量等。

我们就以私有变量举例，私有变量的实现方法很多，有靠约定的（变量名前加_）,有靠Proxy代理的，也有靠Symbol这种新数据类型的。

但是真正广泛流行的其实是使用闭包。

```js
function Person(){
    var name = 'cxk';
    this.getName = function(){
        return name;
    }
    this.setName = function(value){
        name = value;
    }
}

const cxk = new Person()

console.log(cxk.getName()) //cxk
cxk.setName('jntm')
console.log(cxk.getName()) //jntm
console.log(name) //name is not defined
```

函数体内的`var name = 'cxk'`只有`getName`和`setName`两个函数可以访问，外部无法访问，相对于将变量私有化。

### 使用场景

闭包在JavaScript中有多种使用场景，以下是一些常见的应用场景：

1. **模块化编程**：

   - 闭包可以用来模拟私有成员（变量和函数），这对于实现模块化编程非常有用。
   - 通过闭包，你可以创建一个公共接口，而将内部实现细节隐藏起来。

   ```js
   function createCounter() {
       let count = 0;
   
       function increment() {
           count++;
           return count;
       }
   
       function decrement() {
           count--;
           return count;
       }
   
       return {
           increment,
           decrement
       };
   }
   
   const counter = createCounter();
   console.log(counter.increment()); // 输出: 1
   console.log(counter.decrement()); // 输出: 0
   ```

2. **事件处理**：

   - 闭包可以用来在事件处理函数中保存上下文信息。
   - 例如，当创建一系列按钮时，每个按钮的点击事件处理函数都需要访问不同的数据。

   ```js
   function createButtons(count) {
       for (let i = 1; i <= count; i++) {
           const button = document.createElement('button');
           button.textContent = 'Button ' + i;
           button.addEventListener('click', function() {
               console.log('Button ' + i + ' was clicked');
           });
           document.body.appendChild(button);
       }
   }
   
   createButtons(3);
   ```

3. **函数工厂**：

   - 闭包可以用来创建函数工厂，即一个函数返回另一个函数。
   - 这种模式在创建带有预设参数的函数时非常有用。

   ```js
   function createAdder(x) {
       return function(y) {
           return x + y;
       };
   }
   
   const addFive = createAdder(5);
   console.log(addFive(10)); // 输出: 15
   ```

4. **保持状态**：

   - 闭包可以用来保持函数执行之间的一些状态。
   - 这对于实现计数器、定时器等功能非常有用。

   ```js
   function createTimer() {
       let start = Date.now();
   
       return function() {
           return Date.now() - start;
       };
   }
   
   const timer = createTimer();
   console.log(timer()); // 输出: 从创建到现在经过的时间（毫秒）
   ```

### 闭包注意事项

- **内存泄漏**：如果闭包中的变量没有正确地释放，可能会导致内存泄漏。
- **作用域链**：闭包中的函数可以访问其外部作用域中的变量，但不能访问同级作用域中的变量。
- **性能考虑**：闭包可能会导致额外的内存消耗，特别是在大量使用闭包的情况下。

### 总结

闭包是JavaScript中一个非常强大的特性，它允许函数保留对外部作用域变量的引用。通过合理地使用闭包，可以实现许多高级功能，如模块化、事件处理、状态保持等。理解闭包的工作原理对于编写高效、可维护的JavaScript代码至关重要。

## 对JavaScript的作用域链的理解✨

作用域链（Scope Chain）是JavaScript中一个非常重要的概念，它决定了变量的可访问性和查找机制。作用域链定义了变量解析的规则，即当JavaScript引擎试图查找一个变量时，它会遵循一个特定的路径来寻找该变量的定义。下面我将详细介绍作用域链的概念、工作原理以及一些示例。

### 作用域链的基本概念

在JavaScript中，每个执行上下文（Execution Context）都有一个与之相关联的作用域链。作用域链是一个指针列表，它包含了当前执行上下文以及所有父级执行上下文的作用域。作用域链的主要目的是允许引擎查找变量和函数的定义。

其本质是JavaScript在执行过程中会创造可执行上下文，可执行上下文中的词法环境中含有外部词法环境的引用，我们可以通过这个引用获取外部词法环境的变量、声明等，这些引用串联起来一直指向全局的词法环境，因此形成了作用域链。

![2019-06-20-06-00-27]( https://xiaomuzhu-image.oss-cn-beijing.aliyuncs.com/0f1701f3b7061942ae24a9357f28bc2e.png)

### 执行上下文

执行上下文分为两种类型：

- **全局执行上下文**：当JavaScript程序开始执行时，会创建一个全局执行上下文。它包含了全局变量和函数。
- **函数执行上下文**：每当一个函数被调用时，都会创建一个新的函数执行上下文。

### 作用域链的构建

当一个函数执行上下文被创建时，JavaScript引擎会构建一个作用域链，这个作用域链包含当前函数的作用域以及所有父级函数的作用域，一直到全局作用域。

### 作用域链的查找机制

当JavaScript引擎尝试查找一个变量或函数时，它会从当前执行上下文的作用域开始查找，如果没有找到，则沿着作用域链向上查找，直到找到变量的定义或到达全局作用域。如果在全局作用域中仍然没有找到，那么该变量被认为是未定义的。

### 示例代码

让我们通过一个简单的示例来说明作用域链的工作原理：

```js
function outerFunction() {
    var outerVar = "I'm outer";

    function innerFunction() {
        var innerVar = "I'm inner";
        console.log(outerVar); // 输出: I'm outer
        console.log(innerVar); // 输出: I'm inner
    }

    innerFunction();
}

outerFunction();
```

### 作用域链分析

1. **全局执行上下文**：
   - 创建全局执行上下文，其中包括全局变量和函数。
   - 全局作用域成为作用域链的最后一个环节。
2. **`outerFunction` 执行上下文**：
   - 当 `outerFunction` 被调用时，创建一个 `outerFunction` 执行上下文。
   - 构建作用域链，它包含当前函数的作用域和全局作用域。
   - `outerVar` 被定义在当前作用域中。
3. **`innerFunction` 执行上下文**：
   - 当 `innerFunction` 被调用时，创建一个 `innerFunction` 执行上下文。
   - 构建作用域链，它包含当前函数的作用域、`outerFunction` 的作用域和全局作用域。
   - `innerVar` 被定义在当前作用域中。
   - 当尝试访问 `outerVar` 时，它首先在当前作用域中查找，然后沿着作用域链向上查找，最终在 `outerFunction` 的作用域中找到。

### 作用域链与闭包

闭包是作用域链的一个应用。当一个函数返回一个内部函数时，内部函数可以访问并保持对其外部作用域中的变量的引用。这是因为内部函数的作用域链包含了外部函数的作用域，即使外部函数已经执行完毕，内部函数仍然可以访问这些变量。

### 示例代码

```js
function outerFunction() {
    var outerVar = "I'm outer";

    function innerFunction() {
        console.log(outerVar); // 输出: I'm outer
    }

    return innerFunction;
}

const innerFunc = outerFunction();
innerFunc(); // 输出: I'm outer
```

### 总结

- **作用域链** 是由当前执行上下文的作用域和所有父级执行上下文的作用域组成的链表。
- **作用域链** 用于查找变量和函数的定义。
- **闭包** 是作用域链的一个应用，允许内部函数访问外部函数的作用域中的变量。

> 原理详解请移步[JavaScript执行机制](#mechanism)

## ES6模块与CommonJS模块有什么区别

ES6 Module和CommonJS模块的区别：

* CommonJS是对模块的浅拷贝，ES6 Module是对模块的引用,即ES6 Module只存只读，不能改变其值，具体点就是指针指向不能变，类似const
* import的接口是read-only（只读状态），不能修改其变量值。
即不能修改其变量的指针指向，但可以改变变量内部指针指向,可以对commonJS对重新赋值（改变指针指向），但是对ES6 Module赋值会编译报错。

ES6 Module和CommonJS模块的共同点：

* CommonJS和ES6 Module都可以对引入的对象进行赋值，即对对象内部属性的值进行改变。

> 详解请移步[ES6模块与CommonJS模块的差异](http://es6.ruanyifeng.com/#docs/module-loader#ES6-%E6%A8%A1%E5%9D%97%E4%B8%8E-CommonJS-%E6%A8%A1%E5%9D%97%E7%9A%84%E5%B7%AE%E5%BC%82)

## js有哪些类型？

JavaScript的类型分为两大类，一类是原始类型，一类是复杂(引用）类型。

原始类型:

* boolean
* null
* undefined
* number
* string
* symbol

复杂类型:

* Object

还有一个没有正式发布但即将被加入标准的原始类型BigInt。

## 为什么会有BigInt的提案？

JavaScript中Number.MAX_SAFE_INTEGER表示最大安全数字,计算结果是9007199254740991，即在这个数范围内不会出现精度丢失（小数除外）。

但是一旦超过这个范围，js就会出现计算不准确的情况，这在大数计算的时候不得不依靠一些第三方库进行解决，因此官方提出了BigInt来解决此问题。

## null与undefined的区别是什么？

null表示为空，代表此处不应该有值的存在，一个对象可以是null，代表是个空对象，而null本身也是对象。

undefined表示『不存在』，JavaScript是一门动态类型语言，成员除了表示存在的空值外，还有可能根本就不存在（因为存不存在只在运行期才知道），这就是undefined的意义所在。

## 0.1+0.2为什么不等于0.3？

![2019-06-23-09-24-06]( https://xiaomuzhu-image.oss-cn-beijing.aliyuncs.com/b9aa4056155df1baae69d6de5a0ac322.png)

JS 的 `Number` 类型遵循的是 IEEE 754 标准，使用的是 64 位固定长度来表示。

IEEE 754 浮点数由三个域组成，分别为 sign bit (符号位)、exponent bias (指数偏移值) 和 fraction (分数值)。64 位中，sign bit 占 1 位，exponent bias 占 11 位，fraction 占 52 位。

通过公式表示浮点数的值 **value = sign x exponent x fraction**<br />**<br />当一个数为正数，sign bit 为 0，当为负数时，sign bit 为 1.

以 0.1 转换为 IEEE 754 标准表示为例解释一下如何求 exponent bias 和 fraction。转换过程主要经历 3 个过程：

1. 将 0.1 转换为二进制表示
1. 将转换后的二进制通过科学计数法表示
1. 将通过科学计数法表示的二进制转换为 IEEE 754 标准表示


### 将 0.1 转换为二进制表示

回顾一下一个数的小数部分如何转换为二进制。一个数的小数部分，乘以 2，然后取整数部分的结果，再用计算后的小数部分重复计算，直到小数部分为 0 。

因此 0.1 转换为二进制表示的过程如下：

| 小数 | x2 的结果 | 整数部分 |
| :---: | :---: | :---: |
| 0.1 | 0.2 | 0 |
| 0.2 | 0.4 | 0 |
| 0.4 | 0.8 | 0 |
| 0.8 | 1.6 | 1 |
| 0.6 | 1.2 | 1 |
| 0.2 | 0.4 | 0 |
| 0.4 | 0.8 | 0 |
| 0.8 | 1.6 | 1 |
| 0.6 | 1.2 | 1 |
| ... | ... | ... |

得到 0.1 的二进制表示为 0.00011...(无限重复 0011)

### 通过科学计数法表示

0.00011...(无限重复 0011) 通过科学计数法表示则是 1.10011001...(无线重复 1001)*2

### 转换为 IEEE 754 标准表示

当经过科学计数法表示之后，就可以求得 exponent bias 和 fraction 了。

exponent bias (指数偏移值) **等于** 双精度浮点数**固定偏移值** (2-1) 加上指数实际值(即 2 中的 -4) 的 **11 位二进制表示**。为什么是 11 位？因为 exponent bias 在 64 位中占 11 位。

因此 0.1 的 exponent bias **等于** 1023 + (-4) = 1019 的11 位二进制表示，即 011 1111 1011。

再来获取 0.1 的 fraction，fraction 就是 1.10011001...(无线重复 1001) 中的小数位，由于 fraction 占 52位所以抽取 52 位小数，1001...(中间有 11 个 1001)...1010 **(请注意最后四位，是 1010 而不是 1001，因为四舍五入有进位，这个进位就是造成 0.1 + 0.2 不等于 0.3 的原因)**

```
    0       011 1111 1011   1001...( 11 x 1001)...1010
(sign bit) (exponent bias)      (fraction)
```

此时如果将这个数转换为十进制，可以发现值已经变为 0.100000000000000005551115123126 而不是 0.1 了，因此这个计算精度就出现了问题。

## 类型转换的规则有哪些？

在if语句、逻辑语句、数学运算逻辑、==等情况下都可能出现隐士类型转换。

![2019-06-23-09-32-17]( https://xiaomuzhu-image.oss-cn-beijing.aliyuncs.com/c378afab84afcdf430aec5229649faee.png)

## 类型转换的原理是什么？


**类型转换**指的是将一种类型转换为另一种类型,例如:
```javascript
var b = 2;
var a = String(b);
console.log(typeof a); //string
```

当然,**类型转换**分为显式和隐式,但是不管是隐式转换还是显式转换,都会遵循一定的原理,由于JavaScript是一门动态类型的语言,可以随时赋予任意值,但是各种运算符或条件判断中是需要特定类型的,因此JavaScript引擎会在运算时为变量设定类型.

这看起来很美好,JavaScript引擎帮我们搞定了`类型`的问题,但是引擎毕竟不是ASI(超级人工智能),它的很多动作会跟我们预期相去甚远,我们可以从一到面试题开始.

```javascript
{}+[] //0
```


答案是0

是什么原因造成了上述结果呢?那么我们得从ECMA-262中提到的转换规则和抽象操作说起,有兴趣的童鞋可以仔细阅读下这浩如烟海的[语言规范](http://ecma-international.org/ecma-262/5.1/),如果没这个耐心还是往下看.

这是JavaScript种类型转换可以从**原始类型**转为**引用类型**,同样可以将**引用类型**转为**原始类型**,转为原始类型的抽象操作为`ToPrimitive`,而后续更加细分的操作为:`ToNumber ToString ToBoolean`。

为了更深入的探究JavaScript引擎是如何处理代码中类型转换问题的,就需要看 ECMA-262详细的规范,从而探究其内部原理,我们从这段内部原理示意代码开始.

```javascript
// ECMA-262, section 9.1, page 30. Use null/undefined for no hint,
// (1) for number hint, and (2) for string hint.
function ToPrimitive(x, hint) {  
  // Fast case check.
  if (IS_STRING(x)) return x;
  // Normal behavior.
  if (!IS_SPEC_OBJECT(x)) return x;
  if (IS_SYMBOL_WRAPPER(x)) throw MakeTypeError(kSymbolToPrimitive);
  if (hint == NO_HINT) hint = (IS_DATE(x)) ? STRING_HINT : NUMBER_HINT;
  return (hint == NUMBER_HINT) ? DefaultNumber(x) : DefaultString(x);
}

// ECMA-262, section 8.6.2.6, page 28.
function DefaultNumber(x) {  
  if (!IS_SYMBOL_WRAPPER(x)) {
    var valueOf = x.valueOf;
    if (IS_SPEC_FUNCTION(valueOf)) {
      var v = %_CallFunction(x, valueOf);
      if (IsPrimitive(v)) return v;
    }

    var toString = x.toString;
    if (IS_SPEC_FUNCTION(toString)) {
      var s = %_CallFunction(x, toString);
      if (IsPrimitive(s)) return s;
    }
  }
  throw MakeTypeError(kCannotConvertToPrimitive);
}

// ECMA-262, section 8.6.2.6, page 28.
function DefaultString(x) {  
  if (!IS_SYMBOL_WRAPPER(x)) {
    var toString = x.toString;
    if (IS_SPEC_FUNCTION(toString)) {
      var s = %_CallFunction(x, toString);
      if (IsPrimitive(s)) return s;
    }

    var valueOf = x.valueOf;
    if (IS_SPEC_FUNCTION(valueOf)) {
      var v = %_CallFunction(x, valueOf);
      if (IsPrimitive(v)) return v;
    }
  }
  throw MakeTypeError(kCannotConvertToPrimitive);
}
```

上面代码的逻辑是这样的：

1. 如果变量为字符串，直接返回.
2. 如果`!IS_SPEC_OBJECT(x)`，直接返回.
3. 如果`IS_SYMBOL_WRAPPER(x)`，则抛出异常.
4. 否则会根据传入的`hint`来调用`DefaultNumber`和`DefaultString`，比如如果为`Date`对象，会调用`DefaultString`.
5. `DefaultNumber`：首`先x.valueOf`，如果为`primitive`，则返回`valueOf`后的值，否则继续调用`x.toString`，如果为`primitive`，则返回`toString`后的值，否则抛出异常
6. `DefaultString`：和`DefaultNumber`正好相反，先调用`toString`，如果不是`primitive`再调用`valueOf`.

那讲了实现原理，这个`ToPrimitive`有什么用呢？实际很多操作会调用`ToPrimitive`，比如加、相等或比较操。在进行加操作时会将左右操作数转换为`primitive`，然后进行相加。

下面来个实例，({}) + 1（将{}放在括号中是为了内核将其认为一个代码块）会输出啥？可能日常写代码并不会这样写，不过网上出过类似的面试题。

加操作只有左右运算符同时为`String或Number`时会执行对应的`%_StringAdd或%NumberAdd`，下面看下`({}) + 1`内部会经过哪些步骤：

`{}`和`1`首先会调用ToPrimitive
`{}`会走到`DefaultNumber`，首先会调用`valueOf`，返回的是`Object` `{}`，不是primitive类型，从而继续走到`toString`，返回`[object Object]`，是`String`类型
最后加操作，结果为`[object Object]1`
再比如有人问你`[] + 1`输出啥时，你可能知道应该怎么去计算了，先对`[]`调用`ToPrimitive`，返回空字符串，最后结果为"1"。

## 谈谈你对原型链的理解？✨

这个问题关键在于两个点，一个是原型对象是什么，另一个是原型链是如何形成的

### 原型对象

绝大部分的函数(少数内建函数除外)都有一个`prototype`属性,这个属性是原型对象用来创建新对象实例,而所有被创建的对象都会共享原型对象,因此这些对象便可以访问原型对象的属性。

例如`hasOwnProperty()`方法存在于Obejct原型对象中,它便可以被任何对象当做自己的方法使用.

> 用法：`object.hasOwnProperty( propertyName )`

> `hasOwnProperty()`函数的返回值为`Boolean`类型。如果对象`object`具有名称为`propertyName`的属性，则返回`true`，否则返回`false`。

```javascript
 var person = {
    name: "Messi",
    age: 29,
    profession: "football player"
  };
console.log(person.hasOwnProperty("name")); //true
console.log(person.hasOwnProperty("hasOwnProperty")); //false
console.log(Object.prototype.hasOwnProperty("hasOwnProperty")); //true
```

由以上代码可知,`hasOwnProperty()`并不存在于`person`对象中,但是`person`依然可以拥有此方法.

所以`person`对象是如何找到`Object`对象中的方法的呢?靠的是原型链。

### 原型链

原因是每个对象都有 `__proto__` 属性，此属性指向该对象的构造函数的原型。

对象可以通过 `__proto__`与上游的构造函数的原型对象连接起来，而上游的原型对象也有一个`__proto__`，这样就形成了原型链。

> 经典原型链图

![2019-06-15-05-36-59]( https://xiaomuzhu-image.oss-cn-beijing.aliyuncs.com/282ef60fe1dfe60924c6caeaeab6c550.png)

## 如何判断是否是数组？

es6中加入了新的判断方法

```js
if（Array.isArray(value)）{
    return true;
}
```

在考虑兼容性的情况下可以用toString的方法

```js
if(!Array.isArray){
    Array.isArray = function(arg){
        return Object.prototype.toString.call(arg)==='[object Array]'
    }

}

```

## 谈一谈你对this的了解？✨

this的指向不是在编写时确定的,而是在执行时确定的，同时，this不同的指向在于遵循了一定的规则。

首先，在默认情况下，this是指向全局对象的，比如在浏览器就是指向window。

```js
name = "Bale";

function sayName () {
    console.log(this.name);
};

sayName(); //"Bale"
```

其次，如果函数被调用的位置存在上下文对象时，那么函数是被隐式绑定的。

```js
function f() {
    console.log( this.name );
}

var obj = {
    name: "Messi",
    f: f
};

obj.f(); //被调用的位置恰好被对象obj拥有，因此结果是Messi
```

再次，显示改变this指向，常见的方法就是call、apply、bind

以bind为例:

```js
function f() {
    console.log( this.name );
}
var obj = {
    name: "Messi",
};

var obj1 = {
     name: "Bale"
};

f.bind(obj)(); //Messi ,由于bind将obj绑定到f函数上后返回一个新函数,因此需要再在后面加上括号进行执行,这是bind与apply和call的区别

```

最后，也是优先级最高的绑定 new 绑定。

用 new 调用一个构造函数，会创建一个新对象, 在创造这个新对象的过程中,新对象会自动绑定到Person对象的this上，那么 this 自然就指向这个新对象。

```js
function Person(name) {
  this.name = name;
  console.log(name);
}

var person1 = new Person('Messi'); //Messi
```

> 绑定优先级:  new绑定 > 显式绑定 >隐式绑定 >默认绑定

## 那么箭头函数的this指向哪里？✨

箭头函数不同于传统JavaScript中的函数,箭头函数并没有属于自己的this,它的所谓的this是捕获其所在上下文的 this 值，作为自己的 this 值,并且由于没有属于自己的this,而箭头函数是不会被new调用的，这个所谓的this也不会被改变.

我们可以用Babel理解一下箭头函数:

```js
// ES6
const obj = {
    getArrow() {
        return () => {
            console.log(this === obj);
        };
    }
} 
```

转化后

```js
// ES5，由 Babel 转译
var obj = {
    getArrow: function getArrow() {
        var _this = this;
        return function () {
            console.log(_this === obj);
        };
    }
};
```

## async/await是什么？

async 函数，就是 Generator 函数的语法糖，它建立在Promises上，并且与所有现有的基于Promise的API兼容。

1. Async—声明一个异步函数(async function someName(){...})

* 自动将常规函数转换成Promise，返回值也是一个Promise对象
* 只有async函数内部的异步操作执行完，才会执行then方法指定的回调函数
* 异步函数内部可以使用await


2. Await—暂停异步的功能执行(var result = await someAsyncCall();)

* 放置在Promise调用之前，await强制其他代码等待，直到Promise完成并返回结果
* 只能与Promise一起使用，不适用与回调
* 只能在async函数内部使用

## async/await相比于Promise的优势？

* 代码读起来更加同步，Promise虽然摆脱了回调地狱，但是then的链式调用也会带来额外的阅读负担
* Promise传递中间值非常麻烦，而async/await几乎是同步的写法，非常优雅
* 错误处理友好，async/await可以用成熟的try/catch，Promise的错误捕获非常冗余
* 调试友好，Promise的调试很差，由于没有代码块，你不能在一个返回表达式的箭头函数中设置断点，如果你在一个.then代码块中使用调试器的步进(step-over)功能，调试器并不会进入后续的.then代码块，因为调试器只能跟踪同步代码的『每一步』。

## JavaScript的参数是按照什么方式传递的？

### 基本类型传递方式
由于js中存在**复杂类型**和**基本类型**,对于**基本类型**而言,是按值传递的.

```javascript
var a = 1;
function test(x) {
  x = 10;
  console.log(x);
}
test(a); // 10
console.log(a); // 1
```

虽然在函数`test`中`a`被修改,并没有有影响到
外部`a`的值,基本类型是按值传递的.

### 复杂类型按引用传递? 

我们将外部`a`作为一个对象传入`test`函数.

```javascript
var a = {
  a: 1,
  b: 2
};
function test(x) {
  x.a = 10;
  console.log(x);
}
test(a); // { a: 10, b: 2 }
console.log(a); // { a: 10, b: 2 }

```

可以看到,在函数体内被修改的`a`对象也同时影响到了外部的`a`对象,可见复杂类型是按**引用传递的**.

可是如果再做一个实验:

```javascript
var a = {
  a: 1,
  b: 2
};
function test(x) {
  x = 10;
  console.log(x);
}
test(a); // 10
console.log(a); // { a: 1, b: 2 }
```

外部的`a`并没有被修改,如果是按引用传递的话,由于共享同一个堆内存,`a`在外部也会表现为`10`才对.
此时的复杂类型同时表现出了`按值传递`和`按引用传递`的特性.

### 按共享传递

复杂类型之所以会产生这种特性,原因就是在传递过程中,对象`a`先产生了一个`副本a`,这个`副本a`并不是深克隆得到的`副本a`,`副本a`地址同样指向对象`a`指向的堆内存.

![](http://omrbgpqyl.bkt.clouddn.com/17-8-31/72507393.jpg)

因此在函数体中修改`x=10`只是修改了`副本a`,`a`对象没有变化.
但是如果修改了`x.a=10`是修改了两者指向的同一堆内存,此时对象`a`也会受到影响.

有人讲这种特性叫做**传递引用**,也有一种说法叫做**按共享传递**.

## 聊一聊如何在JavaScript中实现不可变对象？

实现不可变数据有三种主流的方法

1. 深克隆，但是深克隆的性能非常差，不适合大规模使用
2. Immutable.js，Immutable.js是自成一体的一套数据结构，性能良好，但是需要学习额外的API
3. immer，利用Proxy特性，无需学习额外的api，性能良好

> 原理详解请移步[实现JavaScript不可变数据](#immuatble)

## JavaScript的基本类型和复杂类型是储存在哪里的？

基本类型储存在栈中，但是一旦被闭包引用则成为常住内存，会储存在内存堆中。

复杂类型会储存在内存堆中。

> 原理解析请移步[JavaScript内存管理](#memory.md)

## 讲讲JavaScript垃圾回收是怎么做的？

此过程比较复杂，请看详细解析。

> 原理解析请移步[JavaScript内存管理](#memory.md)

---

 
