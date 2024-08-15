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

## 为什么会有BigInt的提案

JavaScript中Number.MAX_SAFE_INTEGER表示最大安全数字,计算结果是9007199254740991，即在这个数范围内不会出现精度丢失（小数除外）。

但是一旦超过这个范围，js就会出现计算不准确的情况，这在大数计算的时候不得不依靠一些第三方库进行解决，因此官方提出了BigInt来解决此问题。

## var let const 有什么区别

在JavaScript中，`var`、`let` 和 `const` 是用于声明变量的关键字，它们之间存在一些重要的区别。下面是对这些关键字的详细解释：

### 1. 作用域

- **`var`**：变量声明的作用域是函数级的，即在一个函数内部声明的 `var` 变量在整个函数内部都是可见的。如果在全局作用域中声明，则在整个全局作用域中可见。
- **`let` 和 `const`**：变量声明的作用域是块级的，即在一个块（由 `{}` 包围的代码段）内部声明的 `let` 或 `const` 变量只在该块内部可见。

### 2. 提升

- **`var`**：变量声明会被提升到当前作用域的顶部，但初始化不会被提升。这意味着在声明之前使用 `var` 变量时，它的值默认为 `undefined`。
- **`let` 和 `const`**：声明会被提升到当前作用域的顶部，但在声明之前访问这些变量会导致引用错误。这称为“暂时性死区”（Temporal Dead Zone, TDZ）。

### 3. 变更能力

- **`var`**：可以通过赋值来改变变量的值。
- **`let`**：可以通过赋值来改变变量的值。
- **`const`**：一旦声明，变量的值就不能改变。但是，如果声明的是一个对象或数组，可以修改其属性或元素。

### 4. 重复声明

- **`var`**：可以在同一作用域内重复声明同一个变量名，第二次声明不会引起错误。
- **`let` 和 `const`**：在同一作用域内重复声明同一个变量名会导致语法错误。

### 示例

下面是一些示例来展示这些关键字之间的区别：

#### `var` 示例

```js
console.log(x); // 输出: undefined
var x = 10;
```

#### `let` 示例

```js
console.log(y); // 抛出 ReferenceError: Cannot access 'y' before initialization
let y = 20;
```

#### `const` 示例

```js
console.log(z); // 抛出 ReferenceError: Cannot access 'z' before initialization
const z = 30;
```

#### 块级作用域示例

```js
{
  var x = 10;
  let y = 20;
  const z = 30;
  console.log(x, y, z); // 输出: 10 20 30
}

console.log(x); // 输出: 10
console.log(y); // 抛出 ReferenceError: y is not defined
console.log(z); // 抛出 ReferenceError: z is not defined
```

#### `const` 的变更能力示例

```js
const a = 10;
a = 20; // 抛出 TypeError: Assignment to constant variable.

const b = { value: 10 };
b.value = 20; // 修改对象属性是可以的
console.log(b); // 输出: { value: 20 }
```

### 总结

- **`var`**：函数作用域、提升、可重复声明、可重新赋值。
- **`let`**：块级作用域、提升至暂时性死区、不可重复声明、可重新赋值。
- **`const`**：块级作用域、提升至暂时性死区、不可重复声明、不可重新赋值（但可修改对象属性）。

## JavaScript的参数是按照什么方式传递的

在JavaScript中，参数的传递方式取决于参数的类型。JavaScript有两种基本的数据类型：原始类型（primitive types）和引用类型（reference types）。原始类型直接存储值，而引用类型存储的是指向值的引用。

### 原始类型

原始类型包括 `number`, `string`, `boolean`, `symbol`, `bigint`, `undefined`, 和 `null`。这些类型的数据是按值传递的。

#### 特点：

- 当你将一个原始类型的值传递给函数时，函数内部收到的是这个值的一个副本。
- 在函数内部对原始类型的值所做的任何更改都不会影响到原始值本身。

#### 示例代码：

```js
function updateValue(value) {
    value = 10;
}

let num = 5;
updateValue(num);
console.log(num); // 输出: 5
```

在这个例子中，`num` 的值仍然是 5，尽管我们在 `updateValue` 函数中尝试将其更改为 10。这是因为传递给函数的 `value` 参数是 `num` 的一个副本，对 `value` 的更改不会影响到原始变量 `num`。

### 引用类型

引用类型包括 `object` 和 `array`。这些类型的数据是按引用传递的。

#### 特点：

- 当你将一个引用类型的值传递给函数时，函数内部收到的是指向该值的引用。
- 在函数内部对引用类型的值所做的任何更改都会影响到原始值。

#### 示例代码：

```js
function updateArray(arr) {
    arr.push(3);
}

let numbers = [1, 2];
updateArray(numbers);
console.log(numbers); // 输出: [1, 2, 3]
```

在这个例子中，`numbers` 数组在 `updateArray` 函数内部被修改了。这是因为传递给函数的 `arr` 参数实际上是指向 `numbers` 数组的引用，对 `arr` 的更改会影响到原始数组 `numbers`。

### 总结

- **原始类型**：按值传递。在函数内部对原始类型的值所做的任何更改都不会影响到原始值。
- **引用类型**：按引用传递。在函数内部对引用类型的值所做的任何更改都会影响到原始值。

## JavaScript的基本类型和复杂类型是储存在哪里的

### 基本类型（Primitive Types）

基本类型包括 `number`, `string`, `boolean`, `undefined`, `null`, `symbol`, 和 `bigint`。这些类型的数据直接存储在变量的堆栈内存中。

#### 存储位置

- **堆栈内存**：基本类型的值直接存储在变量所在的堆栈内存中。
- **值传递**：当基本类型的值被传递给函数时，传递的是值的副本，而不是指向值的引用。

#### 示例：

```js
let num = 5;
let anotherNum = num; // 另一个变量接收 num 的值
num = 10;
console.log(anotherNum); // 输出: 5
```

在这个例子中，`anotherNum` 的值没有随着 `num` 的变化而变化，因为它们存储的是独立的值。

### 复杂类型（Reference Types）

复杂类型包括 `object`, `array`, `function` 等。这些类型的数据存储在堆内存中。

#### 存储位置

- **堆内存**：复杂类型的值存储在堆内存中。
- **引用传递**：当复杂类型的值被传递给函数时，传递的是指向该值的引用，而不是值本身。

#### 示例：

```js
let obj = { name: "Alice" };
let anotherObj = obj; // 另一个变量接收 obj 的引用
obj.name = "Bob";
console.log(anotherObj.name); // 输出: Bob
```

在这个例子中，`anotherObj` 的 `name` 属性随着 `obj` 的变化而变化，因为它们指向同一个对象。

### 内存分配

- **堆栈内存**：用于存储基本类型的值和复杂类型的引用。
- **堆内存**：用于存储复杂类型的值（即对象本身）。

### 内存管理

JavaScript 的内存管理是由垃圾回收机制自动完成的。当一个变量不再被引用时，垃圾回收器会自动释放相应的内存空间。

- **基本类型**：当一个基本类型的变量不再被引用时，它占用的内存会被垃圾回收器回收。
- **复杂类型**：当一个对象不再被任何变量引用时，它占用的内存会被垃圾回收器回收。

### 总结

- 基本类型：
  - 存储在堆栈内存中。
  - 值传递。
- 复杂类型：
  - 存储在堆内存中。
  - 引用传递。

> 原理解析请移步[JavaScript内存管理](#memory.md)

## ==和===有什么区别

在JavaScript中，`==`（相等运算符）和 `===`（严格相等运算符）用于比较两个值是否相等，但它们的比较方式有所不同。

### `==`（相等运算符）

`==` 运算符执行类型转换，也就是说，如果两边的值不是相同类型，它会尝试将它们转换为相同的类型，然后再进行比较。

#### 特点：

- **类型转换**：如果两边的值类型不同，`==` 会尝试将它们转换为相同类型后再比较。
- **比较结果**：如果转换后的值相等，则返回 `true`；否则返回 `false`。

#### 示例：

```js
console.log(1 == '1'); // 输出: true
console.log(true == 1); // 输出: true
console.log(null == undefined); // 输出: true
console.log(0 == false); // 输出: true
```

### `===`（严格相等运算符）

`===` 运算符不执行类型转换，它要求两边的值不仅要值相等，而且类型也要相同。

#### 特点：

- **不执行类型转换**：如果两边的值类型不同，则直接返回 `false`。
- **比较结果**：如果值相等且类型相同，则返回 `true`；否则返回 `false`。

#### 示例：

```js
console.log(1 === '1'); // 输出: false
console.log(true === 1); // 输出: false
console.log(null === undefined); // 输出: false
console.log(0 === false); // 输出: false
```

### 总结

- **`==` 运算符**：执行类型转换，比较转换后的值。
- **`===` 运算符**：不执行类型转换，比较值和类型。

### 使用建议

- **推荐使用 `===`**：通常推荐使用 `===` 运算符，因为它避免了意外的类型转换带来的错误。
- **特殊情况**：在某些情况下，如果明确需要类型转换，可以使用 `==`。

### 示例对比

下面是一些具体的比较示例来展示 `==` 和 `===` 的区别：

#### 类型转换示例

```js
console.log(1 == '1'); // 输出: true
console.log(1 === '1'); // 输出: false
```

#### 类型不匹配示例

```js
console.log(1 == true); // 输出: true （`true` 被转换为 `1`）
console.log(1 === true); // 输出: false
```

#### 布尔值和数字示例

```js
console.log(false == 0); // 输出: true
console.log(false === 0); // 输出: false
```

#### 空值示例

```js
console.log(null == undefined); // 输出: true
console.log(null === undefined); // 输出: false
```

### 总结

- **`==`**：执行类型转换，比较转换后的值。
- **`===`**：不执行类型转换，比较值和类型。

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

## 自定义属性的读写

### 1. 使用 `Object.defineProperty()`

`Object.defineProperty()` 方法可以用来定义属性的 getter 和 setter。这允许你对属性的读写操作进行更细粒度的控制。

**示例：**

```js
const person = {};

Object.defineProperty(person, 'name', {
    get: function() {
        return this._name;
    },
    set: function(newValue) {
        if (newValue.length > 0) {
            this._name = newValue;
        } else {
            console.log("Name cannot be empty.");
        }
    },
    enumerable: true, // 是否可以枚举
    configurable: true // 是否可以配置
});

// 设置属性
person.name = "Alice"; // 设置 name 为 "Alice"

// 读取属性
console.log(person.name); // 输出: Alice

// 尝试设置空字符串
person.name = ""; // 输出: Name cannot be empty.
```

### 2. 使用 ES6 的 getter 和 setter

ES6 引入了更为简洁的语法来定义 getter 和 setter。

**示例：**

```js
const person = {
    _name: "",

    get name() {
        return this._name;
    },

    set name(newValue) {
        if (newValue.length > 0) {
            this._name = newValue;
        } else {
            console.log("Name cannot be empty.");
        }
    }
};

// 设置属性
person.name = "Alice"; // 设置 name 为 "Alice"

// 读取属性
console.log(person.name); // 输出: Alice

// 尝试设置空字符串
person.name = ""; // 输出: Name cannot be empty.
```

### 3. 使用类和私有字段

在ES6中，还可以使用类和私有字段来实现自定义属性的读写。

**示例：**

```js
class Person {
    constructor(name) {
        this._name = name;
    }

    get name() {
        return this._name;
    }

    set name(newValue) {
        if (newValue.length > 0) {
            this._name = newValue;
        } else {
            console.log("Name cannot be empty.");
        }
    }
}

const person = new Person("Alice");

// 读取属性
console.log(person.name); // 输出: Alice

// 尝试设置空字符串
person.name = ""; // 输出: Name cannot be empty.
```

### 总结

- **`Object.defineProperty()`**：可以定义属性的 getter 和 setter，提供更细粒度的控制。
- **ES6 getter 和 setter**：提供简洁的语法来定义 getter 和 setter。
- **类和私有字段**：在类中使用私有字段来封装数据，并通过 getter 和 setter 控制访问。

## 介绍一下DOM对象模型

DOM (Document Object Model) 是一种处理 XML 或 HTML 文档的标准规范。它定义了一种方式，使得程序可以读取和修改文档结构、内容和样式。DOM 规范由 W3C (World Wide Web Consortium) 维护，并被广泛应用于浏览器中的网页开发。

### DOM 的基本概念

- **节点** (Node)：在 DOM 中，文档被视为节点树，其中每个节点代表文档的一个组成部分。
- **元素节点** (Element Node)：文档中的标签，例如 `<div>` 或 `<p>`。
- **文本节点** (Text Node)：标签内的文本。
- **属性节点** (Attribute Node)：元素节点的属性，例如 `href` 或 `class`。
- **文档节点** (Document Node)：整个文档本身，通常称为 `document` 对象。
- **注释节点** (Comment Node)：文档中的注释。

### DOM 的核心功能

- **读取和修改内容**：可以获取或更改文档中的任何内容。
- **创建和删除元素**：可以动态地添加新的元素或删除现有元素。
- **查找节点**：可以遍历节点树来查找特定的节点。
- **事件处理**：可以监听和响应用户或浏览器的事件，如点击、键盘输入等。
- **CSS 样式**：可以通过 JavaScript 操作元素的样式。

### DOM 的主要对象

以下是 DOM 中一些常见的对象及其方法：

#### `document` 对象

- **`document.createElement(tagName)`**：创建一个新的元素节点。
- **`document.createTextNode(text)`**：创建一个新的文本节点。
- **`document.querySelector(selector)`**：返回匹配给定 CSS 选择器的第一个元素。
- **`document.querySelectorAll(selector)`**：返回所有匹配给定 CSS 选择器的元素集合。
- **`document.getElementById(id)`**：返回具有指定 ID 的元素。

#### 元素节点对象

- **`element.appendChild(child)`**：向元素末尾添加子节点。
- **`element.insertBefore(newChild, referenceChild)`**：在给定的参考节点之前插入新的子节点。
- **`element.removeChild(child)`**：移除指定的子节点。
- **`element.replaceChild(newChild, oldChild)`**：替换指定的子节点。
- **`element.innerHTML`**：获取或设置元素的 HTML 内容。
- **`element.textContent`**：获取或设置元素的纯文本内容。
- **`element.style`**：访问元素的内联样式。
- **`element.getAttribute(name)`**：获取指定属性的值。
- **`element.setAttribute(name, value)`**：设置或更改属性值。
- **`element.removeAttribute(name)`**：移除属性。

**示例**

下面是一个简单的示例，展示如何使用 DOM 来操作页面上的元素：

```js
// 获取文档中的元素
const header = document.getElementById('header');
const content = document.querySelector('.content');

// 修改元素内容
header.textContent = '这是一个标题';

// 添加新元素
const newParagraph = document.createElement('p');
newParagraph.textContent = '这是新添加的一段文字。';
content.appendChild(newParagraph);

// 添加样式
newParagraph.style.color = 'red';
newParagraph.style.fontSize = '16px';

// 添加事件监听器
newParagraph.addEventListener('click', function(event) {
    alert('你点击了这个段落！');
});
```

### 注意事项

- **性能问题**：频繁地操作 DOM 可能会导致性能下降，特别是在移动设备上。
- **异步操作**：在现代前端开发中，异步数据加载和更新是非常常见的，这通常需要与 AJAX 或 Fetch API 结合使用。
- **框架支持**：许多现代 JavaScript 框架（如 React、Vue 和 Angular）提供了对 DOM 操作的抽象层，简化了开发过程。

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

## 解释一下什么是JSONP

JSONP（JSON with Padding）是一种跨域数据请求的技术，主要用于解决Web开发中跨域资源共享（CORS）的问题。JSONP 不是 JSON 的一部分，而是另一种用于跨域数据传输的技术。

### JSONP 的工作原理

JSONP 的工作原理基于 `<script>` 标签的特性，即可以跨域加载脚本文件。这使得JSONP可以绕过同源策略的限制，从而实现跨域数据请求。

#### 步骤如下：

1. **客户端发送请求**：
   - 客户端生成一个唯一的函数名。
   - 构建一个URL，该URL包含服务器端需要知道的函数名作为查询参数，并且这个URL通过 `<script>` 标签加载。
2. **服务器响应**：
   - 服务器接收到请求，并从中提取客户端提供的函数名。
   - 服务器返回一个JavaScript函数调用，函数体包含所需的数据。
   - 数据以JSON格式包装在函数调用内。
3. **客户端执行**：
   - 当 `<script>` 标签加载完成后，浏览器会执行该脚本。
   - 脚本执行客户端预先定义的函数，并传入服务器返回的数据作为参数。
   - 客户端处理这些数据，并执行相应的业务逻辑。

### 示例代码

下面是一个简单的JSONP示例，展示如何从服务器端获取数据：

#### 客户端代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>JSONP Example</title>
</head>
<body>
    <script>
        function handleResponse(data) {
            console.log("Received data:", data);
        }

        const script = document.createElement('script');
        script.src = 'https://example.com/data?callback=handleResponse';
        document.head.appendChild(script);
    </script>
</body>
</html>
```

#### 服务器端代码（示例）：

```js
// 假设服务器端使用 Node.js 和 Express
const express = require('express');
const app = express();
const port = 3000;

app.get('/data', (req, res) => {
    const callback = req.query.callback;
    const data = { name: "John Doe", age: 30 };
    res.type('application/javascript');
    res.send(`${callback}(${JSON.stringify(data)});`);
});

app.listen(port, () => {
    console.log(`Server listening at http://localhost:${port}`);
});
```

### JSONP 的限制

- **安全性**：JSONP 不支持HTTPS，因此可能存在中间人攻击的风险。
- **数据类型**：JSONP 只能通过GET请求获取数据，因此不适合大量数据的传输。
- **CORS支持**：随着CORS的支持越来越普遍，许多现代浏览器和服务器都支持CORS，这使得JSONP的使用越来越少。

### 总结

- **JSONP** 是一种用于实现跨域数据请求的技术。
- **工作原理**：基于 `<script>` 标签可以跨域加载脚本文件的特性。
- **步骤**：客户端通过 `<script>` 标签发送请求，服务器响应包含JSON数据的函数调用，客户端执行该函数并处理数据。
- **限制**：安全性、数据类型限制以及CORS支持。

## document.write 和 innerHtml 的区别

`document.write()` 和 `innerHTML` 是JavaScript中用于操作HTML文档的不同方法。它们各自有不同的用途和特点。

### `document.write()`

`document.write()` 是一个全局方法，用于将文本写入当前文档流。它可以用来动态生成HTML页面内容。

#### 特点：

- **重写文档**：如果在文档加载完成后使用 `document.write()`，它会重写整个文档的内容。
- **文档流**：`document.write()` 的输出被视为文档的一部分，就像直接写入HTML文件一样。
- **只能在文档加载过程中使用**：一旦文档加载完成，使用 `document.write()` 会重写整个文档，这可能会导致页面刷新。

#### 示例：

```js
document.write("<h1>Hello, World!</h1>");
document.write("<p>Welcome to my website.</p>");
```

### `innerHTML`

`innerHTML` 是一个属性，用于获取或设置一个元素的HTML内容。它可以用来修改页面上的任何元素的内容。

#### 特点：

- **局部更新**：`innerHTML` 可以用来更新页面上特定元素的内容，而不会影响其他部分。
- **安全性**：由于 `innerHTML` 会解析HTML，因此在设置时需要小心，以避免XSS（跨站脚本）攻击。
- **动态更新**：可以在任何时候使用 `innerHTML` 更新页面内容，不会导致整个页面的重写。

#### 示例：

```js
const container = document.getElementById("container");

container.innerHTML = "<h1>Hello, World!</h1>";
container.innerHTML += "<p>Welcome to my website.</p>";
```

### 区别总结

- **`document.write()`**：
  - 用于将文本写入当前文档流。
  - 会在文档加载过程中重写整个文档。
  - 只能在文档加载过程中使用，否则会重写整个文档。
- **`innerHTML`**：
  - 用于获取或设置一个元素的HTML内容。
  - 可以局部更新页面上的元素内容。
  - 可以在任何时候使用，不会重写整个文档。

### 使用场景

- **使用 `document.write()`**：
  - 通常在页面加载时使用，用于动态生成页面内容。
  - 不建议在页面加载完成后使用，因为这会重写整个文档。
- **使用 `innerHTML`**：
  - 用于局部更新页面内容。
  - 适合在页面交互中动态更新页面元素。

### 总结

- **`document.write()`** 用于重写文档内容，通常在文档加载过程中使用。
- **`innerHTML`** 用于局部更新页面上的元素内容，可以在任何时候使用。

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

## 数组去重的方法

### 1. 使用 Set

`Set` 是ES6引入的一种数据结构，它只允许存储唯一的值。可以利用 `Set` 的特性轻松地去除数组中的重复项。

**示例：**

```js
const array = [1, 2, 2, 3, 4, 4, 5];

const uniqueArray = [...new Set(array)];

console.log(uniqueArray); // 输出: [1, 2, 3, 4, 5]
```

### 2. 使用 Filter

`filter()` 方法可以用来过滤数组中的元素。结合 `indexOf()` 或 `lastIndexOf()` 可以去除重复项。

**示例：**

```js
const array = [1, 2, 2, 3, 4, 4, 5];

const uniqueArray = array.filter((value, index, self) => {
    return self.indexOf(value) === index;
});

console.log(uniqueArray); // 输出: [1, 2, 3, 4, 5]
```

### 3. 使用 Map

`Map` 是另一种ES6引入的数据结构，它可以存储任意类型的键和值。可以利用 `Map` 来追踪已出现过的元素。

**示例：**

```js
const array = [1, 2, 2, 3, 4, 4, 5];

const map = new Map();
const uniqueArray = array.filter(item => !map.has(item) && map.set(item, 1));

console.log(uniqueArray); // 输出: [1, 2, 3, 4, 5]
```

### 4. 使用 Reduce

`reduce()` 方法可以用来累积数组中的值。可以累积一个对象，用来记录每个元素是否出现过。

**示例：**

```js
const array = [1, 2, 2, 3, 4, 4, 5];

const uniqueArray = array.reduce((accumulator, currentValue) => {
    if (!accumulator.includes(currentValue)) {
        accumulator.push(currentValue);
    }
    return accumulator;
}, []);

console.log(uniqueArray); // 输出: [1, 2, 3, 4, 5]
```

### 5. 使用 For Loop

可以使用普通的 `for` 循环来迭代数组，并检查每个元素是否已经存在于结果数组中。

**示例：**

```js
const array = [1, 2, 2, 3, 4, 4, 5];

const uniqueArray = [];
for (const item of array) {
    if (!uniqueArray.includes(item)) {
        uniqueArray.push(item);
    }
}

console.log(uniqueArray); // 输出: [1, 2, 3, 4, 5]
```

### 6. 使用 ES6 的 Array.from 和 Set

`Array.from()` 可以将一个类数组对象或可迭代对象转换为真正的数组。结合 `Set` 可以快速去重。

**示例：**

```js
const array = [1, 2, 2, 3, 4, 4, 5];

const uniqueArray = Array.from(new Set(array));

console.log(uniqueArray); // 输出: [1, 2, 3, 4, 5]
```

### 7. 使用 ES6 的 Spread Operator 和 Set

ES6 的扩展运算符 (`...`) 可以将 `Set` 转换回数组。

#### 示例：

```js
const array = [1, 2, 2, 3, 4, 4, 5];

const uniqueArray = [...new Set(array)];

console.log(uniqueArray); // 输出: [1, 2, 3, 4, 5]
```

### 总结

- **使用 `Set`**：最简单直接的方法，适用于ES6及以上版本。
- **使用 `filter()`**：适用于需要兼容旧版浏览器的情况。
- **使用 `Map`**：适用于需要额外信息或复杂条件的情况。
- **使用 `reduce()`**：适用于需要累积结果的情况。
- **使用 `for` 循环**：适用于需要完全控制流程的情况。
- **使用 `Array.from` 和 `Set`**：适用于需要将类数组对象转换为数组的情况。
- **使用扩展运算符和 `Set`**：简洁明了，适用于ES6及以上版本。

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

## 事件冒泡和事件捕捉有什么区别

事件冒泡（Event Bubbling）和事件捕捉（Event Capturing）是描述DOM事件传播路径的两种机制。这两种机制决定了事件是如何从触发事件的元素传播到文档树的其他元素上的。

### 事件冒泡

事件冒泡是从最具体的元素（即事件发生的元素）开始，然后向上逐层传播到最不具体的元素（通常是 `document` 对象）。这是JavaScript中默认的事件传播方式。

#### 特点

- **自下而上**：事件从触发事件的元素开始，然后沿着DOM树向上传播。
- **默认行为**：大多数浏览器默认采用事件冒泡机制。
- **处理时机**：在事件冒泡过程中，可以处理事件。

#### 示例

假设有一个嵌套的元素结构如下：

```js
<div id="outer">
  <div id="inner">Click me!</div>
</div>
```

```js
document.getElementById('outer').addEventListener('click', function(event) {
  console.log('Outer div clicked');
}, false);

document.getElementById('inner').addEventListener('click', function(event) {
  console.log('Inner div clicked');
}, false);
```

当点击内部的 `div` 时，输出顺序将是：

1. `Inner div clicked`
2. `Outer div clicked`

### 事件捕捉

事件捕捉是从最不具体的元素（通常是 `document` 对象）开始，然后向下逐层传播到最具体的元素（即事件发生的元素）。这是一种不太常见的事件传播方式。

#### 特点

- **自上而下**：事件从 `document` 开始，沿着DOM树向下传播。
- **处理时机**：在事件捕捉过程中，可以处理事件。
- **较少使用**：与事件冒泡相比，事件捕捉较少被使用。

#### 示例

假设同样的嵌套元素结构，使用事件捕捉处理事件：

```js
document.getElementById('outer').addEventListener('click', function(event) {
  console.log('Outer div captured');
}, true);

document.getElementById('inner').addEventListener('click', function(event) {
  console.log('Inner div captured');
}, true);
```

当点击内部的 `div` 时，输出顺序将是：

1. `Document captured` (实际上是在事件到达 `outer` 之前发生的)
2. `Outer div captured`
3. `Inner div captured`

### 如何使用

在添加事件监听器时，可以通过第三个参数 `useCapture` 来指定是否使用事件捕捉。默认情况下，该参数为 `false`，表示使用事件冒泡。如果设置为 `true`，则表示使用事件捕捉。

#### 示例

```js
element.addEventListener('click', function(event) {
  console.log('Event handled');
}, true); // 使用事件捕捉
```

### 事件阻止

- **事件阻止冒泡**：可以使用 `event.stopPropagation()` 方法来阻止事件继续向上冒泡。
- **事件阻止默认行为**：可以使用 `event.preventDefault()` 方法来阻止事件的默认行为。

### 总结

- **事件冒泡**：事件从触发事件的元素开始向上传播。
- **事件捕捉**：事件从 `document` 开始向下传播。
- **默认行为**：事件冒泡是默认的事件传播方式。
- **使用场景**：事件捕捉通常用于需要在事件到达目标元素之前进行处理的情况。

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

## 宏任务和微任务都是怎样执行的

在JavaScript中，宏任务（Macro Tasks）和微任务（Micro Tasks）是指事件循环（Event Loop）中的两种不同类型的任务。它们在JavaScript引擎中以不同的顺序执行，这对于理解异步代码的行为至关重要。

### 宏任务（Macro Tasks）

宏任务通常是JavaScript执行的基本单位，包括同步代码块、定时器、I/O 操作等。宏任务通常会阻塞事件循环，直到任务完成。

#### 宏任务的例子

- **全局执行上下文**：程序的入口点。
- **定时器**：如 `setTimeout` 和 `setInterval`。
- **I/O 操作**：如文件读写。
- **UI 渲染**：浏览器的渲染任务。

### 微任务（Micro Tasks）

微任务是指那些在当前宏任务执行结束后、下一个宏任务执行之前必须完成的任务。微任务优先级高于宏任务，除了当前宏任务外，它们总是优先执行。

#### 微任务的例子

- **Promise**：当 Promise 的状态改变时，其 `.then()`、`.catch()` 和 `.finally()` 回调会被添加到微任务队列。
- **Mutation Observers**：用于观察 DOM 变更。
- **Process.nextTick**：Node.js 中的一个特性，用于立即执行回调。

### 执行顺序

1. **执行宏任务**：JavaScript 引擎首先执行宏任务，直到宏任务队列中的所有任务都被处理完。
2. **处理微任务**：在当前宏任务结束之后，JavaScript 引擎会处理所有微任务队列中的任务。这意味着在宏任务结束之后，所有微任务都会被立即执行。
3. **重复**：处理完所有微任务后，事件循环会回到宏任务队列，处理下一个宏任务。

### 示例

下面是一个示例，展示了宏任务和微任务是如何在事件循环中执行的。

```js
console.log('Start');

setTimeout(() => {
  console.log('Timeout');
}, 0);

Promise.resolve().then(() => {
  console.log('Promise');
});

process.nextTick(() => {
  console.log('Next Tick');
});

console.log('End');
```

### 输出顺序

1. **宏任务**：执行同步代码和 `setTimeout`。
2. **微任务**：执行 `Promise` 和 `process.nextTick`。
3. **宏任务**：如果有更多宏任务，继续执行。

### 输出解释

- **Start**：同步代码首先执行。
- **End**：同步代码执行完毕。
- **Promise**：`Promise` 的 `.then()` 回调被添加到微任务队列。
- **Next Tick**：`process.nextTick` 的回调被添加到微任务队列。
- **Timeout**：`setTimeout` 的回调被添加到宏任务队列，在所有微任务执行完毕后执行。

### 总结

- **宏任务**：同步代码、定时器、I/O 操作等。
- **微任务**：`Promise`、`Mutation Observers`、`process.nextTick` 等。
- **执行顺序**：宏任务 → 微任务 → 下一个宏任务。

## 什么是执行栈

执行栈（Execution Stack），也被称为调用栈（Call Stack），是JavaScript运行时的重要概念之一。它是JavaScript引擎用来跟踪函数调用顺序和管理函数上下文的数据结构。执行栈负责保存函数调用时的信息，如函数的局部变量、参数以及返回地址等。每当函数被调用时，执行栈就会为该函数创建一个新的栈帧（Stack Frame），并将这个栈帧压入栈顶。当函数执行完毕后，对应的栈帧会被弹出栈顶。

### 执行栈的主要职责

- **保存函数调用的信息**：每当一个函数被调用时，执行栈会创建一个栈帧，用于保存函数的局部变量、参数、返回地址等信息。
- **管理函数调用的顺序**：执行栈按照后进先出的原则管理函数调用，确保函数能够按照正确的顺序执行和返回。
- **控制程序执行流程**：执行栈决定了JavaScript程序的执行流程，保证了函数的正确执行和返回。

### 执行栈的工作流程

1. **主执行上下文**：当JavaScript程序开始执行时，首先创建一个全局执行上下文（Global Execution Context），这个上下文对应着程序的全局作用域，并且会自动被压入执行栈的底部。
2. **函数调用**：当遇到函数调用时，JavaScript引擎会为这个函数创建一个新的执行上下文，并将其压入执行栈的顶部。
3. 执行上下文的生命周期：
   - **创建阶段**：在函数调用前，创建执行上下文，并初始化相关变量和作用域链。
   - **执行阶段**：函数开始执行，局部变量和参数被赋值。
   - **销毁阶段**：函数执行完毕后，执行上下文被销毁，对应的栈帧从执行栈中弹出。
4. **函数返回**：当函数执行完毕并返回时，它的执行上下文会被销毁，对应的栈帧从执行栈中弹出。

### 示例

下面是一个简单的JavaScript程序，展示了执行栈的工作流程：

```js
function outerFunction() {
    console.log("outerFunction called");

    function innerFunction() {
        console.log("innerFunction called");
    }

    innerFunction();
}

outerFunction();
```

### 执行流程分析

1. **全局执行上下文**：程序启动时，创建全局执行上下文，并将其压入执行栈。
2. **`outerFunction` 调用**：遇到 `outerFunction` 调用，创建 `outerFunction` 的执行上下文，并将其压入执行栈。
3. **`innerFunction` 调用**：在 `outerFunction` 内部调用 `innerFunction`，创建 `innerFunction` 的执行上下文，并将其压入执行栈。
4. **`innerFunction` 返回**：`innerFunction` 执行完毕，其执行上下文被销毁，对应的栈帧从执行栈中弹出。
5. **`outerFunction` 返回**：`outerFunction` 执行完毕，其执行上下文被销毁，对应的栈帧从执行栈中弹出。
6. **全局执行上下文销毁**：程序执行完毕，全局执行上下文被销毁。

### 总结

- **执行栈**：用于跟踪函数调用顺序和管理函数上下文的数据结构。
- **栈帧**：每个函数调用时都会创建一个栈帧，用于保存函数的信息。
- **工作流程**：创建执行上下文、执行函数、销毁执行上下文。

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

ES6模块（ECMAScript 2015 模块）和 CommonJS 模块是 JavaScript 中两种不同的模块化编程方案。它们各有特点，并在不同的环境中被广泛使用。下面我将详细介绍它们之间的主要区别：

### 1. 导入和导出语法

- **ES6 模块**：

  - 使用 `import` 语句导入模块。
  - 使用 `export` 语句导出模块。
  - 可以使用 `export default` 来导出一个默认的导出项。

  示例：

  ```js
  // myModule.js
  export const myFunction = () => {
      console.log("Hello from myModule!");
  };
  
  export default function anotherFunction() {
      console.log("Another function in myModule!");
  }
  
  // app.js
  import { myFunction } from './myModule';
  import defaultFunction from './myModule'; // 或者 import anotherFunction from './myModule';
  
  myFunction();
  defaultFunction();
  ```

- **CommonJS 模块**：

  - 使用 `require` 函数导入模块。
  - 使用 `module.exports` 或 `exports` 导出模块。

  示例：

  ```js
  // myModule.js
  const myFunction = () => {
      console.log("Hello from myModule!");
  };
  
  module.exports = {
      myFunction,
      anotherFunction: function() {
          console.log("Another function in myModule!");
      }
  };
  
  // app.js
  const myModule = require('./myModule');
  
  myModule.myFunction();
  myModule.anotherFunction();
  ```

### 2. 执行时机

- **ES6 模块**：
  - 导入语句在编译阶段被解析，这意味着所有导入的模块都会在执行任何代码之前被加载。
  - 导入的模块在第一次加载时会被缓存，后续的导入请求会从缓存中获取模块。
- **CommonJS 模块**：
  - 导入语句在运行时动态加载模块。
  - 每次导入都会执行模块代码，这意味着如果模块中有副作用（如日志记录或网络请求），每次导入都会重新执行这些副作用。

### 3. 动态导入

- **ES6 模块** 支持动态导入，可以使用 `import()` 表达式按需加载模块。

  ```js
  import('./myModule').then(myModule => {
      myModule.default(); // 调用默认导出
  });
  ```

- **CommonJS 模块** 不支持动态导入，但可以使用 `require` 异步加载模块，例如使用 `require.ensure`（已废弃）。

### 4. 循环引用

- **ES6 模块**：
  - 不允许循环引用，即模块 A 不能同时依赖模块 B，而模块 B 也不能依赖模块 A。
- **CommonJS 模块**：
  - 允许循环引用，因为模块在运行时加载，可以先加载一部分代码然后再加载另一部分。

### 5. 运行环境

- **ES6 模块**：
  - 在现代浏览器和 Node.js v12.0.0 及更高版本中得到支持。
  - 在旧版浏览器中需要使用转译工具（如 Babel）将 ES6 模块转换为 CommonJS 或其他格式。
- **CommonJS 模块**：
  - 主要在 Node.js 环境中使用。
  - 不被浏览器原生支持，但在 Node.js 中广泛使用。

### 6. 性能

- **ES6 模块**：
  - 由于在编译阶段解析，ES6 模块可以优化加载顺序，减少不必要的加载。
  - 支持 Tree-shaking，这意味着未使用的导出不会被包含在最终的打包文件中。
- **CommonJS 模块**：
  - 由于在运行时加载，可能导致额外的运行时开销。

### 总结

- **ES6 模块** 是现代 JavaScript 的标准模块化方案，提供更简洁的语法和更好的性能优化。
- **CommonJS 模块** 是 Node.js 的默认模块化方案，提供了更多的灵活性，但在现代开发实践中逐渐被 ES6 模块取代。

选择使用哪种模块化方案取决于你的项目需求和运行环境。如果你正在开发一个现代的前端项目，建议使用 ES6 模块。如果你正在开发一个 Node.js 项目，可以选择 ES6 模块，因为它们已经在 Node.js 中得到很好的支持。如果你需要向后兼容旧版本的 Node.js，你可能还需要使用 CommonJS 模块。

> 详解请移步[ES6模块与CommonJS模块的差异](http://es6.ruanyifeng.com/#docs/module-loader#ES6-%E6%A8%A1%E5%9D%97%E4%B8%8E-CommonJS-%E6%A8%A1%E5%9D%97%E7%9A%84%E5%B7%AE%E5%BC%82)

## 为什么要使用模块化？都有哪几种方式可以实现模块化，各有什么特点？

模块化是软件开发中一种重要的设计理念，它通过将程序分解成独立的、可复用的单元（称为模块）来提高代码的可维护性和可读性。在JavaScript中，模块化特别重要，因为它有助于管理大型项目的复杂度，并促进了代码的重用。

### 为什么要使用模块化？

1. **代码组织**：模块化有助于将代码组织成逻辑上相关的部分，便于理解和维护。
2. **重用性**：模块化的代码更容易被其他项目重用。
3. **依赖管理**：通过模块化，可以明确地管理每个模块之间的依赖关系。
4. **命名空间**：避免全局命名空间的污染，减少命名冲突的风险。
5. **加载优化**：模块化允许按需加载代码，从而减少初始加载时间和提高性能。
6. **测试性**：模块化的代码更容易进行单元测试。

### JavaScript 中实现模块化的方式

#### 1. CommonJS

- 特点：

  - CommonJS 是服务器端模块系统的一个标准，最初用于 Node.js。
  - 使用 `require` 函数来导入模块，使用 `module.exports` 导出模块。
  - 模块在加载时就立即执行并缓存结果，因此每个模块只执行一次。

- 示例：

  ```js
  // myModule.js
  module.exports = {
    greeting: 'Hello, CommonJS!'
  };
  
  // main.js
  const myModule = require('./myModule');
  console.log(myModule.greeting); // 输出: Hello, CommonJS!
  ```

#### 2. AMD (Asynchronous Module Definition)

- 特点：

  - AMD 是一个前端模块化规范，主要用于浏览器环境。
  - 使用 `define` 函数定义模块，使用 `require` 加载模块。
  - 支持异步加载模块，可以在定义模块时指定依赖。

- 示例：

  ```js
  // 使用 RequireJS
  define(function() {
    return {
      greeting: 'Hello, AMD!'
    };
  });
  
  require(['myModule'], function(myModule) {
    console.log(myModule.greeting); // 输出: Hello, AMD!
  });
  ```

#### 3. ES Modules (ESM)

- 特点：

  - ECMAScript 2015 (ES6) 引入的标准模块系统。
  - 使用 `import` 语句来导入模块，使用 `export` 语句导出模块。
  - 支持动态导入 (`import()` 表达式)。
  - 模块是惰性加载的，只在第一次引用时加载。

- 示例：

  ```js
  // myModule.js
  export const greeting = 'Hello, ES Modules!';
  
  // main.js
  import { greeting } from './myModule';
  console.log(greeting); // 输出: Hello, ES Modules!
  ```

### 各种方式的特点总结

- CommonJS：
  - 适用于服务器端。
  - 同步加载。
  - 每个模块只加载一次。
- AMD：
  - 主要用于浏览器端。
  - 异步加载。
  - 明确指定依赖。
- ES Modules：
  - 标准化的模块系统。
  - 支持动态导入。
  - 惰性加载。
  - 浏览器和 Node.js 支持。

### 选择合适的模块化方式

- **浏览器**：ES Modules 逐渐成为浏览器中的首选，而 AMD 仍然被广泛用于旧的项目。
- **Node.js**：ES Modules 已经成为 Node.js 的默认模块系统，但 CommonJS 仍然被广泛使用。

### 总结

- **模块化**：有助于代码组织、重用、依赖管理和性能优化。
- **CommonJS**：服务器端模块化标准。
- **AMD**：浏览器端模块化规范。
- **ES Modules**：ECMAScript 标准化的模块系统。

## null与undefined的区别是什么

`null` 和 `undefined` 在 JavaScript 中都是原始数据类型，它们各自有自己的用途和含义。下面是 `null` 和 `undefined` 的主要区别：

### 1. 含义

- **`undefined`**：
  - 通常表示一个变量已经被声明但还没有被赋值。
  - 也可以表示一个函数没有返回任何值。
  - 当访问一个不存在的对象属性时，返回 `undefined`。
- **`null`**：
  - 表示一个空值，即没有任何对象值。
  - 常常用来表示一个空的或未定义的对象引用。
  - 可以被赋给变量来表示该变量不指向任何对象。

### 2. 类型

- **`undefined`** 的类型是 `undefined`。
- **`null`** 的类型是 `object`，尽管这在语义上有些奇怪，但这是 JavaScript 的历史遗留问题。

### 3. 使用场景

- **`undefined`**：
  - 当一个变量被声明但没有赋值时，默认值为 `undefined`。
  - 函数如果没有返回任何值，返回值为 `undefined`。
  - 访问对象中不存在的属性时，返回 `undefined`。
- **`null`**：
  - 通常用来表示一个空的或无效的对象引用。
  - 可以被显式地赋给变量，以表示该变量不指向任何对象。
  - 有时用来表示一个预期的对象引用为空的情况。

### 4. 类型检测

- `typeof` 运算符：
  - `typeof undefined` 返回 `"undefined"`。
  - `typeof null` 返回 `"object"`（这是一个历史遗留问题）。

### 5. 严格相等

- `===` 运算符：
  - `undefined === undefined` 返回 `true`。
  - `null === null` 返回 `true`。
  - `null === undefined` 返回 `false`。

### 6. 相等比较

- `==` 运算符：
  - `undefined == undefined` 返回 `true`。
  - `null == null` 返回 `true`。
  - `null == undefined` 返回 `true`，因为它们被认为是相等的。

### 示例

```js
let x;
console.log(x); // 输出: undefined

let y = null;
console.log(y); // 输出: null

console.log(typeof x); // 输出: undefined
console.log(typeof y); // 输出: object

console.log(x === undefined); // 输出: true
console.log(y === null); // 输出: true

console.log(x == y); // 输出: false
console.log(null == undefined); // 输出: true
```

### 总结

- **`undefined`** 通常表示一个变量还没有被赋值，或者一个函数没有返回值。
- **`null`** 通常表示一个变量被显式地赋值为空，或者表示一个对象引用为空。

## 0.1+0.2为什么不等于0.3

在JavaScript中，`0.1 + 0.2` 不等于 `0.3` 是由于浮点数的精度问题。这是因为浮点数在计算机内部是以二进制形式存储的，而某些十进制小数无法精确地表示为二进制小数。

![2019-06-23-09-24-06]( https://xiaomuzhu-image.oss-cn-beijing.aliyuncs.com/b9aa4056155df1baae69d6de5a0ac322.png)

### 为什么会出现这种情况？

在二进制系统中，有些十进制小数不能被准确地表示。例如，十进制中的 `0.1` 和 `0.2` 在二进制中是无限循环小数，因此在计算机中存储时会有舍入误差。

- `0.1` 的二进制表示：
  - `0.1` 的二进制形式是一个无限循环小数，大约为 `0.0001100110011001100...`。
- `0.2` 的二进制表示：
  - `0.2` 的二进制形式也是一个无限循环小数，大约为 `0.001100110011001100...`。

当这两个数相加时，由于舍入误差，结果将不是精确的 `0.3`。

JS 的 `Number` 类型遵循的是 IEEE 754 标准，使用的是 64 位固定长度来表示。

IEEE 754 浮点数由三个域组成，分别为 sign bit (符号位)、exponent bias (指数偏移值) 和 fraction (分数值)。64 位中，sign bit 占 1 位，exponent bias 占 11 位，fraction 占 52 位。

当一个数为正数，sign bit 为 0，当为负数时，sign bit 为 1.

以 0.1 转换为 IEEE 754 标准表示为例解释一下如何求 exponent bias (指数偏移值)  和 fraction (分数值)。转换过程主要经历 3 个过程：

1. 将 0.1 转换为二进制表示
1. 将转换后的二进制通过科学计数法表示
1. 将通过科学计数法表示的二进制转换为 IEEE 754 标准表示

#### 1、将 0.1 转换为二进制表示

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

#### 2、通过科学计数法表示

0.00011...(无限重复 0011) 通过科学计数法表示则是 1.10011001...(无线重复 1001)*2

#### 3、转换为 IEEE 754 标准表示

当经过科学计数法表示之后，就可以求得 exponent bias 和 fraction 了。

exponent bias (指数偏移值) **等于** 双精度浮点数**固定偏移值** (2-1) 加上指数实际值(即 2 中的 -4) 的 **11 位二进制表示**。为什么是 11 位？因为 exponent bias 在 64 位中占 11 位。

因此 0.1 的 exponent bias **等于** 1023 + (-4) = 1019 的11 位二进制表示，即 011 1111 1011。

再来获取 0.1 的 fraction，fraction 就是 1.10011001...(无线重复 1001) 中的小数位，由于 fraction 占 52位所以抽取 52 位小数，1001...(中间有 11 个 1001)...1010 **(请注意最后四位，是 1010 而不是 1001，因为四舍五入有进位，这个进位就是造成 0.1 + 0.2 不等于 0.3 的原因)**

```
    0       011 1111 1011   1001...( 11 x 1001)...1010
(sign bit) (exponent bias)      (fraction)
```

此时如果将这个数转换为十进制，可以发现值已经变为 0.100000000000000005551115123126 而不是 0.1 了，因此这个计算精度就出现了问题。

### 解决方法

为了处理这种精度问题，有几种常见的解决方法：

1. **使用整数计算**：

   - 将浮点数转换为整数进行计算，然后在最后转换回浮点数。
   - 例如，计算 `0.1 + 0.2` 时，可以将它们乘以 `10`，得到 `1 + 2`，然后将结果除以 `10`。

   ```js
   let result = (0.1 * 10 + 0.2 * 10) / 10;
   console.log(result); // 输出: 0.3
   ```

2. **四舍五入**：

   - 使用 `toFixed()` 方法将结果四舍五入到所需的精度。

   ```js
   let result = (0.1 + 0.2).toFixed(1);
   console.log(result); // 输出: "0.3"
   ```

3. **使用库**：

   - 使用专门处理浮点数精度问题的库，如 `decimal.js` 或 `bignumber.js`。

### 示例代码

这里有一个使用整数计算的例子：

```js
function addFloats(a, b) {
    const factor = 10; // 选择适当的因子
    return (a * factor + b * factor) / factor;
}

console.log(addFloats(0.1, 0.2)); // 输出: 0.3
```

### 总结

在JavaScript中，`0.1 + 0.2` 不等于 `0.3` 是由于浮点数的精度问题。这种问题在所有使用二进制浮点数的编程语言中都是普遍存在的。为了确保精度，可以采用上述方法之一来处理浮点数的计算。

## 既然0.1不是0.1了，为什么在console.log(0.1)的时候还是0.1呢?

当你在JavaScript中使用 `console.log(0.1)` 时，控制台实际上会将浮点数格式化为一个接近原始十进制表示的字符串。这是因为大多数情况下，开发者希望看到一个易于理解的数字表示，而不是一个复杂的二进制浮点数表示。

#### 内部表示

在内部，`0.1` 实际上被表示为一个非常接近 `0.1` 的二进制浮点数。这个二进制浮点数在二进制表示中是无限循环的，但在JavaScript中被截断为一个有限长度的近似值。

**示例：**

```js
console.log(0.1); // 输出: 0.1
```

### 浮点数的内部表示

根据IEEE 754标准，浮点数在内部被表示为一个二进制形式，这可能导致一些十进制小数不能被精确表示。例如，`0.1` 在二进制中的表示是一个无限循环的小数。

### 如何查看内部表示

如果你想查看 `0.1` 在内部的实际表示，可以使用 `toString` 方法，并指定基数为16（十六进制）来查看其内部表示。

**示例：**

```js
console.log(0.1.toString(16)); // 输出: 0.1999999999999a
```

这里 `0.1999999999999a` 表示的是 `0.1` 在十六进制下的近似值，这反映了它在二进制浮点数中的实际表示。

### 总结

- **控制台输出**：`console.log(0.1)` 显示为 `0.1` 是为了方便阅读和理解。
- **内部表示**：`0.1` 在内部被表示为一个近似的二进制浮点数。
- **精度问题**：浮点数的计算可能会导致精度问题，特别是当涉及到加减运算时。

## 字面量创建对象和 new 创建对象有什么区别

### 1. 使用字面量创建对象

使用字面量创建对象是一种非常直观的方法，可以直接定义对象的属性和值。

#### 语法：

```js
const objectLiteral = {
    property1: value1,
    property2: value2,
    method1: function() {
        // ...
    }
};
```

#### 特点：

- **简单直观**：字面量语法简单易懂，直接在花括号 `{}` 中定义属性和方法。
- **无需构造函数**：不需要定义构造函数，也不涉及原型链的显式设置。
- **属性和方法**：可以在创建对象的同时定义所有的属性和方法。

#### 示例：

```js
const person = {
    name: 'Alice',
    age: 30,
    sayHello: function() {
        console.log(`Hello, my name is ${this.name}.`);
    }
};

person.sayHello(); // 输出: Hello, my name is Alice.
```

### 2. 使用 `new` 关键字和构造函数创建对象

使用构造函数创建对象需要定义一个构造函数，然后使用 `new` 关键字创建对象实例。

#### 语法：

```js
function Person(name, age) {
    this.name = name;
    this.age = age;
}

Person.prototype.sayHello = function() {
    console.log(`Hello, my name is ${this.name}.`);
};

const person = new Person('Alice', 30);
```

#### 特点：

- **构造函数**：需要定义一个构造函数来初始化对象的属性。
- **原型链**：通过设置构造函数的 `prototype` 属性来共享方法，这可以节省内存，因为方法只保存一份。
- **继承**：使用构造函数可以更容易地实现继承。

#### 示例：

```js
function Person(name, age) {
    this.name = name;
    this.age = age;
}

Person.prototype.sayHello = function() {
    console.log(`Hello, my name is ${this.name}.`);
};

const alice = new Person('Alice', 30);
alice.sayHello(); // 输出: Hello, my name is Alice.
```

### 主要区别

- **字面量**：
  - 直接定义属性和方法。
  - 每个对象都有自己的方法副本，如果多个对象共享相同的属性和方法，则可能会占用更多的内存。
  - 适用于简单的对象创建。
- **构造函数 + `new`**：
  - 通过构造函数初始化对象。
  - 方法通常定义在构造函数的 `prototype` 上，这样多个对象实例可以共享这些方法，节省内存。
  - 支持继承，可以创建更加复杂的对象结构。

### 使用场景

- **使用字面量**：
  - 当对象结构简单且不需要共享方法时。
  - 当对象不需要继承时。
- **使用构造函数 + `new`**：
  - 当需要创建多个相似对象时。
  - 当需要使用继承时。
  - 当对象需要共享方法时。

### 总结

- **字面量**：简单直接，适用于简单的对象创建。
- **构造函数 + `new`**：支持更复杂的对象结构和继承，适用于需要创建多个相似对象的情况。

## new 操作符具体干了什么

在JavaScript中，`new`操作符用于创建一个由构造函数定义的新实例。当我们使用`new`操作符来调用一个构造函数时，实际上执行了一系列的操作。下面是一些关键步骤：

1. **创建新对象**：`new`操作符首先创建一个新的空对象。
2. **设置原型**：新创建的对象的原型被设置为构造函数的`prototype`属性所指向的对象。
3. **绑定`this`**：构造函数内部的`this`值被绑定到新创建的对象上，这意味着在构造函数内部对`this`的引用实际上是指向新创建的对象。
4. **执行构造函数**：构造函数被调用，通常它会做一些初始化工作，比如为新对象添加属性和方法。
5. **返回新对象**：如果构造函数没有显式返回一个对象，则默认返回新创建的对象。如果构造函数返回了一个对象类型的值（如另一个对象或者原始类型的包装对象），那么这个返回值会替代新创建的对象。

这里有一个具体的例子来说明这个过程：

```js
function Person(name, age) {
    this.name = name;
    this.age = age;
}

Person.prototype.sayHello = function() {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
};

const john = new Person('John Doe', 30);

john.sayHello(); // 输出: Hello, my name is John Doe and I am 30 years old.
```

在这个例子中，`new Person('John Doe', 30)` 实际上执行了以下步骤：

1. 创建一个新的空对象。
2. 设置新对象的原型为 `Person.prototype`。
3. 在 `Person` 函数内部，`this` 指向新创建的对象。
4. 使用给定的名字和年龄初始化新对象的属性。
5. 返回新创建的对象。

## 手写一个new方法

手写的 `new` 方法需要做以下几件事：

1. 创建一个新的空对象。
2. 设置新对象的原型为构造函数的 `prototype`。
3. 将构造函数的 `this` 指向新创建的对象。
4. 执行构造函数。
5. 如果构造函数没有显式返回一个对象，则返回新创建的对象。

#### 示例代码：

```js
function myNew(constructor, ...args) {
    // Step 1: 创建一个新的空对象
    const newObj = {};

    // Step 2: 设置新对象的原型为构造函数的 prototype
    newObj.__proto__ = constructor.prototype;

    // Step 3: 将构造函数的 this 指向新创建的对象，并执行构造函数
    const result = constructor.apply(newObj, args);

    // Step 4: 如果构造函数返回了一个对象类型的值，则返回这个值
    // 否则返回新创建的对象
    return (typeof result === 'object' && result !== null) || typeof result === 'function' ? result : newObj;
}

// 使用示例
function Person(name, age) {
    this.name = name;
    this.age = age;
}

Person.prototype.sayHello = function() {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
};

const alice = myNew(Person, 'Alice', 30);
alice.sayHello(); // 输出: Hello, my name is Alice and I am 30 years old.
```

### 详细解释

- **创建新对象**：使用 `{}` 创建一个空对象。
- **设置原型**：使用 `__proto__` 属性将新对象的原型设置为构造函数的 `prototype`。
- **执行构造函数**：使用 `apply` 方法调用构造函数，并将 `this` 绑定到新创建的对象上。同时传递构造函数所需的参数。
- **返回新对象或构造函数返回的值**：如果构造函数返回了一个对象类型的值，则返回这个值；否则返回新创建的对象。

### 注意事项

- **构造函数返回值**：如果构造函数返回了一个对象类型的值（例如另一个对象或者原始类型的包装对象），则 `myNew` 方法会返回这个值，而不是新创建的对象。
- **构造函数的返回值**：如果构造函数返回了一个非对象类型的值（例如 `undefined`、`null`、原始类型的值等），则 `myNew` 方法会忽略这个返回值，并返回新创建的对象。

## 类型转换的规则有哪些

在if语句、逻辑语句、数学运算逻辑、==等情况下都可能出现隐士类型转换。

![2019-06-23-09-32-17]( https://xiaomuzhu-image.oss-cn-beijing.aliyuncs.com/c378afab84afcdf430aec5229649faee.png)

## 类型转换的原理是什么


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

## 谈谈你对原型对象的理解✨

### 原型对象的基本概念

在JavaScript中，每个对象都有一个内部的`Prototype`属性，这个属性是原型对象用来创建新对象实例，而所有被创建的对象都会共享原型对象，因此这些对象便可以访问原型对象的属性。

### 原型对象的作用

原型对象的主要作用是用于实现继承。当JavaScript引擎试图查找一个对象的属性或方法时，它会首先在该对象自身上查找。如果没有找到，它会沿着原型链向上查找，直到找到该属性或方法，或者到达原型链的末端（通常是`Object.prototype`，该原型对象的原型为`null`）。

例如`hasOwnProperty()`方法存在于Obejct原型对象中,它便可以被任何对象当做自己的方法使用.

> 用法：`object.hasOwnProperty( propertyName )`

> `hasOwnProperty()`函数的返回值为`Boolean`类型。如果对象`object`具有名称为`propertyName`的属性，则返回`true`，否则返回`false`。

由以上代码可知,`hasOwnProperty()`并不存在于`person`对象中,但是`person`依然可以拥有此方法.

所以`person`对象是如何找到`Object`对象中的方法的呢?靠的是原型链。

### 创建原型对象

当你定义一个构造函数并创建一个实例时，这个实例会有一个指向构造函数原型的内部链接。构造函数的原型可以通过`Constructor.prototype`来访问，其中`Constructor`是你定义的构造函数。

### 示例代码

让我们通过一个简单的示例来说明原型对象的概念：

```js
function Person(name) {
    this.name = name;
}

Person.prototype.sayHello = function() {
    console.log(`Hello, my name is ${this.name}`);
};

const alice = new Person('Alice');
alice.sayHello(); // 输出: Hello, my name is Alice
```

### 原型对象分析

1. **`Person` 构造函数**：
   - 定义了一个名为 `sayHello` 的方法。
   - `Person.prototype` 是一个对象，它是所有 `Person` 实例的原型。
2. **创建 `Person` 实例**：
   - 创建了一个名为 `alice` 的 `Person` 实例。
   - `alice`的原型链包含：
     - `alice.__proto__` 指向 `Person.prototype`
     - `Person.prototype.__proto__` 指向 `Object.prototype`
     - `Object.prototype.__proto__` 指向 `null`
3. **调用 `sayHello` 方法**：
   - 当 `alice.sayHello()` 被调用时，JavaScript 引擎首先在 `alice` 上查找 `sayHello` 方法。
   - 没有找到，然后沿着原型链向上查找。
   - 在 `Person.prototype` 中找到了 `sayHello` 方法，并执行它。

### 原型对象与继承

原型对象是JavaScript实现继承的基础。当一个对象的原型指向另一个对象时，就形成了一个继承关系。子对象可以访问父对象的属性和方法，这就是继承。

**示例代码**

```js
function Animal(sound) {
    this.sound = sound;
}

Animal.prototype.makeSound = function() {
    console.log(this.sound);
};

function Dog(sound, breed) {
    Animal.call(this, sound);
    this.breed = breed;
}

Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

Dog.prototype.bark = function() {
    console.log("Woof!");
};

const myDog = new Dog("Woof", "Golden Retriever");
myDog.makeSound(); // 输出: Woof
myDog.bark(); // 输出: Woof
```

### 总结

- **原型对象**： 是每个构造函数的一个属性，它用于存储该构造函数实例共有的属性和方法。
- **继承**： 通过设置对象的原型来实现，使得子对象可以访问父对象的属性和方法。
- **查找机制**：当查找一个属性或方法时，从当前对象开始，沿着原型链向上查找，直到找到或到达原型链的末端。

## 谈谈你对原型链的理解✨

原型链（Prototype Chain）是JavaScript中一个非常重要的概念，它用于实现继承和对象间属性及方法的查找。理解原型链的工作原理对于深入掌握JavaScript是非常关键的。

### 原型链的基本概念

在JavaScript中，每个对象都有 `__proto__` 属性，此属性指向该对象的构造函数的原型。对象可以通过 `__proto__`与上游的构造函数的原型对象连接起来，而上游的原型对象也有一个`__proto__`，这样就形成了原型链。

> 经典原型链图

![2019-06-15-05-36-59]( https://xiaomuzhu-image.oss-cn-beijing.aliyuncs.com/282ef60fe1dfe60924c6caeaeab6c550.png)

### 示例代码

让我们通过一个简单的示例来说明原型链的工作原理：

```js
function Person(name) {
    this.name = name;
}

Person.prototype.sayHello = function() {
    console.log(`Hello, my name is ${this.name}`);
};

function Student(name, grade) {
    Person.call(this, name);
    this.grade = grade;
}

// 设置 Student 的原型为 Person 的实例
Student.prototype = Object.create(Person.prototype);

// 修复构造函数
Student.prototype.constructor = Student;

Student.prototype.study = function(subject) {
    console.log(`${this.name} is studying ${subject}`);
};

const alice = new Student('Alice', 10);
alice.sayHello(); // 输出: Hello, my name is Alice
alice.study('Math'); // 输出: Alice is studying Math
```

### 原型链分析

1. **`Person` 构造函数**：
   - 定义了一个名为 `sayHello` 的方法。
   - `Person.prototype` 是一个对象，它是所有 `Person` 实例的原型。
2. **`Student` 构造函数**：
   - 继承了 `Person` 的属性和方法。
   - 使用 `Object.create()` 方法设置了 `Student.prototype` 为 `Person.prototype` 的一个新实例。
   - 添加了一个名为 `study` 的方法。
   - 修复了 `Student.prototype.constructor` 为 `Student` 构造函数。
3. **创建 `Student` 实例**：
   - 创建了一个名为 `alice` 的 `Student` 实例。
   - `alice`的原型链包含：
     - `alice.__proto__` 指向 `Student.prototype`
     - `Student.prototype.__proto__` 指向 `Person.prototype`
     - `Person.prototype.__proto__` 指向 `Object.prototype`
     - `Object.prototype.__proto__` 指向 `null`

### 原型链查找过程

当 `alice.sayHello()` 被调用时：

1. JavaScript 引擎首先在 `alice` 上查找 `sayHello` 方法。
2. 没有找到，然后沿着原型链向上查找。
3. 在 `Person.prototype` 中找到了 `sayHello` 方法，并执行它。

## 如何判断是否是数组

在JavaScript中，判断一个变量是否是数组有几种常用的方法。下面我将详细介绍这些方法及其使用场景。

### 1. 使用 `Array.isArray()`

`Array.isArray()` 是一个静态方法，用来检查一个值是否是一个数组。这是推荐的现代方法，因为它简单、直观且可靠。

**示例代码：**

```js
const arr = [1, 2, 3];
const str = "Hello, world!";

console.log(Array.isArray(arr)); // 输出: true
console.log(Array.isArray(str)); // 输出: false
```

### 2. 使用 `instanceof Array`

`instanceof` 操作符可以用来测试一个对象是否是特定类的一个实例。

#### 示例代码：

```js
const arr = [1, 2, 3];
const str = "Hello, world!";

console.log(arr instanceof Array); // 输出: true
console.log(str instanceof Array); // 输出: false
```

### 3. 使用 `typeof` 和 `toString` 方法

这种方法利用 `Object.prototype.toString.call()` 方法来确定变量的具体类型。每个内置类型的 `toString` 方法都会返回一个特定的字符串，对于数组来说，它会返回 `[object Array]`。

#### 示例代码：

```js
const arr = [1, 2, 3];
const str = "Hello, world!";

function isArray(value) {
    return Object.prototype.toString.call(value) === '[object Array]';
}

console.log(isArray(arr)); // 输出: true
console.log(isArray(str)); // 输出: false
```

### 4. 使用 `constructor` 属性

虽然这不是一个可靠的方法，但在某些情况下可以使用对象的 `constructor` 属性来检查它是否是一个数组。

#### 示例代码：

```js
const arr = [1, 2, 3];
const str = "Hello, world!";

function isArray(value) {
    return value.constructor === Array;
}

console.log(isArray(arr)); // 输出: true
console.log(isArray(str)); // 输出: false
```

### 注意事项

- **`instanceof` 方法**：
  - 这个方法在大多数情况下是可靠的，但它依赖于原型链，如果原型链被修改过，可能会给出错误的结果。
  - 如果你的代码可能在不同的全局作用域中运行（例如在不同的浏览器窗口或框架中），`instanceof` 可能会给出错误的结果。
- **`constructor` 属性**：
  - 这个方法不推荐使用，因为 `constructor` 属性可以被篡改。
  - 如果有人手动修改了 `constructor` 属性，这个方法就会失败。

### 总结

- **推荐方法**：使用 `Array.isArray()`，因为它简单、可靠且跨浏览器兼容。
- **备选方法**：使用 `instanceof Array` 或 `Object.prototype.toString.call()`，这些方法在大多数情况下也有效。

## instanceof的原理是什么

`instanceof` 是JavaScript中的一个二元运算符，用于检测一个对象是否为某个构造函数的实例。`instanceof` 运算符的工作原理涉及到原型链和继承的概念。

### `instanceof` 的工作原理

`instanceof` 运算符的工作原理可以概括为以下步骤：

1. **获取原型**：获取右侧构造函数的 `prototype` 属性。
2. **比较原型**：检查左侧对象的内部 `[[Prototype]]` 链中是否包含右侧构造函数的 `prototype`。
3. **返回布尔值**：如果包含，则返回 `true`；否则返回 `false`。

### 详细解释

- **原型链**：每个JavaScript对象都有一个内部的 `[[Prototype]]` 属性，它指向该对象的原型对象。如果一个对象没有直接的原型，它的 `[[Prototype]]` 将指向 `null`。
- **构造函数的 `prototype` 属性**：每个构造函数都有一个 `prototype` 属性，它是一个对象，包含了构造函数创建的所有实例共享的属性和方法。

### 示例

假设我们有两个构造函数 `Person` 和 `Student`，并且 `Student` 继承自 `Person`。

```js
function Person(name) {
    this.name = name;
}

function Student(name, grade) {
    Person.call(this, name);
    this.grade = grade;
}

// 设置继承关系
Student.prototype = Object.create(Person.prototype);
Student.prototype.constructor = Student;

// 创建实例
const alice = new Student('Alice', 12);

// 使用 instanceof 检查实例类型
console.log(alice instanceof Student); // 输出: true
console.log(alice instanceof Person);  // 输出: true
console.log(alice instanceof Object);  // 输出: true
```

### 分析

- **`alice instanceof Student`**：`alice` 的 `[[Prototype]]` 指向 `Student.prototype`，因此结果为 `true`。
- **`alice instanceof Person`**：`Student.prototype` 的 `[[Prototype]]` 指向 `Person.prototype`，因此结果也为 `true`。
- **`alice instanceof Object`**：所有对象的原型链最终都指向 `Object.prototype`，因此结果也是 `true`。

### 注意事项

- **原型链**：`instanceof` 会沿着原型链向上查找，直到找到匹配的原型或者到达原型链的末端。
- **`null` 和 `undefined`**：`null` 和 `undefined` 没有原型链，因此它们与任何构造函数使用 `instanceof` 检查时都会返回 `false`。
- **跨域对象**：如果对象来自另一个域，则 `instanceof` 的结果可能不正确，因为原型链可能不一致。

### 总结

- **`instanceof` 运算符**：用于检测一个对象是否为某个构造函数的实例。
- **工作原理**：检查对象的原型链中是否包含构造函数的 `prototype`。
- **注意事项**：注意原型链的结构和跨域对象的问题。

## instanceof和typeof两者的区别

在JavaScript中，`instanceof` 和 `typeof` 是两种常用的类型检测方法，它们各有特点和适用场景。下面我将详细解释这两种方法的优缺点、异同点，并讨论在判断属性类型时哪一种更好。

### 1. `typeof`

`typeof` 是一个一元运算符，用于检测变量的数据类型，并返回一个字符串表示该类型。

#### 优点：

- **简单易用**：`typeof` 语法简单，易于理解和使用。
- **广泛支持**：所有JavaScript实现都支持 `typeof`。
- **快速**：`typeof` 检测类型的速度很快。

#### 缺点：

- **不区分数组和其他对象**：`typeof` 对于数组和非数组对象都返回 `"object"`。
- **对 `null` 的处理**：`typeof null` 返回 `"object"`，这是JavaScript的一个历史遗留问题。
- **对 `function` 的处理**：对于函数，`typeof` 返回 `"function"`，但不区分普通函数和构造函数。

#### 示例代码：

```js
console.log(typeof 42); // 输出: "number"
console.log(typeof "hello"); // 输出: "string"
console.log(typeof true); // 输出: "boolean"
console.log(typeof undefined); // 输出: "undefined"
console.log(typeof null); // 输出: "object" （注意：这是一个特殊情况）
console.log(typeof {}); // 输出: "object"
console.log(typeof []); // 输出: "object"
console.log(typeof function() {}); // 输出: "function"
```

### 2. `instanceof`

`instanceof` 是一个二元运算符，用于检测一个对象是否为某个构造函数的实例。

#### 优点：

- **区分数组和其他对象**：`instanceof` 可以区分数组和普通对象。
- **区分构造函数**：`instanceof` 可以区分不同的构造函数实例。

#### 缺点：

- **依赖原型链**：`instanceof` 的结果依赖于对象的原型链，如果原型链被篡改，结果可能不准确。
- **全局作用域问题**：在不同的全局作用域中使用 `instanceof` 可能会给出错误的结果。

#### 示例代码：

```js
console.log([1, 2, 3] instanceof Array); // 输出: true
console.log({} instanceof Object); // 输出: true
console.log(new String("hello") instanceof String); // 输出: true
console.log(new Date() instanceof Date); // 输出: true
```

### 3. 异同点

- **相同点**：
  - 两者都是用来检测类型的方法。
  - 都可以用来识别基本类型和引用类型。
- **不同点**：
  - `typeof` 是一个一元运算符，而 `instanceof` 是一个二元运算符。
  - `typeof` 可以检测基本类型（如 `number`, `string`, `boolean`, `undefined`）和引用类型（如 `object`, `function`）。
  - `instanceof` 主要用于检测一个对象是否为某个构造函数的实例。

### 4. 判断属性类型时的选择

- **对于基本类型**：使用 `typeof` 是最佳选择，因为它简单且易于使用。
- 对于引用类型：
  - 如果你需要区分数组和其他对象，使用 `instanceof` 更好，因为它可以直接区分数组和普通对象。
  - 如果你想确认一个对象是否为某个特定构造函数的实例，使用 `instanceof` 更好。
  - 如果你关心的是一个对象是否是一个数组，推荐使用 `Array.isArray()`，因为它简单且可靠。

### 总结

- **`typeof`** 适用于检测基本类型和简单的引用类型。
- **`instanceof`** 适用于检测对象是否是特定构造函数的实例，特别适合于区分数组和其他对象。
- **`Array.isArray()`** 是检测数组的最佳选择，因为它简单且可靠。

## 谈一谈你对this的了解✨

`this` 关键字是JavaScript中一个非常重要的概念，它代表了当前执行上下文中的“主体”对象。this的指向不是在编写时确定的，而是在执行时确定的，同时，this不同的指向在于遵循了一定的规则。

### 1、默认情况下：

this是指向全局对象的，比如在浏览器就是指向window。

```js
name = "Bale";

function sayName () {
    console.log(this.name);
};

sayName(); //"Bale"
```

### 2、作为普通函数调用：

- 当函数作为普通函数调用时（即不作为对象的方法调用），`this` 的值通常取决于函数执行的上下文。
- 在非严格模式下（`function foo() { ... }`），`this` 指向全局对象（在浏览器中通常是 `window`）。
- 在严格模式下（`function foo() { "use strict"; ... }`），`this` 的值是 `undefined`。

```js
function sayHello() {
    console.log(this);
}

sayHello(); // 输出: window (非严格模式) 或 undefined (严格模式)
```

### 3、**作为对象的方法调用**：

- 当函数作为对象的方法调用时，`this` 的值是指向调用该方法的对象。

```js
const person = {
    name: "Alice",
    sayHello: function() {
        console.log("Hello, my name is " + this.name);
    }
};

person.sayHello(); // 输出: Hello, my name is Alice
```

### 4、**使用构造函数调用**：

- 当使用 `new` 关键字调用构造函数时，`this` 指向新创建的对象实例。

```js
function Person(name) {
    this.name = name;
}

const alice = new Person("Alice");
console.log(alice.name); // 输出: Alice
```

### 5、**使用 `call`, `apply` 或 `bind` 方法调用**：

- 这些方法可以显式地设置 `this` 的值。
- `call` 和 `apply` 方法立即执行函数，而 `bind` 方法返回一个新的函数，其中 `this` 已经绑定到指定的对象。

```js
function sayHello() {
    console.log("Hello, my name is " + this.name);
}

const person = { name: "Alice" };
sayHello.call(person); // 输出: Hello, my name is Alice
sayHello.apply(person); // 输出: Hello, my name is Alice

const boundSayHello = sayHello.bind(person);
boundSayHello(); // 输出: Hello, my name is Alice
```

### 6、**箭头函数**：

- 箭头函数没有自己的 `this` 值，而是从封闭作用域中继承 `this` 的值。
- 这意味着箭头函数中的 `this` 与其所在作用域中的 `this` 是相同的。

```js
const person = {
    name: "Alice",
    sayHello: function() {
        setTimeout(() => {
            console.log("Hello, my name is " + this.name);
        }, 1000);
    }
};

person.sayHello(); // 输出: Hello, my name is Alice (1秒后)
```

### 注意事项

- **非严格模式与严格模式**：在非严格模式下，`this` 在全局作用域中指向全局对象（通常是 `window`），而在严格模式下则指向 `undefined`。
- **函数内部的 `this`**：在函数内部，`this` 的值取决于函数是如何被调用的。
- **箭头函数没有自己的 `this`**：箭头函数从其封闭作用域继承 `this` 的值。

### 总结

- `this` 的值取决于函数的调用方式。
- 在不同的调用上下文中，`this` 的值可能指向全局对象、调用该方法的对象或新创建的对象实例。
- 使用 `call`, `apply`, `bind` 方法可以显式地设置 `this` 的值。
- 箭头函数没有自己的 `this` 值，而是从封闭作用域中继承。

> 绑定优先级:  new绑定 > 显式绑定 >隐式绑定 >默认绑定

## 那么箭头函数的this指向哪里✨

箭头函数（Arrow Function）在JavaScript中具有特殊的 `this` 行为。与普通函数不同，箭头函数没有自己的 `this` 值，而是从封闭作用域中继承 `this` 的值。这意味着箭头函数中的 `this` 值与其所在的作用域中的 `this` 值相同。

### 箭头函数的特点

- **没有自己的 `this`**：箭头函数不绑定自己的 `this` 值，而是从封闭作用域继承 `this` 的值。
- **词法作用域**：箭头函数遵循词法作用域（lexical scoping），这意味着它的 `this` 值是在定义时确定的，而不是在调用时确定的。

### 示例代码

让我们通过几个示例来理解箭头函数中 `this` 的行为：

#### 示例 1：在对象的方法中使用箭头函数

```js
const person = {
    name: "Alice",
    sayHello: function() {
        setTimeout(() => {
            console.log("Hello, my name is " + this.name);
        }, 1000);
    }
};

person.sayHello(); // 输出: Hello, my name is Alice (1秒后)
```

在这个例子中，箭头函数中的 `this` 指向 `person` 对象，因为在箭头函数被定义时，其封闭作用域中的 `this` 是指向 `person` 的。

#### 示例 2：在构造函数中使用箭头函数

```js
function Person(name) {
    this.name = name;
    this.sayHello = function() {
        setTimeout(() => {
            console.log("Hello, my name is " + this.name);
        }, 1000);
    };
}

const alice = new Person("Alice");
alice.sayHello(); // 输出: Hello, my name is Alice (1秒后)
```

在这个例子中，箭头函数中的 `this` 指向 `alice` 对象，因为在箭头函数被定义时，其封闭作用域中的 `this` 是指向 `alice` 的。

#### 示例 3：在事件监听器中使用箭头函数

```js
document.getElementById("myButton").addEventListener("click", () => {
    console.log(this); // 输出: window 或 document (取决于浏览器实现)
});

// 或者
const button = document.getElementById("myButton");
button.addEventListener("click", () => {
    console.log(this); // 输出: button 元素
});
```

在这个例子中，箭头函数中的 `this` 指向事件发生时的上下文。在第一个示例中，`this` 可能指向 `window` 或 `document`（取决于浏览器实现），而在第二个示例中，`this` 指向触发事件的按钮元素。

### 总结

- **箭头函数中的 `this`**：箭头函数没有自己的 `this` 值，而是从其封闭作用域继承 `this` 的值。
- **词法作用域**：箭头函数遵循词法作用域，这意味着 `this` 的值在定义时就已经确定了。

## 箭头函数和普通函数的区别有哪些

箭头函数（Arrow Functions）和普通函数（Regular Functions）在JavaScript中有一些重要的区别。下面是一些主要的区别：

### 1. 语法

- **箭头函数**：

  ```js
  const arrowFunc = (param1, param2) => {
    // 函数体
  };
  ```

- **普通函数**：

  ```js
  function regularFunc(param1, param2) {
    // 函数体
  }
  ```

### 2. `this` 的绑定

- **箭头函数**：箭头函数不绑定自己的 `this`，而是继承自定义函数所在的上下文中的 `this` 值。这意味着箭头函数中的 `this` 与定义它的上下文中的 `this` 是相同的。
- **普通函数**：普通函数有自己的 `this` 绑定。在非严格模式下，如果没有明确绑定，`this` 通常指向全局对象（在浏览器中是 `window`，在 Node.js 中是 `global`）。在严格模式下，`this` 为 `undefined`。

**示例**

```js
const obj = {
  value: 10,
  logValue: function() {
    console.log(this.value);
  },
  logValueWithArrow: () => {
    console.log(this.value);
  }
};

obj.logValue(); // 输出: 10
obj.logValueWithArrow(); // 输出: undefined (在浏览器中) 或 global 对象的值 (在 Node.js 中)

// 在类的方法中
class MyClass {
  value = 10;
  logValue() {
    console.log(this.value);
  }
  logValueWithArrow = () => {
    console.log(this.value);
  }
}

const myInstance = new MyClass();
myInstance.logValue(); // 输出: 10
myInstance.logValueWithArrow(); // 输出: 10
```

### 3. `arguments` 对象

- **箭头函数**：箭头函数没有自己的 `arguments` 对象，而是直接使用定义它的上下文中的 `arguments`。
- **普通函数**：普通函数有自己的 `arguments` 对象。

**示例**

```js
function regularFunc() {
  console.log(arguments); // 输出: arguments 对象
}

const arrowFunc = () => {
  console.log(arguments); // 抛出 ReferenceError: arguments is not defined
};

regularFunc(1, 2, 3);
arrowFunc(1, 2, 3);
```

### 4. 构造函数

- **箭头函数**：不能用作构造函数，因此不能使用 `new` 关键字调用。
- **普通函数**：可以用作构造函数，并可以使用 `new` 关键字调用。

**示例**

```js
function RegularConstructor() {
  this.value = 10;
}

const regularInstance = new RegularConstructor();
console.log(regularInstance.value); // 输出: 10

const ArrowConstructor = () => {
  this.value = 10;
};

const arrowInstance = new ArrowConstructor(); // 抛出 TypeError: Arrow functions cannot be used as constructors
```

### 5. 函数体和返回值

- **箭头函数**：如果函数体只有一条语句并且是返回语句，则可以省略花括号和 `return` 关键字。
- **普通函数**：必须显式使用 `return` 关键字来返回值。

**示例**

```js
const arrowFunc = x => x + 1; // 等价于: (x) => { return x + 1; }
const regularFunc = function(x) {
  return x + 1;
};

console.log(arrowFunc(5)); // 输出: 6
console.log(regularFunc(5)); // 输出: 6
```

### 6. 词法作用域

- **箭头函数**：箭头函数中的 `this`、`arguments` 和其他变量都遵循词法作用域。
- **普通函数**：普通函数中的 `this` 和 `arguments` 不遵循词法作用域，而是根据函数调用的方式动态决定。

### 总结

- **箭头函数**：更简洁的语法、不绑定自己的 `this`、没有自己的 `arguments` 对象、不能用作构造函数。
- **普通函数**：有自己的 `this` 绑定、有自己的 `arguments` 对象、可以用作构造函数。

## async/await是什么

`async/await` 是JavaScript中处理异步操作的一种方式，它让异步代码看起来像同步代码一样简洁易读。`async/await` 是基于Promise构建的，它使得异步函数的编写更加直观和简洁。

### `async` 关键字

`async` 关键字用于声明一个函数为异步函数。这样的函数会返回一个Promise对象。如果函数体中没有任何 `await` 表达式，返回的Promise会自动解析为函数的返回值。

#### 示例：

```js
async function fetchUser() {
    const response = await fetch('https://api.example.com/user');
    const user = await response.json();
    return user;
}
```

### `await` 关键字

`await` 关键字用于等待一个Promise解析完成。`await` 只能在 `async` 函数内部使用。当 `await` 一个Promise时，如果Promise成功，`await` 表达式的结果就是该Promise的成功值；如果Promise失败，`await` 表达式会抛出一个异常，需要通过 `try...catch` 块来捕获。

#### 示例：

```js
async function fetchUser() {
    try {
        const response = await fetch('https://api.example.com/user');
        if (!response.ok) {
            throw new Error('Network response was not ok');
        }
        const user = await response.json();
        console.log(user);
    } catch (error) {
        console.error('There has been a problem with your fetch operation:', error);
    }
}
```

### 优点

- **更简洁的语法**：`async/await` 使得异步代码看起来更像是同步代码，提高了代码的可读性和可维护性。
- **错误处理**：可以使用传统的 `try...catch` 结构来处理错误，使错误处理更加直观。
- **简化Promise链**：避免了Promise链中的回调地狱（callback hell），使得代码更加简洁。

### 示例代码

下面是一个使用 `async/await` 的完整示例，演示了如何从API获取数据并处理可能发生的错误：

```js
async function fetchUser() {
    try {
        const response = await fetch('https://api.example.com/user');
        if (!response.ok) {
            throw new Error('Network response was not ok');
        }
        const user = await response.json();
        console.log(user);
    } catch (error) {
        console.error('There has been a problem with your fetch operation:', error);
    }
}

fetchUser();
```

### 注意事项

- **`await` 必须在 `async` 函数内部使用**：你不能在普通的同步函数中使用 `await` 关键字。
- **`async` 函数总是返回一个Promise**：即使没有显式返回值，`async` 函数也会返回一个解析为 `undefined` 的Promise。
- **`async` 函数可以抛出异常**：如果 `async` 函数中有一个未捕获的异常，它会被转化为一个被拒绝的Promise。

### 总结

- **`async`** 关键字用于声明一个函数为异步函数，这样的函数返回一个Promise。
- **`await`** 关键字用于等待一个Promise的解析结果，只能在 `async` 函数内部使用。
- **`async/await`** 使得异步代码更加简洁、直观，提高了代码的可读性和可维护性。

## async/await相比于Promise的优势

### 1. 更简洁的语法

`async/await` 使得异步代码看起来更像同步代码，提高了代码的可读性和可维护性。这使得代码更容易理解，尤其是对于那些不熟悉异步编程的新手来说。

#### 示例：

使用Promise：

```js
fetch('https://api.example.com/user')
    .then(response => {
        if (!response.ok) {
            throw new Error('Network response was not ok');
        }
        return response.json();
    })
    .then(user => console.log(user))
    .catch(error => console.error('There has been a problem with your fetch operation:', error));
```

使用 `async/await`：

```js
async function fetchUser() {
    try {
        const response = await fetch('https://api.example.com/user');
        if (!response.ok) {
            throw new Error('Network response was not ok');
        }
        const user = await response.json();
        console.log(user);
    } catch (error) {
        console.error('There has been a problem with your fetch operation:', error);
    }
}

fetchUser();
```

### 2. 错误处理

`async/await` 可以使用传统的 `try...catch` 结构来处理错误，使得错误处理更加直观。这样可以更容易地捕获和处理错误，而不需要层层嵌套的 `.catch()`。

#### 示例：

使用Promise：

```js
fetch('https://api.example.com/user')
    .then(response => {
        if (!response.ok) {
            throw new Error('Network response was not ok');
        }
        return response.json();
    })
    .then(user => console.log(user))
    .catch(error => console.error('There has been a problem with your fetch operation:', error));
```

使用 `async/await`：

```js
async function fetchUser() {
    try {
        const response = await fetch('https://api.example.com/user');
        if (!response.ok) {
            throw new Error('Network response was not ok');
        }
        const user = await response.json();
        console.log(user);
    } catch (error) {
        console.error('There has been a problem with your fetch operation:', error);
    }
}

fetchUser();
```

### 3. 简化Promise链

`async/await` 避免了Promise链中的回调地狱（callback hell），使得代码更加简洁。这意味着你可以更容易地管理复杂的异步流程。

#### 示例：

使用Promise：

```js
fetch('https://api.example.com/user')
    .then(user => {
        return fetch(`https://api.example.com/posts?userId=${user.id}`);
    })
    .then(postsResponse => {
        return postsResponse.json();
    })
    .then(posts => {
        console.log(posts);
    })
    .catch(error => console.error('There has been a problem with your fetch operation:', error));
```

使用 `async/await`：

```js
async function fetchPostsForUser(userId) {
    try {
        const userResponse = await fetch(`https://api.example.com/user?id=${userId}`);
        const user = await userResponse.json();

        const postsResponse = await fetch(`https://api.example.com/posts?userId=${user.id}`);
        const posts = await postsResponse.json();

        console.log(posts);
    } catch (error) {
        console.error('There has been a problem with your fetch operation:', error);
    }
}

fetchPostsForUser(1);
```

### 4. 易于调试

由于 `async/await` 使得异步代码看起来更像同步代码，因此在调试时更容易设置断点和跟踪代码执行流程。

### 5. 更好的控制流

使用 `async/await` 可以更容易地控制异步操作的顺序，比如在一系列异步操作之间插入同步操作。

### 总结

- **更简洁的语法**：`async/await` 使得异步代码更加简洁易读。
- **错误处理**：可以使用传统的 `try...catch` 结构来处理错误，使错误处理更加直观。
- **简化Promise链**：避免了Promise链中的回调地狱，使得代码更加简洁。
- **易于调试**：由于代码看起来更像同步代码，因此更容易调试。
- **更好的控制流**：更容易控制异步操作的顺序。

## 聊一聊如何在JavaScript中实现不可变对象

在JavaScript中实现不可变对象可以通过多种方式来完成。不可变对象指的是对象的状态一旦创建之后就不能被改变的对象。这有助于提高代码的可预测性和减少潜在的bug。

### 1. 使用 `Object.freeze()`

`Object.freeze()` 方法可以冻结一个对象，使其成为不可变的。冻结后的对象不允许添加新属性，现有的属性也不能被修改，也不能删除现有属性。

#### 示例代码：

```js
const person = {
    name: "Alice",
    age: 25
};

Object.freeze(person);

// 尝试修改属性
person.name = "Bob"; // 不会改变 person.name 的值

// 尝试添加新属性
person.gender = "female"; // 不会添加新属性

// 尝试删除属性
delete person.age; // 不会删除 age 属性

console.log(person); // 输出: { name: "Alice", age: 25 }
```

### 2. 使用只读属性

通过定义只读属性，我们可以创建不可变对象。在ES6中，我们可以使用 `Object.defineProperty()` 方法来定义只读属性。

#### 示例代码：

```js
const person = {};

Object.defineProperty(person, 'name', {
    value: "Alice",
    writable: false,
    enumerable: true,
    configurable: false
});

Object.defineProperty(person, 'age', {
    value: 25,
    writable: false,
    enumerable: true,
    configurable: false
});

// 尝试修改属性
person.name = "Bob"; // 不会改变 person.name 的值

console.log(person); // 输出: { name: "Alice", age: 25 }
```

### 3. 使用 `Object.preventExtensions()`

`Object.preventExtensions()` 方法阻止向对象添加新属性，但现有的属性仍然可以被修改。如果你想创建一个不可添加新属性但允许修改现有属性的对象，可以使用这个方法。

#### 示例代码：

```js
const person = {
    name: "Alice",
    age: 25
};

Object.preventExtensions(person);

// 尝试添加新属性
person.gender = "female"; // 不会添加新属性

console.log(person); // 输出: { name: "Alice", age: 25 }
```

### 4. 使用 `Object.seal()`

`Object.seal()` 方法不仅阻止向对象添加新属性，还阻止删除现有属性，但现有属性仍然可以被修改。如果你想创建一个不可添加新属性也不可删除现有属性的对象，可以使用这个方法。

#### 示例代码：

```js
const person = {
    name: "Alice",
    age: 25
};

Object.seal(person);

// 尝试添加新属性
person.gender = "female"; // 不会添加新属性

// 尝试删除属性
delete person.age; // 不会删除 age 属性

console.log(person); // 输出: { name: "Alice", age: 25 }
```

### 5. 使用 `const` 和深拷贝

如果对象是浅层的，可以使用 `const` 和深拷贝来创建一个不可变的对象。

#### 示例代码：

```js
const person = {
    name: "Alice",
    age: 25
};

const immutablePerson = JSON.parse(JSON.stringify(person));

// 尝试修改属性
immutablePerson.name = "Bob"; // 不会改变 immutablePerson.name 的值

console.log(immutablePerson); // 输出: { name: "Alice", age: 25 }
```

请注意，这种方法仅适用于浅层的对象，对于包含深层嵌套对象的情况，需要使用专门的深拷贝库或函数来处理。

### 总结

- **`Object.freeze()`**：最严格的不可变性，禁止修改现有属性的值、添加新属性或删除现有属性。
- **只读属性**：使用 `Object.defineProperty()` 来定义只读属性。
- **`Object.preventExtensions()`**：防止添加新属性，但允许修改现有属性。
- **`Object.seal()`**：防止添加新属性和删除现有属性，但允许修改现有属性的值。
- **使用 `const` 和深拷贝**：创建一个不可变的浅层对象。

> 原理详解请移步[实现JavaScript不可变数据](#immuatble)

## 简述一下你对 web 性能优化的方案

- 尽量减少`HTTP`请求。
- 使⽤浏览器缓存。
- 使⽤压缩组件。
- 图片、JavaScript的预载入。
- 将脚本放在底部。
- 将样式文件放在⻚⾯顶部。
- 使⽤外部的`JS`和`CSS`。
- 精简代码。

## JS中会造成内存泄漏的情况

在JavaScript中，内存泄漏是指程序中不再需要的内存没有被及时释放，导致可用内存逐渐减少，最终可能导致程序性能下降甚至崩溃。下面是一些常见会导致内存泄漏的情况：

### 1. 循环引用

循环引用是指两个或多个对象互相引用对方，导致垃圾回收器无法正确识别这些对象为垃圾。这种情况下，即使对象不再被使用，它们也不会被回收。

**示例：**

```js
function createLeak() {
    const objA = {};
    const objB = {};
    objA.reference = objB;
    objB.reference = objA;
}

createLeak();
```

### 2. 闭包

闭包可以保持对外部变量的引用，如果闭包长时间存在并且外部变量不再需要，则会导致这些变量占据内存而不会被回收。

**示例：**

```js
function createLeak() {
    let data = [];
    setInterval(function() {
        data.push({ message: "Memory leak!" });
    }, 1000);
}

createLeak();
```

### 3. 未清除的定时器和事件监听器

定时器和事件监听器如果未被清除，可能会持续占用内存。

**示例：**

```js
function createLeak() {
    document.getElementById("someElement").addEventListener("click", function() {
        // do something
    });

    setInterval(function() {
        // do something
    }, 1000);
}

createLeak();
```

### 4. DOM元素引用

如果DOM元素被JavaScript代码引用，而该元素被从DOM树中移除，那么该DOM元素将不会被垃圾回收。

**示例：**

```js
function createLeak() {
    const element = document.createElement("div");
    element.onclick = function() {
        // do something
    };
    document.body.appendChild(element);
    document.body.removeChild(element);
}

createLeak();
```

### 5. 全局变量

全局变量如果不被清除，会一直占据内存。

**示例：**

```js
let globalVar;

function createLeak() {
    globalVar = new Array(1000000);
}

createLeak();
```

### 6. Node.js中的持久事件监听器

在Node.js环境中，如果事件监听器没有被适当清除，也可能导致内存泄漏。

**示例：**

```js
const http = require('http');

function createLeak() {
    const server = http.createServer((req, res) => {
        // do something
    });

    server.listen(3000);
}

createLeak();
```

### 解决方法

- **清除定时器**：使用 `clearTimeout` 或 `clearInterval` 清除定时器。
- **移除事件监听器**：使用 `removeEventListener` 移除不再需要的事件监听器。
- **解除DOM元素引用**：在DOM元素从页面中移除之前，解除对该元素的所有引用。
- **使用弱引用**：某些JavaScript引擎支持弱引用，可以用来避免循环引用问题。
- **及时解除引用**：当不再需要一个对象时，显式地将其引用设置为 `null` 或者其他值，帮助垃圾回收器更快地识别无用对象。

### 总结

- **循环引用**：对象互相引用导致垃圾回收器无法回收。
- **闭包**：闭包保持对外部变量的引用，如果外部变量不再需要，则可能导致内存泄漏。
- **未清除的定时器和事件监听器**：定时器和事件监听器如果未被清除，可能会持续占用内存。
- **DOM元素引用**：DOM元素被JavaScript代码引用，如果元素从DOM树中移除但引用仍然存在，则可能导致内存泄漏。
- **全局变量**：全局变量如果不被清除，会一直占据内存。
- **Node.js中的持久事件监听器**：事件监听器没有被适当清除，可能导致内存泄漏。

## 介绍一下Promise，Promise的原理是什么

Promise 是 JavaScript 中用于处理异步操作的一种模式。它提供了一个更清晰的方式来组织异步代码，避免了所谓的“回调地狱”（callback hell）问题，即多个嵌套的回调函数使得代码难以阅读和维护。

### Promise 的概念

在 JavaScript 中，Promise 是一个代表异步操作最终完成（或失败）及其结果的对象。Promise 对象有三种状态：

1. **Pending（待定）**：初始状态，既不是成功也不是失败。
2. **Fulfilled（已成功）**：代表异步操作已完成并且成功。
3. **Rejected（已失败）**：代表异步操作已完成但是失败了。

一旦 Promise 处于 `fulfilled` 或 `rejected` 状态，它就会保持这种状态不变。

### Promise 的基本用法

创建一个 Promise 需要传递一个执行器函数给构造函数，这个执行器函数会立即执行。执行器函数接收两个参数：`resolve` 和 `reject`，这两个都是函数，用于改变 Promise 的状态。

```js
const promise = new Promise((resolve, reject) => {
  // 异步操作
  setTimeout(() => {
    const success = true; // 假设这里有一个异步操作的结果
    if (success) {
      resolve('Success!');
    } else {
      reject(new Error('Something went wrong.'));
    }
  }, 1000);
});

// 处理成功的情况
promise.then(result => {
  console.log('Result:', result);
}).catch(error => {
  console.error('Error:', error);
});
```

### Promise 的核心方法

- **`.then()`**：用于指定 Promise 成功后的回调函数。
- **`.catch()`**：用于指定 Promise 失败后的回调函数。
- **`.finally()`**：无论 Promise 最终是成功还是失败都会被执行。

### Promise 的链式调用

Promise 支持链式调用，这意味着你可以连续地调用 `.then()`、`.catch()` 或 `.finally()` 方法，每个方法都返回一个新的 Promise。

```js
promise
  .then(result => {
    console.log('First then:', result);
    return 'Second then';
  })
  .then(result => {
    console.log('Second then:', result);
    return new Promise((resolve, reject) => {
      setTimeout(() => resolve('Third then'), 1000);
    });
  })
  .then(result => {
    console.log('Third then:', result);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

### Promise 的原理

1. **构造函数**：当创建一个 Promise 时，构造函数立即执行，其中包含的异步操作也会立即开始执行。
2. **状态改变**：异步操作完成后，执行器函数会调用 `resolve` 或 `reject` 函数来改变 Promise 的状态。
3. **队列机制**：所有的 `.then()`、`.catch()` 和 `.finally()` 方法都会被添加到一个队列中，等待 Promise 的状态改变后依次执行。
4. **状态不可变**：一旦 Promise 的状态被改变为 `fulfilled` 或 `rejected`，就不能再改变。因此，Promise 的队列会在状态改变时执行，不会因为后续的操作而受到影响。

### 实现细节

- **状态管理**：Promise 内部维护一个状态标志来跟踪当前状态。
- **回调注册**：Promise 在内部注册回调函数，这些函数会在状态改变时调用。
- **事件循环**：JavaScript 的事件循环机制确保 Promise 的回调函数在适当的时候被调用。

### 示例

下面是一个简单的示例，展示了如何使用 Promise 来处理异步操作。

```js
function fetchUserData(userId) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const user = { id: userId, name: 'John Doe' };
      resolve(user);
    }, 2000);
  });
}

fetchUserData(1)
  .then(user => {
    console.log('User:', user);
    return fetchUserPosts(user.id);
  })
  .then(posts => {
    console.log('Posts:', posts);
  })
  .catch(error => {
    console.error('Error:', error);
  });

function fetchUserPosts(userId) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const posts = [
        { id: 1, title: 'First post', authorId: userId },
        { id: 2, title: 'Second post', authorId: userId }
      ];
      resolve(posts);
    }, 1000);
  });
}
```

## 如何手写一个Promise功能

手写一个简易版的 `Promise` 可以帮助你更好地理解 `Promise` 的工作原理。下面是一个简化的实现，它涵盖了 `Promise` 的基本功能，包括状态管理、回调注册和异步处理。

### 简易版 `Promise` 实现

```js
class SimplePromise {
  constructor(executor) {
    this.state = 'pending'; // 初始状态
    this.value = null; // 存储成功的值
    this.reason = null; // 存储失败的原因
    this.onFulfilledCallbacks = []; // 成功回调队列
    this.onRejectedCallbacks = []; // 失败回调队列

    // resolve 函数
    const resolve = (value) => {
      if (this.state === 'pending') {
        this.state = 'fulfilled';
        this.value = value;
        this.onFulfilledCallbacks.forEach(callback => callback(value));
      }
    };

    // reject 函数
    const reject = (reason) => {
      if (this.state === 'pending') {
        this.state = 'rejected';
        this.reason = reason;
        this.onRejectedCallbacks.forEach(callback => callback(reason));
      }
    };

    try {
      executor(resolve, reject);
    } catch (error) {
      reject(error);
    }
  }

  then(onFulfilled, onRejected) {
    onFulfilled = typeof onFulfilled === 'function' ? onFulfilled : value => value;
    onRejected = typeof onRejected === 'function' ? onRejected : reason => { throw reason; };

    if (this.state === 'pending') {
      this.onFulfilledCallbacks.push(() => {
        const result = onFulfilled(this.value);
        return result instanceof SimplePromise ? result : new SimplePromise(resolve => resolve(result));
      });

      this.onRejectedCallbacks.push(() => {
        const result = onRejected(this.reason);
        return result instanceof SimplePromise ? result : new SimplePromise(reject => reject(result));
      });
    }

    if (this.state === 'fulfilled') {
      return new SimplePromise(resolve => {
        setTimeout(() => {
          try {
            const result = onFulfilled(this.value);
            resolve(result);
          } catch (error) {
            reject(error);
          }
        }, 0);
      });
    }

    if (this.state === 'rejected') {
      return new SimplePromise((resolve, reject) => {
        setTimeout(() => {
          try {
            const result = onRejected(this.reason);
            if (result instanceof SimplePromise) {
              result.then(resolve, reject);
            } else {
              reject(result);
            }
          } catch (error) {
            reject(error);
          }
        }, 0);
      });
    }
  }

  catch(onRejected) {
    return this.then(null, onRejected);
  }
}

// 使用示例
const promise = new SimplePromise((resolve, reject) => {
  setTimeout(() => {
    const success = true;
    if (success) {
      resolve('Success!');
    } else {
      reject(new Error('Failed.'));
    }
  }, 1000);
});

promise
  .then(result => {
    console.log('Result:', result);
    return 'Next step';
  })
  .then(nextStep => {
    console.log('Next step:', nextStep);
    return new SimplePromise(resolve => {
      setTimeout(() => resolve('Final step'), 1000);
    });
  })
  .then(finalStep => {
    console.log('Final step:', finalStep);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

### 说明

1. **构造函数**：接受一个执行器函数 `executor`，该函数接受 `resolve` 和 `reject` 函数作为参数。
2. **状态管理**：使用 `state` 属性来跟踪当前状态，可以是 `'pending'`、`'fulfilled'` 或 `'rejected'`。
3. **回调注册**：在 `pending` 状态下，注册成功和失败的回调函数到相应的队列中。
4. **异步处理**：使用 `setTimeout` 来模拟异步操作，确保回调函数在下一事件循环中执行。
5. **`.then()` 方法**：用于处理成功和失败的情况，返回一个新的 `SimplePromise` 实例。
6. **`.catch()` 方法**：用于处理失败的情况，简化了 `.then()` 方法的调用。

### 注意事项

- **简单实现**：这个实现非常基础，缺少一些 `Promise` 的高级功能，比如 `Promise.all`、`Promise.race` 等。
- **错误处理**：在 `then` 和 `catch` 方法中处理了异常情况，确保不会抛出未捕获的异常。
- **异步处理**：使用 `setTimeout` 来确保回调是在异步执行的，这与原生 `Promise` 的行为一致。

## Promise.all是什么

`Promise.all` 是 JavaScript 中的一个静态方法，用于等待多个 Promise 全部完成（成功或失败）。它接收一个 Promise 数组作为参数，并返回一个新的 Promise，这个新的 Promise 在所有输入的 Promises 都成功完成时解析，或者在任何一个 Promise 失败时立即拒绝。

### `Promise.all` 的工作原理

1. **成功条件**：只有当所有输入的 Promises 都成功完成时，`Promise.all` 返回的 Promise 才会解析。
2. **失败条件**：只要任何一个输入的 Promises 失败，`Promise.all` 返回的 Promise 就会立即拒绝，并且拒绝的原因是第一个失败的 Promise 的拒绝原因。
3. **返回值**：如果所有输入的 Promises 都成功，那么 `Promise.all` 返回的 Promise 的解析值是一个数组，数组中的元素是每个输入 Promise 的解析值。
4. **失败时的返回值**：如果任何一个输入的 Promises 失败，那么 `Promise.all` 返回的 Promise 的拒绝原因是第一个失败的 Promise 的拒绝原因。

### 使用示例

下面是一个简单的示例，展示了如何使用 `Promise.all` 来处理多个 Promise。

```js
function fetchUser(id) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve({ id: id, name: 'User ' + id });
    }, 1000);
  });
}

function fetchPosts(id) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve([
        { id: id, title: 'Post ' + id },
        { id: id + 1, title: 'Post ' + (id + 1) }
      ]);
    }, 1500);
  });
}

// 使用 Promise.all
Promise.all([fetchUser(1), fetchPosts(1)])
  .then(results => {
    const [user, posts] = results;
    console.log('User:', user);
    console.log('Posts:', posts);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

### 详细解释

在这个示例中，我们定义了两个函数 `fetchUser` 和 `fetchPosts`，分别用于模拟异步获取用户信息和帖子信息。我们使用 `Promise.all` 来等待这两个 Promise 都完成。

1. **创建 Promise 数组**：我们将 `fetchUser(1)` 和 `fetchPosts(1)` 的结果放入一个数组中。
2. **调用 `Promise.all`**：将 Promise 数组传递给 `Promise.all`。
3. 处理结果：
   - **成功时**：当所有 Promise 都成功完成时，`Promise.all` 返回的 Promise 会解析，解析值是一个数组，数组中的元素分别是每个输入 Promise 的解析值。
   - **失败时**：如果任何一个 Promise 失败，`Promise.all` 返回的 Promise 会立即拒绝，并且拒绝的原因是第一个失败的 Promise 的拒绝原因。

### 总结

- **`Promise.all`**：用于等待多个 Promise 全部完成。
- **成功条件**：所有输入的 Promises 都成功完成。
- **失败条件**：任何一个输入的 Promises 失败。
- **返回值**：成功时返回一个包含所有输入 Promises 解析值的数组；失败时返回一个被拒绝的 Promise。

## 手写一个Promise.all

手写一个 `Promise.all` 方法可以帮助你更好地理解其内部工作机制。下面是一个简单的实现示例，它涵盖了 `Promise.all` 的基本功能。

### 手写 `Promise.all`

```js
function myPromiseAll(promises) {
  return new Promise((resolve, reject) => {
    // 用于存储每个 Promise 的解析结果
    const results = [];

    // 用于跟踪已完成的 Promise 的数量
    let completedCount = 0;

    // 遍历输入的 Promise 数组
    promises.forEach((promise, index) => {
      promise
        .then((result) => {
          // 当一个 Promise 成功时，存储结果
          results[index] = result;

          // 增加已完成的 Promise 的计数
          completedCount++;

          // 如果所有 Promise 都已完成，则解析 `Promise.all` 返回的 Promise
          if (completedCount === promises.length) {
            resolve(results);
          }
        })
        .catch((error) => {
          // 如果任何一个 Promise 失败，则立即拒绝 `Promise.all` 返回的 Promise
          reject(error);
        });
    });
  });
}

// 使用示例
function fetchUser(id) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve({ id: id, name: 'User ' + id });
    }, 1000);
  });
}

function fetchPosts(id) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve([
        { id: id, title: 'Post ' + id },
        { id: id + 1, title: 'Post ' + (id + 1) }
      ]);
    }, 1500);
  });
}

// 使用 hand-written `myPromiseAll`
myPromiseAll([fetchUser(1), fetchPosts(1)])
  .then(results => {
    const [user, posts] = results;
    console.log('User:', user);
    console.log('Posts:', posts);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

### 详细解释

1. **创建新的 Promise**：`myPromiseAll` 函数接收一个 Promise 数组，并返回一个新的 Promise。
2. **结果存储**：使用一个数组 `results` 来存储每个输入 Promise 的解析结果。
3. **计数器**：使用一个变量 `completedCount` 来跟踪已完成的 Promise 的数量。
4. **遍历 Promise 数组**：遍历输入的 Promise 数组，并对每个 Promise 使用 `.then()` 和 `.catch()` 方法。
5. 处理成功：
   - 当一个 Promise 成功时，将其解析结果存入 `results` 数组中。
   - 增加 `completedCount` 的值。
   - 如果所有 Promise 都已完成（即 `completedCount` 等于输入的 Promise 数组的长度），则解析 `myPromiseAll` 返回的 Promise，解析值为 `results` 数组。
6. 处理失败：
   - 如果任何一个 Promise 失败，则立即拒绝 `myPromiseAll` 返回的 Promise，拒绝的原因是第一个失败的 Promise 的拒绝原因。

### 注意事项

- **简单实现**：这个实现非常基础，没有处理一些特殊情况，比如输入的数组为空或者输入的数组包含非 Promise 的值。
- **错误处理**：在 `.catch()` 方法中处理了异常情况，确保不会抛出未捕获的异常。

## 什么是防抖？什么是节流？二者有什么区别

防抖（Debounce）和节流（Throttle）是两种常见的JavaScript技术，用于控制函数的调用频率，以提高性能和用户体验。

### 防抖（Debounce）

防抖的主要目的是防止函数在短时间内被频繁调用。它确保函数在一系列调用中只执行一次，通常是在最后一次调用后的一定延迟时间内。

#### 工作原理

- 当触发事件时，防抖函数开始计时。
- 如果在计时期间再次触发事件，则重新开始计时。
- 只有在最后一次触发事件后过了设定的时间间隔，防抖函数才会执行。
- 如果在计时期间没有新的触发事件，则在计时期满后执行函数。

#### 用途

- 输入框的实时搜索建议。
- 调整窗口大小时更新布局。
- 频繁触发的事件，如键盘输入、鼠标移动等。

#### 示例

```js
function debounce(func, wait) {
  let timeout;
  return function() {
    const context = this;
    const args = arguments;
    clearTimeout(timeout);
    timeout = setTimeout(function() {
      func.apply(context, args);
    }, wait);
  };
}

// 使用示例
const searchInput = document.getElementById('search-input');
searchInput.addEventListener('input', debounce(function(event) {
  console.log('Search input changed:', event.target.value);
}, 300));
```

### 节流（Throttle）

节流是为了限制函数的执行频率，确保函数在固定的时间间隔内最多只能执行一次。

#### 工作原理

- 无论事件触发多少次，函数都会按照固定的间隔执行。
- 如果在设定的时间间隔内多次触发事件，函数只会执行一次。
- 在时间间隔过后，函数会准备好再次被调用。

#### 用途

- 拖动操作，如拖动文件或调整窗口大小。
- 高频触发的事件，如滚动、鼠标移动等。

#### 示例

```js
function throttle(func, limit) {
  let inThrottle;
  return function() {
    const args = arguments;
    const context = this;
    if (!inThrottle) {
      func.apply(context, args);
      inThrottle = true;
      setTimeout(function() {
        inThrottle = false;
      }, limit);
    }
  };
}

// 使用示例
const resizeHandler = throttle(function() {
  console.log('Window resized');
}, 250);

window.addEventListener('resize', resizeHandler);
```

### 防抖与节流的区别

- **防抖**：确保函数在一系列连续触发事件后只执行一次，通常在最后一次触发事件后的延迟时间内执行。
- **节流**：确保函数在固定的时间间隔内最多只能执行一次，即使在这段时间内事件被多次触发。

### 总结

- **防抖**：用于处理需要在一段时间内的最后一个动作上执行的操作。
- **节流**：用于限制函数的执行频率，确保函数在固定的时间间隔内最多只能执行一次。

选择使用防抖还是节流取决于具体的使用场景。如果你的应用需要确保在用户停止某种操作后才执行某项任务，那么应该使用防抖。如果需要限制某个操作的执行频率，比如在用户滚动页面时限制更新视图的频率，那么应该使用节流。

## Generator 是怎么样使用的以及各个阶段的变化如何

Generator 函数是ES6中引入的一种特殊类型的函数，它允许函数暂停执行并在需要时恢复执行。Generator 函数可以生成一系列值，并且可以接收外部传入的值。它们在异步编程和控制流方面非常有用。

### Generator 函数的特点

- **使用 `function\*` 定义**：使用 `function*` 关键字定义 Generator 函数。
- **使用 `yield` 语句**：Generator 函数内部使用 `yield` 语句来产生值。
- **可以多次调用**：Generator 函数可以多次调用，每次调用都会从上次停止的地方继续执行。

### 使用 Generator 函数

#### 定义 Generator 函数

```js
function* myGenerator() {
    yield 1; // 第一次调用 next() 时返回的值
    yield 2; // 第二次调用 next() 时返回的值
    return 'done'; // 可选的返回值
}
```

#### 调用 Generator 函数

```js
const gen = myGenerator();
```

#### 使用 `.next()` 方法

- **`.next()` 方法**：调用 `.next()` 方法来执行 Generator 函数直到下一个 `yield` 语句或函数结束。
- 返回值：`.next()`方法返回一个对象，该对象有两个属性：
  - `value`：生成的值。
  - `done`：布尔值，表示是否已经到了 Generator 函数的末尾。

**示例**

```js
function* countUpTo(n) {
    for (let i = 1; i <= n; i++) {
        yield i;
    }
}

const counter = countUpTo(5);

console.log(counter.next()); // { value: 1, done: false }
console.log(counter.next()); // { value: 2, done: false }
console.log(counter.next()); // { value: 3, done: false }
console.log(counter.next()); // { value: 4, done: false }
console.log(counter.next()); // { value: 5, done: false }
console.log(counter.next()); // { value: undefined, done: true }
```

### Generator 函数的状态变化

1. **初始状态**：
   - Generator 函数被定义，但尚未执行。
   - 调用 `function*` 定义的函数会返回一个 Iterator 对象。
2. **执行状态**：
   - 调用 `.next()` 方法来开始执行 Generator 函数。
   - 执行到第一个 `yield` 语句时暂停，并返回 `yield` 的值。
3. **暂停状态**：
   - 每次调用 `.next()` 方法都会执行到下一个 `yield` 语句。
   - 如果没有更多的 `yield` 语句，Generator 函数会执行到结束。
4. **完成状态**：
   - 当 Generator 函数执行到结束或到达 `return` 语句时，`done` 属性变为 `true`。
   - 之后再次调用 `.next()` 方法时，`value` 为 `undefined`，`done` 为 `true`。

### 通过 `.next()` 传值

你可以通过 `.next()` 方法的参数向 Generator 函数内部传值。

**示例**

```js
function* askForInput() {
    let input = yield 'What is your name? ';
    console.log(`Hello, ${input}!`);

    input = yield 'How old are you? ';
    console.log(`So you are ${input} years old.`);
}

const conversation = askForInput();

console.log(conversation.next().value); // What is your name? 
console.log(conversation.next('Alice').value); // How old are you? 
console.log(conversation.next(30).value); // undefined
console.log(conversation.next().done); // true
```

### 总结

- **定义**：使用 `function*` 定义 Generator 函数。
- **执行**：通过 `.next()` 方法执行 Generator 函数。
- **状态**：Generator 函数的状态包括初始、执行、暂停和完成。
- **传值**：通过 `.next()` 方法的参数向 Generator 函数内部传值。

## 讲讲JavaScript垃圾回收是怎么做的

JavaScript的垃圾回收机制负责自动管理内存，确保不再使用的内存能够被及时释放。垃圾回收的主要目标是回收不再被程序引用的对象所占用的内存空间。下面是关于JavaScript垃圾回收的一些关键概念和机制。

### JavaScript中的垃圾回收机制

JavaScript的垃圾回收主要依赖于两种机制：标记-清除（Mark and Sweep）和引用计数（Reference Counting）。

#### 1. 标记-清除（Mark and Sweep）

标记-清除算法是最常见的垃圾回收算法之一。它分为两个阶段：标记和清除。

- **标记**：垃圾回收器遍历所有可达对象，并标记这些对象。可达对象是指可以从根节点（如全局对象、活动对象等）直接或间接访问到的对象。
- **清除**：垃圾回收器清理未被标记的对象，即认为这些对象已经不再被使用，可以安全地回收它们占用的内存。

#### 2. 引用计数（Reference Counting）

引用计数是一种早期的垃圾回收策略，它记录每个对象被引用的次数。当一个对象的引用计数变为零时，该对象就可以被回收。

然而，JavaScript引擎很少单独使用引用计数，因为它无法处理循环引用的问题。在循环引用的情况下，即使对象不再被需要，它们之间的相互引用也会导致引用计数始终大于零，从而阻止垃圾回收器回收这些对象。

### JavaScript中的垃圾回收算法

现代JavaScript引擎通常使用更高级的垃圾回收算法，如分代收集（Generational Collection）、增量标记（Incremental Marking）等。

#### 3. 分代收集（Generational Collection）

分代收集假设对象越年轻，它成为垃圾的可能性越大。基于这个假设，JavaScript引擎将对象划分为不同的代，新创建的对象放在年轻代，经过一段时间存活下来的对象会被移动到老年代。

- **年轻代**：对象生命周期较短的对象存储在这里。年轻代的垃圾回收频率较高。
- **老年代**：长期存活的对象存储在这里。老年代的垃圾回收频率较低。

#### 4. 增量标记（Incremental Marking）

增量标记是一种优化技术，它将标记阶段分成多个较小的任务，这些任务可以在其他JavaScript任务之间执行。这种方式减少了标记阶段对应用程序性能的影响。

### 垃圾回收的触发时机

JavaScript的垃圾回收机制通常是自动触发的，但也可以通过以下方式显式触发：

- **手动触发**：在V8引擎中，可以使用 `gc()` 函数手动触发垃圾回收。但这不是标准JavaScript的一部分，通常不建议使用。
- **自动触发**：当内存占用达到一定阈值时，JavaScript引擎会自动触发垃圾回收。

### 如何帮助垃圾回收

虽然JavaScript的垃圾回收机制是自动的，但开发者可以通过以下方式帮助提高垃圾回收的效率：

- **及时解除引用**：当不再需要一个对象时，显式地将其引用设置为 `null` 或者其他值，帮助垃圾回收器更快地识别无用对象。
- **避免循环引用**：确保对象之间没有不必要的循环引用。
- **使用弱引用**：某些JavaScript引擎支持弱引用，可以用来避免循环引用问题。

### 总结

- **标记-清除**：最常用的垃圾回收算法，分为标记和清除两个阶段。
- **分代收集**：基于对象的生命周期将对象划分成不同的代，年轻代的对象更容易成为垃圾。
- **增量标记**：将标记阶段分解为多个小任务，减少对应用程序性能的影响。
- **手动触发**：虽然可以手动触发垃圾回收，但这通常不是最佳实践。

> 原理解析请移步[JavaScript内存管理](#memory.md)

---

## 说说你对代理的理解

代理（Proxy）是ECMAScript 6 (ES6) 引入的一个强大特性，它允许你在访问一个对象时拦截并定制基本操作。代理可以用于对象、数组、函数等任何类型的数据。通过代理，你可以实现各种高级功能，如数据验证、性能监控、记录访问等。

### 代理的基本概念

- **代理对象**：一个由 `new Proxy(target, handler)` 创建的对象，它作为目标对象的代理。
- **目标对象**：你希望代理的对象。
- **处理器对象**（handler）：一个包含了代理行为的方法的对象。

### 代理的工作原理

当你创建一个代理对象时，你需要传递两个参数：

1. **目标对象**：你想要代理的对象。
2. **处理器对象**：一个包含了代理行为的方法的对象，这些方法定义了代理对象如何响应特定的操作。

### 代理的方法

代理可以通过定义处理器对象中的方法来拦截和自定义目标对象的行为。以下是常用的代理方法：

- **`get`**：拦截对象属性的读取操作。
- **`set`**：拦截对象属性的赋值操作。
- **`has`**：拦截 `in` 操作符，检查对象中是否存在某个属性。
- **`deleteProperty`**：拦截 `delete` 操作符。
- **`apply`**：拦截函数的调用、`call` 和 `apply`。
- **`construct`**：拦截 `new` 关键字的构造函数调用。
- **`ownKeys`**：拦截 `Object.getOwnPropertyNames`、`Object.getOwnPropertySymbols` 和 `Object.keys` 方法。
- **`getOwnPropertyDescriptor`**：拦截 `Object.getOwnPropertyDescriptor` 方法。
- **`defineProperty`**：拦截 `Object.defineProperty` 和 `Object.defineProperties` 方法。
- **`preventExtensions`**：拦截 `Object.preventExtensions` 方法。
- **`getPrototypeOf`**：拦截 `Object.getPrototypeOf` 方法。
- **`isExtensible`**：拦截 `Object.isExtensible` 方法。
- **`setPrototypeOf`**：拦截 `Object.setPrototypeOf` 方法。

### 示例

下面是一个简单的示例，演示了如何使用代理来拦截对象的属性访问和修改：

```js
const target = {
  message: 'Hello, world!'
};

const handler = {
  get: function(target, prop, receiver) {
    console.log(`Getting ${prop}`);
    return Reflect.get(target, prop, receiver);
  },
  set: function(target, prop, value, receiver) {
    console.log(`Setting ${prop} to ${value}`);
    return Reflect.set(target, prop, value, receiver);
  }
};

const proxy = new Proxy(target, handler);

console.log(proxy.message); // 输出: Getting message
                            //        Hello, world!

proxy.message = 'Hello, ES6!';
// 输出: Setting message to Hello, ES6!
console.log(proxy.message); // 输出: Getting message
                            //        Hello, ES6!
```

### 重要注意事项

- **`Reflect` API**：代理中的大多数方法都有一个对应的 `Reflect` 方法，这些方法可以用来执行原本的操作，而不经过拦截。
- **性能考虑**：虽然代理提供了强大的功能，但过度使用代理可能会导致性能下降，尤其是在频繁访问或修改大量属性的情况下。
- **调试**：使用代理可能会使调试变得复杂，因为代理操作可能会隐藏原始对象的真实行为。

### 总结

- **代理**：允许你拦截并自定义对象的基本操作。
- **目标对象**：你想要代理的对象。
- **处理器对象**：定义了代理行为的方法的对象。
- **方法**：如 `get`、`set` 等方法用于定义代理行为。
- **应用**：Vue2 的双向绑定 vue2 用的是`Object.defineProperty`，vue3 用的是`proxy`。

## 函数柯里化是什么

函数柯里化（Currying）是一种将多参数函数转换为一系列单参数函数的技术。这种技术允许我们将一个函数拆分成多个步骤，每次调用时只提供一部分参数，直到所有的参数都被提供后才执行原始函数。柯里化的主要目的是提高函数的灵活性和重用性。

### 柯里化的定义

柯里化是指将一个多参数函数转换为一系列单参数函数的过程。例如，一个接受两个参数的函数 `f(x, y)` 可以被柯里化为 `f(x)(y)`，其中 `f(x)` 返回一个新的函数，该函数接受剩余的参数 `y` 并执行原始函数。

### 柯里化的用途

- **函数重用**：通过柯里化，可以创建部分应用的函数，这些函数可以重用并组合成更复杂的函数。
- **代码简洁**：可以减少不必要的参数传递，使得代码更加简洁和易于理解。
- **延迟执行**：允许将函数的调用延迟到所有参数都准备好时再执行。
- **参数预设**：可以在某些情况下提前设定某些参数，以便后续调用时不需要重复提供这些参数。

### 柯里化的实现

下面是一个简单的示例，展示了如何实现柯里化：

```js
function curry(fn) {
  const arity = fn.length; // 获取原始函数的参数个数
  return function curried(...args) {
    if (args.length >= arity) {
      return fn(...args); // 如果参数个数足够，执行原始函数
    } else {
      return function(...moreArgs) {
        return curried(...args, ...moreArgs); // 否则返回一个新的函数
      };
    }
  };
}

// 使用示例
function add(x, y, z) {
  return x + y + z;
}

const curriedAdd = curry(add);

console.log(curriedAdd(1)(2)(3)); // 输出: 6
console.log(curriedAdd(1, 2)(3)); // 输出: 6
console.log(curriedAdd(1)(2, 3)); // 输出: 6
console.log(curriedAdd(1, 2, 3)); // 输出: 6
```

### 详细解释

1. **定义柯里化函数**：`curry` 函数接收一个原始函数 `fn`。
2. **确定参数个数**：使用 `fn.length` 获取原始函数期望的参数个数。
3. **返回新的函数**：`curried` 函数接收当前传入的参数 `args`。
4. **判断参数个数**：
   - 如果提供的参数个数等于或大于原始函数期望的参数个数，则直接执行原始函数。
   - 如果提供的参数个数不足，则返回一个新的函数，该函数接受剩余的参数，并递归地调用自身，直到参数个数满足要求。
5. **使用示例**：通过不同的调用方式演示柯里化的灵活性。

### 总结

- **柯里化**：将多参数函数转换为一系列单参数函数的技术。
- **用途**：提高函数的灵活性和重用性。
- **实现**：通过递归地返回函数来实现。

## 什么是requestAnimationFrame

`requestAnimationFrame`（简称 `raf`）是JavaScript中的一种API，用于在浏览器的下一帧之前请求执行动画。它提供了一种高效的方式来更新用户界面，并且能够与浏览器的刷新率同步，从而提高动画的平滑度和性能。

### `requestAnimationFrame` 的工作原理

`requestAnimationFrame` 允许开发者告诉浏览器他们希望执行一个动画，并请求浏览器在下次重绘之前调用指定的函数来更新动画。这种方法比使用 `setTimeout` 或 `setInterval` 更高效，因为它与浏览器的刷新率同步。

### 使用示例

下面是一个简单的使用 `requestAnimationFrame` 的示例，用于更新一个元素的位置来实现动画效果。

```js
const element = document.getElementById('moving-element');
let position = 0;

function animate() {
  position += 1;
  element.style.transform = `translateX(${position}px)`;

  if (position < 500) {
    requestAnimationFrame(animate); // 请求下一帧继续动画
  }
}

animate(); // 开始动画
```

### 详细解释

1. **获取元素**：获取要移动的元素。
2. **定义动画函数**：定义一个名为 `animate` 的函数，用于更新元素的位置。
3. **更新位置**：每次调用 `animate` 时，元素的位置都会增加 1px。
4. **调用 `requestAnimationFrame`**：在动画函数内部调用 `requestAnimationFrame` 来请求下一帧继续动画。
5. **检查条件**：如果位置小于 500px，则继续动画。否则动画结束。

### 特点

- **与刷新率同步**：`requestAnimationFrame` 与浏览器的刷新率（通常是 60fps）同步，这意味着它会在每一帧之前调用动画函数。
- **高效**：浏览器会自动优化动画帧的调用，以确保最佳性能。
- **暂停和恢复**：当浏览器标签页不在活动状态时，`requestAnimationFrame` 会自动暂停，从而节省资源。

### 与 `setTimeout` 和 `setInterval` 的比较

- **`setTimeout`**：可以指定延迟时间后调用函数，但无法保证与浏览器刷新率同步。
- **`setInterval`**：定期调用函数，但可能导致性能问题，因为它不考虑浏览器的实际刷新率。
- **`requestAnimationFrame`**：与浏览器刷新率同步，自动优化调用频率，更适合动画。

### 取消动画

如果你需要取消正在进行的动画，可以使用 `cancelAnimationFrame`。你需要保存 `requestAnimationFrame` 返回的标识符，然后在需要时使用该标识符来取消动画。

**示例**

```js
let requestId;

function startAnimation() {
  requestId = requestAnimationFrame(animate);
}

function stopAnimation() {
  cancelAnimationFrame(requestId);
}

startAnimation(); // 开始动画
// ...
stopAnimation(); // 停止动画
```

### 总结

- **`requestAnimationFrame`**：用于在浏览器的下一帧之前请求执行动画。
- **与刷新率同步**：与浏览器的刷新率同步，提高动画的平滑度和性能。
- **高效**：自动优化动画帧的调用，节省资源。
- **取消动画**：使用 `cancelAnimationFrame` 来取消正在进行的动画。

##  JS 性能优化的方式有哪些

avaScript 性能优化是一个广泛的话题，涉及到多个方面，包括代码编写、运行时性能、内存管理以及DOM操作等。下面是一些常用的JavaScript性能优化方法：

### 1. 代码层面的优化

- 减少全局作用域查找：
  - 使用局部变量而非全局变量。
  - 缓存对经常访问的对象的引用。
- 避免不必要的类型转换：
  - 明确地指定数据类型，减少隐式转换。
- 使用更高效的算法：
  - 选择复杂度更低的算法。
  - 避免重复计算，比如使用缓存技术。
- 循环优化：
  - 尽可能减少循环内的工作量。
  - 避免在循环内进行函数调用。
  - 使用 `for` 循环替代 `forEach` 或其他高阶函数，除非后者提供了更好的可读性和维护性。
- 尽早退出函数：
  - 如果函数中有条件可以提前返回，那么应该尽早返回以减少不必要的计算。

### 2. DOM 操作优化

- 减少DOM操作：
  - 尽量减少直接修改DOM的次数。
  - 批量修改DOM，使用文档片段（DocumentFragment）来构建复杂的DOM结构，然后一次性添加到页面上。
- 避免重排和重绘：
  - 使用CSS3硬件加速属性（如 transform 和 opacity）来减少重绘。
  - 避免修改样式属性，而是使用类来控制样式。
- 使用事件代理：
  - 对于大量相似元素的事件处理，可以使用事件代理（event delegation）来绑定事件监听器到父级元素上。

### 3. 异步编程

- 异步加载资源：
  - 使用 `async`/`defer` 属性来异步加载脚本文件。
- 非阻塞UI：
  - 使用 `Promise`、`async/await` 进行异步操作，避免长时间阻塞主线程。
- Web Workers：
  - 对于一些耗时的任务，可以在后台线程中处理，使用 Web Workers。

### 4. 内存管理

- 及时释放不再使用的对象：
  - 释放引用，让垃圾回收机制能够清理不再使用的对象。
- 避免内存泄漏：
  - 注意闭包中的变量引用。
  - 清除定时器和其他监听器。

### 5. 利用浏览器特性

- 使用 `requestAnimationFrame`：
  - 对于动画，使用 `requestAnimationFrame` 而不是 `setTimeout` 或 `setInterval`。
- 利用浏览器缓存：
  - 设置合适的HTTP缓存策略，减少网络请求。

### 6. 使用现代JavaScript特性和工具

- ES6+ 特性：
  - 使用新的语言特性如箭头函数、解构赋值、模板字符串等，这些通常更高效。
- 模块化：
  - 使用模块系统（如 ES6 modules）来组织代码，减少全局作用域的污染。
- 树摇动：
  - 使用支持“tree shaking”的打包工具（如 Rollup），可以移除未使用的代码。

### 7. 使用性能分析工具

- Chrome DevTools：
  - 使用 Chrome DevTools 中的 Performance 面板来分析性能瓶颈。
- Lighthouse：
  - 使用 Lighthouse 来评估页面的整体性能并获得改进建议。

### 8. 代码压缩与合并

- 压缩和混淆：
  - 在生产环境中使用压缩过的代码，减少下载时间。
- 合并文件：
  - 合并多个小文件以减少HTTP请求的数量。

### 9. 懒加载

- 按需加载：
  - 使用懒加载技术来延迟加载非关键资源（如图片和视频）。

### 10. CDN 使用

- 使用CDN：
  - 利用内容分发网络（CDN）来加快资源加载速度。

## js延迟加载的方式有哪些

JavaScript 延迟加载（也称为懒加载或异步加载）是一种优化技术，用于在用户真正需要时才加载某些脚本或资源，而不是在页面加载时就立即加载所有内容。这种方法可以显著提高页面的初始加载速度，因为减少了初始加载时需要下载的数据量。以下是几种常见的 JavaScript 延迟加载方式：

### 1. 动态插入 `<script>` 标签

这种方法可以通过 JavaScript 动态创建 `<script>` 标签，并将其插入到文档中。当用户滚动到页面的某个部分或触发某个事件时，脚本会被加载。

```js
function loadScript(url, callback) {
    var script = document.createElement('script');
    script.type = 'text/javascript';
    if (script.readyState) {  // IE
        script.onreadystatechange = function () {
            if (script.readyState === 'loaded' || script.readyState === 'complete') {
                script.onreadystatechange = null;
                callback();
            }
        };
    } else {  // Others
        script.onload = function () {
            callback();
        };
    }
    script.src = url;
    document.getElementsByTagName('head')[0].appendChild(script);
}

// 使用示例
loadScript('https://example.com/some-script.js', function() {
    console.log('Script loaded and executed.');
});
```

### 2. 使用 `async` 和 `defer` 属性

HTML `<script>` 标签支持 `async` 和 `defer` 属性，这两个属性可以让浏览器异步加载脚本。

- **`async`**：脚本会在下载完成后立即执行，不保证按照顺序执行。
- **`defer`**：脚本会等到整个页面解析完成后再执行，并且保证按照在文档中的顺序执行。

```js
<script src="https://example.com/some-script.js" async></script>
<script src="https://example.com/some-other-script.js" defer></script>
```

### 3. 使用 JavaScript 模块 (`import()`)

ES6 模块引入了动态导入功能，允许你在运行时按需加载模块。

```js
document.addEventListener('DOMContentLoaded', function() {
    import('./lazy-loaded-module.js').then(function(module) {
        module.default();  // 调用模块的默认导出函数
    });
});
```

### 4. 使用 AJAX 请求

你可以通过 AJAX 请求来获取外部脚本的内容，然后将其作为字符串插入到一个新的 `<script>` 标签中。

```js
function loadScriptViaAjax(url, callback) {
    var xhr = new XMLHttpRequest();
    xhr.open('GET', url, true);
    xhr.onreadystatechange = function () {
        if (xhr.readyState === 4 && xhr.status === 200) {
            var script = document.createElement('script');
            script.innerHTML = xhr.responseText;
            document.body.appendChild(script);
            if (callback) {
                callback();
            }
        }
    };
    xhr.send();
}

// 使用示例
loadScriptViaAjax('https://example.com/some-script.js', function() {
    console.log('Script loaded via AJAX.');
});
```

### 5. 使用 Web Workers

对于一些耗时的任务，可以在后台线程中处理，使用 Web Workers 来异步加载和执行脚本。

```js
var worker = new Worker('worker.js');

worker.onmessage = function(event) {
    console.log('Message received from the worker:', event.data);
};

worker.postMessage({ data: 'Hello from main thread!' });
```

### 6. 使用事件监听器

可以监听用户的交互事件（如点击按钮或滚动到页面的特定部分），然后在这些事件发生时加载脚本。

```js
window.addEventListener('scroll', function() {
    if (isElementInViewport('#some-element')) {
        loadScript('https://example.com/some-script.js', function() {
            console.log('Script loaded on scroll.');
        });
    }
});

function isElementInViewport(selector) {
    var rect = document.querySelector(selector).getBoundingClientRect();
    return (
        rect.top >= 0 &&
        rect.left >= 0 &&
        rect.bottom <= (window.innerHeight || document.documentElement.clientHeight) &&
        rect.right <= (window.innerWidth || document.documentElement.clientWidth)
    );
}
```

### 7. 使用第三方库

有些库专门用于实现懒加载，例如 `lazysizes` 或 `lozad.js`，它们可以帮助你轻松地实现图片和脚本的懒加载。

## 请解释一下 JavaScript的同源策略

JavaScript 的同源策略（Same-Origin Policy）是一种安全措施，用于限制一个来源的脚本与另一个来源的脚本之间的交互。这个策略旨在保护用户的隐私和数据安全，防止恶意脚本从一个来源获取或修改另一个来源的数据。

### 同源策略的基本概念

同源策略规定，来自不同来源的脚本不能相互访问或修改对方的资源，除非明确允许。这里的“来源”通常指的是协议、域名和端口的组合。如果两个脚本具有相同的协议、域名和端口，则它们被认为是同源的。

### 来源的定义

来源（origin）由以下三个部分组成：

- **协议**：如 HTTP、HTTPS。
- **域名**：如 example.com、sub.example.com。
- **端口**：如 80、443、8080。

### 同源策略的规则

- **读写限制**：来自不同来源的脚本不能读取或修改另一个来源的文档或DOM元素。
- **跨域资源共享**（CORS）：通过服务器设置适当的HTTP头部信息，可以允许跨源请求。
- **JSONP**：使用 JSONP 技术可以在一定程度上绕过同源策略限制，但只能用于 GET 请求。

### 示例

假设有两个来源：

- **来源 A**：`http://example.com:8080`
- **来源 B**：`https://example.com:80`

根据同源策略，来源 A 的脚本不能访问来源 B 的资源，反之亦然。

### 实现细节

- **DOM 访问**：来自不同来源的脚本不能访问另一个来源的DOM节点。
- **XMLHttpRequest**：默认情况下，XMLHttpRequest 只能在同源情况下发送请求。通过设置 CORS 头部，可以允许跨源请求。
- **WebSocket**：WebSocket 也遵循同源策略，但可以通过服务器设置允许跨源连接。
- **Web Storage**：LocalStorage 和 SessionStorage 也遵循同源策略。

### 允许跨源访问的方法

- **CORS**（Cross-Origin Resource Sharing）：通过设置HTTP头部来允许跨源请求。
- **JSONP**：使用脚本标签和回调函数实现跨源数据请求，但只限于 GET 请求。
- **PostMessage**：允许不同来源的窗口之间进行通信。
- **Service Workers**：可以配置为代理跨源请求。

### 例外情况

尽管同源策略限制了不同来源之间的交互，但也有一些例外情况：

- **`<img>`、`<link>` 和 `<script>` 标签**：这些标签可以加载不同来源的资源。
- **`<iframe>`**：可以通过设置 `sandbox` 属性和 `allow` 属性来控制子框架的权限。

### 示例

下面是一个简单的示例，展示了如何通过CORS允许跨源请求。

#### 服务器端（Node.js）

```js
const express = require('express');
const app = express();

app.use((req, res, next) => {
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
    next();
});

app.get('/api/data', (req, res) => {
    res.json({ message: 'This is cross-origin data.' });
});

app.listen(3000, () => console.log('Server started on port 3000'));
```

#### 客户端

```js
fetch('http://localhost:3000/api/data')
    .then(response => response.json())
    .then(data => console.log(data));
```

**总结**

- **同源策略**：限制不同来源的脚本之间的交互。
- **来源定义**：由协议、域名和端口组成。
- **允许跨源访问**：通过 CORS、JSONP、PostMessage 等技术实现。

 ## 手写浅拷贝

```js
// ----------------------------------------------浅拷贝
    // 只是把对象的属性和属性值拷贝到另一个对象中
    var obj1 = {
      a: {
        a1: { a2: 1 },
        a10: { a11: 123, a111: { a1111: 123123 } }
      },
      b: 123,
      c: "123"
    }
    // 方式1
    function shallowClone1(o) {
      let obj = {}
 
      for (let i in o) {
        obj[i] = o[i]
      }
      return obj
    }
 
    // 方式2
    var shallowObj2 = { ...obj1 }
 
    // 方式3
    var shallowObj3 = Object.assign({}, obj1)
 
    let shallowObj = shallowClone1(obj1);
 
    shallowObj.a.a1 = 999
    shallowObj.b = true
 
    console.log(obj1);  //第一层的没有被改变，一层以下就被改变了
```

## 手写深拷贝

```js
// ----------------------------------------------深拷贝
 
    // 简易版  
    function deepClone(o) {
      let obj = {}
      for (var i in o) {
        // if(o.hasOwnProperty(i)){
        if (typeof o[i] === "object") {
          obj[i] = deepClone(o[i])
        } else {
          obj[i] = o[i]
        }
        // }
      }
      return obj
    }
 
 
    var myObj = {
      a: {
        a1: { a2: 1 },
        a10: { a11: 123, a111: { a1111: 123123 } }
      },
      b: 123,
      c: "123"
    }
 
    var deepObj1 = deepClone(myObj)
    deepObj1.a.a1 = 999
    deepObj1.b = false
    console.log(myObj);
 
 
 
    // 简易版存在的问题：参数没有做检验，传入的可能是 Array、null、regExp、Date
    function deepClone2(o) {
      if (Object.prototype.toString.call(o) === "[object Object]") {  //检测是否为对象
        let obj = {}
        for (var i in o) {
          if (o.hasOwnProperty(i)) {
            if (typeof o[i] === "object") {
              obj[i] = deepClone(o[i])
            } else {
              obj[i] = o[i]
            }
          }
        }
        return obj
      } else {
        return o
      }
    }
 
    function isObject(o) {
      return Object.prototype.toString.call(o) === "[object Object]" || Object.prototype.toString.call(o) === "[object Array]"
    }
 
    // 继续升级，没有考虑到数组，以及ES6中的map、set、weakset、weakmap
    function deepClone3(o) {
      if (isObject(o)) {//检测是否为对象或者数组
        let obj = Array.isArray(o) ? [] : {}
        for (let i in o) {
          if (isObject(o[i])) {
            obj[i] = deepClone(o[i])
          } else {
            obj[i] = o[i]
          }
        }
        return obj
      } else {
        return o
      }
    }
 
 
    // 有可能碰到循环引用问题  var a = {}; a.a = a; clone(a);//会造成一个死循环
    // 循环检测
    // 继续升级
    function deepClone4(o, hash = new map()) {
      if (!isObject(o)) return o//检测是否为对象或者数组
      if (hash.has(o)) return hash.get(o)
      let obj = Array.isArray(o) ? [] : {}
 
      hash.set(o, obj)
      for (let i in o) {
        if (isObject(o[i])) {
          obj[i] = deepClone4(o[i], hash)
        } else {
          obj[i] = o[i]
        }
      }
      return obj
    }
 
    // 递归易出现爆栈问题
    //  将递归改为循环，就不会出现爆栈问题了
    var a1 = { a: 1, b: 2, c: { c1: 3, c2: { c21: 4, c22: 5 } }, d: 'asd' };
    var b1 = { b: { c: { d: 1 } } }
    function cloneLoop(x) {
      const root = {};
      // 栈 
      const loopList = [  //->[]->[{parent:{a:1,b:2},key:c,data:{ c1: 3, c2: { c21: 4, c22: 5 } }}]
        {
          parent: root,
          key: undefined,
          data: x,
        }
      ];
      while (loopList.length) {
        // 深度优先
        const node = loopList.pop();
        const parent = node.parent; //{} //{a:1,b:2}
        const key = node.key; //undefined //c
        const data = node.data; //{ a: 1, b: 2, c: { c1: 3, c2: { c21: 4, c22: 5 } }, d: 'asd' }  //{ c1: 3, c2: { c21: 4, c22: 5 } }}
        // 初始化赋值目标，key 为 undefined 则拷贝到父元素，否则拷贝到子元素
        let res = parent; //{}->{a:1,b:2,d:'asd'} //{a:1,b:2}->{}
        if (typeof key !== 'undefined') {
          res = parent[key] = {};
        }
        for (let k in data) {
          if (data.hasOwnProperty(k)) {
            if (typeof data[k] === 'object') {
              // 下一次循环 
              loopList.push({
                parent: res,
                key: k,
                data: data[k],
              })
            } else {
              res[k] = data[k];
            }
          }
        }
      }
      return root
    }
 
 
    function deepClone5(o) {
      let result = {}
      let loopList = [
        {
          parent: result,
          key: undefined,
          data: o
        }
      ]
 
      while (loopList.length) {
        let node = loopList.pop()
        let { parent, key, data } = node
        let anoPar = parent
        if (typeof key !== 'undefined') {
          anoPar = parent[key] = {}
        }
 
        for (let i in data) {
          if (typeof data[i] === 'object') {
            loopList.push({
              parent: anoPar,
              key: i,
              data: data[i]
            })
          } else {
            anoPar[i] = data[i]
          }
        }
      }
      return result
    }
 
 
    let cloneA1 = deepClone5(a1)
    cloneA1.c.c2.c22 = 5555555
    console.log(a1);
    console.log(cloneA1);
 
 
    // ------------------------------------------JSON.stringify()实现深拷贝
 
    function cloneJson(o) {
      return JSON.parse(JSON.stringify(o))
    }
 
    // let obj = { a: { c: 1 }, b: {} };
    // obj.b = obj;
    // console.log(JSON.parse(JSON.stringify(obj))) // 报错 // Converting circular structure to JSON
```

> 深拷贝能使用hash递归的方式写出来就可以了 不过技多不压身，推荐还是看一看使用 while 实现深拷贝方法

## 手写防抖

### 手写防抖函数

```js
function debounce(func, wait) {
  let timeoutId;
  return function(...args) {
    const context = this;
   if (timeoutId) clearTimeout(timeoutId);
    timeoutId = setTimeout(() => {
      func.apply(context, args);
    }, wait);
  };
}
```

### 详细解释

1. **定义函数**：`debounce` 接收两个参数：
   - `func`：要防抖的函数。
   - `wait`：在最后一次调用后等待的毫秒数。
2. **内部状态**：使用 `timeoutId` 变量来存储 `setTimeout` 的 ID，以便在新的调用到来时清除之前的定时器。
3. **返回新函数**：返回一个新的函数，这个函数在每次调用时会清除之前的定时器，并设置一个新的定时器来执行原始函数 `func`。
4. **处理调用**：
   - 每次调用返回的新函数时，会清除之前的定时器（如果有的话）。
   - 设置一个新的定时器，在 `wait` 毫秒后执行原始函数 `func`。
5. **保存上下文和参数**：使用 `context` 和 `args` 来保存当前上下文和传递给原始函数的参数，这样在定时器触发时可以正确地执行原始函数。

### 使用示例

下面是一个简单的使用示例，展示了如何使用手写的防抖函数来处理输入框的变化事件。

```js
const searchInput = document.getElementById('search-input');

const handleInputChange = debounce(function(event) {
  console.log('Search input changed:', event.target.value);
}, 300);

searchInput.addEventListener('input', handleInputChange);
```

### 说明

- **输入变化事件**：每次输入框发生变化时，都会触发 `input` 事件。
- **防抖函数**：使用 `debounce` 函数来确保 `handleInputChange` 函数只在最后一次输入后的 300 毫秒内执行一次。
- **输出**：每 300 毫秒打印一次输入框的值，即使用户快速连续输入。

## 手写节流

### 手写节流函数

```js
function throttle(func, limit) {
  let inThrottle = false;

  return function(...args) {
    const context = this;

    if (!inThrottle) {
      func.apply(context, args);
      inThrottle = true;
      setTimeout(() => {
        inThrottle = false;
      }, limit);
    }
  };
}
```

### 详细解释

1. **定义函数**：`throttle` 接收两个参数：
   - `func`：要节流的函数。
   - `limit`：两次执行之间的时间间隔（毫秒）。
2. **内部状态**：使用 `inThrottle` 变量来跟踪当前是否正在节流周期内。
3. **返回新函数**：返回一个新的函数，这个函数在每次调用时会检查当前是否处于节流周期内。
4. **处理调用**：
   - 如果 `inThrottle` 为 `false`，则执行原始函数 `func`。
   - 设置 `inThrottle` 为 `true`，表示现在处于节流周期内。
   - 使用 `setTimeout` 来在 `limit` 毫秒后将 `inThrottle` 设置回 `false`。
5. **保存上下文和参数**：使用 `context` 和 `args` 来保存当前上下文和传递给原始函数的参数，这样在调用原始函数时可以正确地执行。

### 使用示例

下面是一个简单的使用示例，展示了如何使用手写的节流函数来处理窗口大小变化事件。

```js
const resizeHandler = throttle(function() {
  console.log('Window resized');
}, 250);

window.addEventListener('resize', resizeHandler);
```

### 说明

- **窗口大小变化事件**：每当窗口大小发生变化时，都会触发 `resize` 事件。
- **节流函数**：使用 `throttle` 函数来确保 `resizeHandler` 函数最多每 250 毫秒执行一次。
- **输出**：每 250 毫秒打印一次 “Window resized”，即使用户快速连续改变窗口大小。



