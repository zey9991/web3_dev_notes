# Reference

[01. Hello JavaScript | WTF Academy](https://www.wtf.academy/docs/javascript-101/HelloJavaScript/)

# 1. Hello JavaScript (2行代码)

2023年，WTF Academy 将开发一个零基础入门的 JavaScript 教程，帮助新人进入 Web3 开发。第一讲，我们将介绍什么是 JavaScript，并编写第一个JavaScript 程序：`Hello JavaScript`（两行代码）。

## 什么是 `Javascript`?

JavaScript 是一种用于与网页元素交互的轻量型编程语言。前端开发者可以将它与 HTML/CSS 结合并增强网页的功能，例如动态更新网页内容，网页交互等。现在，JavaScript 也可以在服务器（后端）通过 Node.js 运行，用于更新数据库、文件系统等。

## JavaScript的历史

JavaScript是一种由Netscape公司在1995年开发的脚本语言。Netscape的布兰登·艾希（Brendan Eich）在仅仅10天内设计出了这种语言的初版，起初命名为Mocha，之后更名为LiveScript，最后在1995年底与Sun Microsystems公司联手宣布更名为JavaScript，当时的目的是与那时广受欢迎的Java语言相吸引。

尽管Java和JavaScript的名字相似，但两者在设计理念和语法上有着显著的差异。JavaScript设计之初主要是为了在浏览器中执行简单的任务，如表单验证、动画效果等，而Java是一种用于构建大型企业级应用的全功能编程语言。

1997年，JavaScript被提交到ECMA国际（European Computer Manufacturers Association）并成为ECMAScript的标准。这个标准从那时起就一直在不断的发展和进化，现在我们通常说的JavaScript其实就是遵循ECMAScript标准的语言。

## 为什么要学习JavaScript?

JavaScript在现代Web开发中起着至关重要的作用，它是浏览器中唯一的编程语言。主要的作用包括：

1. **动态交互**：JavaScript使网页具有动态性，例如，可以在用户不需要重新加载整个页面的情况下对网页的一部分进行更新，或响应用户的点击，滚动等操作。
2. **操作DOM**：JavaScript可以操作网页上的DOM元素，动态更改网页内容。
3. **前端验证**：JavaScript可以在数据发送到服务器之前进行前端验证，提高数据的正确性。
4. **Ajax通信**：通过JavaScript的Ajax，我们可以在后台与服务器进行数据交互，创建动态而且实时的网页。

近年来，JavaScript的使用范围已经扩展到了浏览器之外。例如，Node.js是一个基于JavaScript的开源服务器框架，使得JavaScript也可以用于服务器端的开发。而React Native、Ionic等框架则让JavaScript成为了移动应用开发的工具。同时，很多新兴的前端框架和库，如React.js、Vue.js、Angular.js都是基于JavaScript的，极大地推动了前端开发的进步。

根据2022年[Stack Overflow社区年度调查显示](https://survey.stackoverflow.co/2022/#most-popular-technologies-language)，JavaScript 已经连续十年成为最受开发者欢迎的一门编程语言。学习 JavaScript 不仅是普通 web 开发者的必备技能，同时也是全栈 web3 学习者的必要知识。



![1-1](https://www.wtf.academy/assets/images/1-1-6e6c0ebbd96466857c5898fa6fcee5a7.png)



## JavaScript与其他语言的比较

虽然JavaScript和其他编程语言（例如Python和Java）在语法和设计上存在一些差异，但JavaScript的基本组件（如变量，函数，循环和条件语句）与其他语言非常相似。然而，JavaScript有一些独特的特性，使得它在Web开发领域独树一帜。

- **动态类型**：JavaScript是一种动态类型的语言，这意味着你不需要预先声明变量的类型。一个变量可能开始时是一个数字，稍后可以变成一个字符串。
- **解释型语言**：与需要先编译后运行的语言（如C++和Java）不同，JavaScript是一种解释型语言。这意味着代码在运行时被解释和执行，不需要进行预编译。
- **基于原型的对象模型**：不同于基于类的语言（如Java），JavaScript使用的是基于原型的对象模型。在JavaScript中，对象可以继承其他对象的属性，称为原型链。
- **第一类函数**：在JavaScript中，函数是第一类对象，这意味着函数可以作为其他函数的参数，也可以作为其他函数的返回值。

## 开发工具

### 1. playcode.io



![img](https://www.wtf.academy/assets/images/1-2-6640abc83da67fa09c6419e839438c7a.png)



[playcode](https://playcode.io/)是一个JavaScript的在线编译平台，你不需要在本地安装任何程序就可以运行`.js`文件，非常方便。本教程将使用 playcode 进行代码演示，未来也将在 [wtf.academy](https://wtf.academy/) 的教程中嵌入可互动代码模块。你可以在[链接](https://playcode.io/1051873)上找到这一讲的代码。



![img](https://www.wtf.academy/assets/images/1-3-bb38aec82c0a4630d9477a37163b3f6e.png)



### 2. VS Code & WebStorm

你可以使用本地 [VS Code](https://code.visualstudio.com/download) 或[WebStorm](https://www.jetbrains.com/webstorm/)进行开发，需要安装[Node.js](https://nodejs.org/zh-cn/download/)，我们会在之后的章节介绍如何使用它。

## Hello JavaScript!

下面，我们要写第一个 JavaScript 程序：`Hello JavaScript`。在这个程序中，我们定义了一个变量，并将它的值输出到控制台。

代码:

```js
let hello = "Hello JavaScript!";
console.log(hello);
```



输出:

![1-2](https://www.wtf.academy/assets/images/1-4-e497e7cb679fd531655eb0858eb5cd9b.png)



下面，我们逐行学习一下。

1. 第 1 行，我们利用 `let` 关键字定义了一个名为 `hello` 的变量，并将`"Hello JavaScript!"` 赋值给它，最后以分号 `;` 结束这一行语句。

   ```js
   let hello = "Hello JavaScript!";
   ```

   

2. 第 2 行，我们利用内置函数 `console.log` 将 `hello` 变量的值输出到控制台，让人们可以看到。

   ```js
   console.log(hello);
   ```

   

## 【拓展知识】Javascript 程序是如何运行的?



![img](https://www.wtf.academy/assets/images/1-5-95abd90f9649f662dfcca87a13d233b9.png)



> 你不理解下面这段话也没关系，不妨碍你继续学习 JavaScript，因为我也不是很理解！

如果说`编程语言`是人类与机器沟通的语言，那么`程序`是一篇篇文章，`代码`是其中的文本。Javascript 程序运行的大致步骤如下：

1. 程序员完成一段代码。

   ```js
   let hello = "Hello JavaScript!";
   ```

   

2. 将代码提交给`编译器`（compiler）编译。首先，`编译器`会将`代码`分解为单个的`令牌`（token）。上面的语句会被分解为 `5` 个令牌: `let`, `hello`, `=`, `"Hello JavaScript!"`, 和 `；`。

3. 接下来，`令牌`会被重新组织成一个树状结构，也叫`抽象语法树`（Abstract Syntax Tree, AST）。你可以在[AstExplorer](https://astexplorer.net/)上输入代码，并查看生成的`抽象语法树`。

4. 最后，编译器会将结构化的`抽象语法树`转换并生成计算机能运行的的`机器码`。

如果你的`代码`没有按照`编程语言`的语法来写，编译器就无法把它解析为机器能懂的`机器码`，那么`程序`就无法运行。这时，你就要去找出程序的`bug`并修复它。在未来的教程中，我们将介绍更多的 `JavaScript` 语法。

## 习题

将 `Hello Javascript` 程序中变量 `hello` 的值改为 `“Hello WTF Academy!”`，并观察控制台的输出。

## 总结

第一讲，我们介绍了什么是 JavaScript，为什么要学习它，JavaScript 开发工具，并编写了第一个仅有两行的 JavaScript 程序：`Hello JavaScript`。接下来，我们将继续 JavaScript 之旅！

# 2. 声明变量

编程最基本的技术之一就是使用变量（variable）来表示值，就像用 `0xAA` 来指代一个人。在 JavaScript 程序中使用变量之前必须先声明这个变量。这一讲，我们将介绍声明变量的三个关键字 `let`，`const`，和 `var`，以及它们之间的区别。

## `let`

在现代 JavaScript 中（ES6 版本之后），变量通过 `let` 关键字声明。

```js
// 1. 先声明 year 变量，再给它赋值 2023
let year;
year = 2023;
// 2. 声明 name 变量的同时给它赋值 "0xAA" 
let name = "0xAA";
// 3. 声明 newName 变量，同时将变量 name 的值 “0xAA” 赋给它
let newName = name;
```



在上面的代码中，我们先声明了一个名为 `year` 的变量，并给它赋值 `2023`；之后声明另一个名为 `name` 变量的同时给它赋值 `"0xAA"`。最后，我们声明了一个名为 `newName` 的变量，并将变量 `name` 的值（`"0xAA"`）赋给它。

> 代码中以 `//` 开头的行是注释，用于提高代码的可读性，不会被执行。

## `const`

在声明常量（constant，值不能改变的变量）是要用 `const` 关键字，声明时必须给它赋值。常量在第一次赋值后不能改变，不然会报错。

```javascript
// 声明 age 常量，并赋值 18
const age = 18;
// 尝试改变常量的值时会报错 TypeError: Assignment to constant variable
age = 20; 
```



## `var`（不推荐）

在 ES6 之前的 JavaScript 中，没有 `let` 和 `const` 关键字，声明变量只能用 `var` 关键字。`var` 和 `let` 使用上类似，但是会造成全局对象的污染，是个过时的关键字，不推荐使用。

```javascript
// 声明 variable 变量并赋值 "hello"
var variable = "hello"
```



更多关于 `var` 的细节请参考 [MDN教程](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/var)。

## 使用规范

ES6 之后新增的 `let` 和 `const` 关键字很好地解决了过时的 `var` 在作用域和语义上存在的诸多问题，也形成了开发时的使用规范。

1. 能用 `const` 就用 `const`：使用 `const` 声明变量可以确保一些重要的值不会被改变，同时也能迅速发现一些因意外赋值导致的不合理行为。
2. 不能用 `const` 就用 `let`，不要使用`var`：当开发者提前知道某些变量未来需要被修改时就使用 `let`，这样可以确保变量拥有明确的作用域和声明位置。

## 习题

下面的代码是否会报错？如果会，请修改它，让它正确运行。你可以在[链接](https://playcode.io/1058216)上找到这段代码。

```js
const fruit = 'apple'
fruit = 'orange'
console.log(fruit)
```



## 总结

这一讲我们介绍了声明变量的三个关键字 `let`，`const`，和 `var`，并讲解了它们之间的区别和用法。在开发中，能用 `const` 就用 `const`，不能用 `const` 就用`let`，不要使用 `var`。

# 3. 常用类型

这一讲，我们将介绍 JavaScript 中常用的数据类型：数值（*Number*）、字符串（*String*） 和 布尔值（*Boolean*）。

## 1. 数值 Number

数值（Number）是 JavaScript 中最常用的类型，它既可以声明整数，也可以声明浮点数（小数）。

```js
// 声明整数
const int = 10;
// 声明浮点数
const float = 1.1;
```



### 1.1 NaN、Infinity、-Infinity

JavaScript 中有三个特殊数值。

1. `NaN`：表示 “不是数值”，当返回数值的操作失败时会出现，比如 `0 / 0`（表示 0 除以 0）。

   ```js
   const nan = 0/0 // NaN
   ```

   

2. `Infinity`：无穷大，表示超出上限的结果，比如 `1 / 0`。

   ```js
   const inf = 1/0 // Infinity
   ```

   

3. `-Infinity`：负无穷大，表示超出下限的结果，比如 `-1 / 0`。

   ```js
   const negInf = -1/0 // -Infinity
   ```

   

## 2. 字符串 String

JavaScript 中的文本由字符串（String）类型表示。你可以使用双引号（`""`）、单引号（`''`）或反引号（````）标示它。

```js
const str1 = "WTF"; // 双引号（推荐）
const str2 = 'Academy'; // 单引号
const str3 = `JavaScript`; // 反引号（模板字符串）
```



### 2.1 模板字符串

在 ES6 之后的版本中，字符串可以用反引号标示，这样的字符串被称为“模板字符串”（Template Literals）。它很有意思，可以用作字符串插值：在模板字符串使用 `${}` 可以在其中插入变量并解析。

```js
const name = "0xAA";
const age = 18;
const template = `姓名 ${name}，年龄 ${age}。`;
console.log(template); // 姓名 0xAA，年龄 18。
```



改变 `name` 和 `age` 值改变的时候，模板字符串也会作相应改变。

## 3. 布尔值 Boolean

布尔值（Boolean）类型用于表示 *真或假*，*是与非*。它只有两个值：`true` 和 `false`。我们经常在控制结构，比如 `if/else` 语句中使用它，之后章节中会涉及。

```js
const bool1 = true;
const bool2 = false;
```



## 习题

请补全下面的代码，让它正常运行。注意，`nickname` 为字符串， `age` 为数值，`isDev` 为布尔值。你可以在[链接](https://playcode.io/1059248)上找到这段代码。

```js
const nickname = ; // 昵称
const age = ; // 年龄
const isDev = ; // 是否为开发者
const template = `欢迎 ${age} 岁的 ${nickname} 来到 WTF Academy！
你是开发者吗？ ${isDev}`;
console.log(template);
```



## 总结

这一讲，我们介绍了三种最常用的变量类型：数值，字符串，和布尔值。你会在之后的 JavaScript 之旅中不断和他们打交道！

# 4. 运算符

运算符可以对单个或多个变量（操作数）进行某些操作并产生结果。这一讲，我们将介绍 JavaScript 中常用的运算符，包括算数运算符，比较运算符，和逻辑运算符。

## 1. 算数运算符

算数运算符用于操作数之间的数学运算，有以下几种（`x` 和 `y` 为数值变量）：

| 运算符 | 描述     | 例子             |
| ------ | -------- | ---------------- |
| +      | 加法     | x + y            |
| -      | 减法     | x - y            |
| *      | 乘法     | x * y            |
| /      | 除法     | x / y            |
| %      | 取余     | x % y            |
| **     | 求幂     | x ** y           |
| ++     | 递增运算 | num1++ 或 ++num1 |
| --     | 递减运算 | num2-- 或 --num2 |

```js
let num1 = 1 + 1; // 2
let num2 = 1 - 1; // 0
let num3 = 2 * 3; // 6
let num4 = 6 / 2; // 3
let num5 = 7 % 2; // 1
let num6 = 2 ** 3; // 8
num1++ // 3
num2--; // -1
```



前三个运算符非常简单，我们主要介绍后五个。

### 1.1 除法

在很多编程语言中，例如 Java、C、C++ 等，除法 `/` 一般都是作整除运算。但是在 JavaScript 中，除法 `/` 就是指数学上的除。如果你要做整除运算，需要调用 `Math.floor()` 函数进行向下取整。

```js
5 / 4; // 1.25
Math.floor(5 / 4); // 1
```



### 1.2 取余

`x % y` 结果是 `x` 整除 `y` 的余数。

```js
5 % 4; // 1
```



### 1.3 求幂

`x % y` 结果是 `a` 的 `y` 次方。

```js
2 ** 3; // 2³ = 8
```



### 1.4 递增和递减

递增和递减运算符的原理都类似，我们以递增运算符作为讲解。递增运算符有两个形式：

- 前缀形式（++i）：运算符在变量的前面，先递增，后执行语句。
- 后缀形式（i++）：运算符在变量的后面，先执行语句，后递增。

```js
let x = 1;
let y = x++; // y 赋值 1，然后 x 递增为 2
let z = ++x; // x 递增为 3，然后 z 赋值为 3
console.log(x, y, z) // 3, 1, 3
```



## 2. 比较运算符

比较运算符用于确定操作数之间的差异，然后返回一个布尔值。主要有以下几种：

| 操作符 | 描述               |
| ------ | ------------------ |
| ==     | 相等               |
| !=     | 不相等             |
| >      | 大于               |
| <      | 小于               |
| >=     | 大于等于           |
| <=     | 小于等于           |
| ===    | 严格相等（推荐）   |
| !==    | 严格不相等（推荐） |

```js
let x = 1;
let y = 2;
let bool1 = (x == y); // false
let bool2 = (x != y); // true
let bool3 = (x > y); // false
let bool4 = (x < y); // true
let bool5 = (x >= y); // flase
let bool6 = (x <= y); // true
let bool7 = (x === y); // flase
let bool8 = (x !== y); // true
```



## 严格不相等

JavaScript 是弱类型语言，开发者在声明变量的时候不需要声明变量类型，而是由 JavaScript 引擎在编译时隐式完成。这会带来方便，但也带来一些坑。比如 `==` 和 `!=` 操作符在比较时，会先对变量进行强制类型转换，然后再做比较：例如 `"5" == 5` 会返回 `true`。但是强制类型转换的规则很复杂，比如 `"" == "0"` 返回 `false`，但是 `0 == ""` 返回 `true`。

因此实际使用时，推荐用 `===` 和 `!==` 进行相等和不相等的判断:

- 严格相等 `===`：只有变量的值和类型均相等时，才算严格相等。
- 严格不相等 `!==`：不同类型的变量是不相等的，例如 `"5"` 和 `5` 不相等。

```js
// 相等/不相等，强制类型转换
"5" == 5; // true
"5" != 5; // false
// 严格相等/严格不相等，不进行类型转换
"5" === 5; // false
"5" !== 5; // true
```



## 3. 逻辑运算符

逻辑运算符常用于布尔值之间，主要有以下 `3` 个 (`a` 和 `b` 为布尔值)：

- 或 `||`: `a || b`
- 与 `&&`: `a && b`
- 非 `!` : `!a`

### 3.1 或 `||`

或运算是指当参与运算的任何一个操作数为 `true` 时，返回的结果就为 `true`，否则就返回 `false`。即只要有一个操作数是对的，整个表达式就是对的。

```js
true || true; // true
false || true; // true
true || false; // true
false || false; // false
```



### 3.2 与 `&&`

与运算是指当参与运算的任何一个操作数为`false`时，返回的结果就为`false`，否则就返回`true`。即所有操作数均是对的，整个表达式才是对的。

```js
true && true; // true
false && true; // false
true && false; // false
false && false; // false
```



### 3.3 非 `!`

非运算符是对操作数取反，将 `true` 变为 `false`，`false` 变为 `true`。

```js
!true; // false
!false; // true
```



## 习题

给出下面 `6` 个变量的值。你可以在[链接](https://playcode.io/1061414)上找到这段代码。

```js
let a = 69;
let b = a++ + a; //139
let c = a * 2; //140
let d = (b === c);
let e = true;
let f = e && d;

console.log(f);
```



## 总结

这一讲，我们介绍了 JavaScript 中最常用的运算符：算数运算符，比较运算符，逻辑运算符。大家可能对递增/递减（`++`/`--`）和严格等于（`===`）比较陌生，不用担心，我们将在之后的教程中反复练习。

# 5. 函数

这一讲，我们将介绍 JavaScript 中的函数 `function`，包括定义函数的语法、函数引用和函数的参数。

## 函数声明

函数是 JavaScript 的基本组件之一，它将一串指令包装起来，形成一个代码块，方便重复利用，让代码更加系统化，你可以把搜索引擎理解为一个函数，每次在你输入搜索内容并点击搜索键之后，它会运行一串非常复杂的逻辑，然后返回给你搜索结果。

函数最大的特征是拥有参数和返回值：

```js
function foo(input){
    return input;
}
// foo(5) 将返回 5
```



上面的代码中，我们用 `function` 关键字声明了一个名为 `foo` 的函数。它有一个参数 `input`，可以在调用函数的时候输入。花括号 `{}` 中包裹着函数体，承载着函数的逻辑。这个函数逻辑非常简单，我们用 `return` 关键字定义了一个返回值，它会结束函数的运行并将 `input` 原封不动的返回给调用者。

`foo()` 看起来有点没用，下面我们丰富一下函数体，让它完成更多功能。

```js
function bar(input){
    const output = input * 2;
    return output;
}
// bar(5) 将返回 10
```



上面的 `bar()` 函数中，我们计算了 `input * x`，然后将它赋值给 `output` 变量，最后返回。

函数可以承载多个参数，下面的 `sum()` 函数中，我们实现了加法，将参数 `x` 和 `y` 相加，并返回。这里返回值我们没有使用变量，而是一个表达式；运行时，程序会先执行表达式，然后将结果返回。

```js
function sum(x, y){
    return x + y;
}
// sum(5, 6) 将返回 11
```



## 函数调用

你可以使用 `函数名(参数)` 的模式来调用函数，例如:

```js
sum(5, 6); // 返回 11
```



你也可以在函数中调用另一个函数:

```js
function sumCall(x, y){
    const output = sum(x, y)
    return output;
}
```



> `Tips`: 如果仅使用 `函数名` 的话，会返回该函数对象，而非返回值，因此调用函数时一定要加括号和参数。

## 函数表达式和箭头函数

下面我们介绍另外两种定义函数的方法。

1. 函数表达式: 它与上面的方式声明几乎一样，唯一的区别就是函数名 `sum1` 被提到前面作为变量，并且多了赋值操作。使用起来也是一样的。更多内容见 [MDN 教程](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/function#语法)

   ```js
   const sum1 = function(x, y){
       return x + y;
   }
   ```

   

2. 箭头函数: ES6 版本新增了使用箭头语法 `=>` 来定义函数，这种语法比另外两种方法更为简洁。更多内容见 [MDN 教程](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions)。

   ```js
   const sum2 = (x, y) => {
       return x + y;
   }
   ```

   

## 习题

修改下面的 `prod()` 函数，让它返回两个参数 `x` 和 `y` 的积。

```jsx
function TestJS05(props) {
  // 要修改的函数 prod，计算x和y的积
  function prod(x, y){
    return ;
  }

  // 应返回30
  return prod(5, 6);
}
```



## 总结

这一讲，我们介绍了 JavaScript 中的函数，包括定义函数的语法和如何调用函数。函数是你编程中最好的伴侣，我们会在之后的教程中反复利用它。

# 6. 条件语句

在投资中，我们经常会根据价格不同而采取不同的策略。这一讲，我们介绍 JavaScript 中的条件语句，它可以让我们做到根据不同条件执行不同的操作。



![img](https://www.wtf.academy/assets/images/6-1-d3febd93e6a8052b34acf3bed788adcd.png)



## if 语句

`if` 语句的基本结构如下：

```js
if (条件) {
  语句
}
```



当 `if` 语句的条件为  `true` 时，则会执行对应的代码块。例如：

```js
let x = 1;
if (x > 0) {
  x = x + 1;
}
console.log(x); // 2
```



`if` 语句会计算圆括号内的表达式，并将计算结果转换为布尔类型，下列值将会被计算为 `false` ：

- `false`
- `undefined`
- `null`
- `0`
- `NaN`
- 空字符串（`""`）

当传递给 `if` 语句所有其他的值，包括所有对象会被计算为 `true`

## if-else 语句

`if` 代码块后还可以跟随一个 `else` 代码块，如果判断条件不成立，则会执行它内部的代码。

```js
let y = 1;
if (y != 1) {
  y = y + 1;
} else {
  y = y - 1;
}
console.log(y); // 0
```



## else-if 语句

有时我们需要进行多次判断，可以通过使用  `else-if` 语句实现：

```js
const z = 2;

if (z === 0) {
  console.log('x 的值为 0');
} else if (z === 1) {
  console.log('x 的值为 1');
} else if (z === 2) {
  console.log('x 的值为 2');
} else {
  console.log('x 为其它值');
}
```



## 三元运算符

三元运算符，也称条件运算符，是 JavaScript 唯一使用三个操作数的运算符。使用规则： `条件 ? 表达式1 : 表达式2`。当条件为真时，执行`表达式1`，否则执行`表达式2`。该运算符经常当作 `if-else` 语句的简捷形式来使用。例如：

```js
// 返回 x 和 z 之中更大的数
const bigger = x < z ? z : x;
console.log(bigger);
```



## 习题

补全下面的 `isOdd` 函数，完成逻辑: 当输入参数 `num` 为奇数时，返回 `true`，偶数时返回 `false`。

> 提示：可以使用取余运算符 `%` 来计算 `num` 与 2 的余数。如果是 0，则为偶数；如果是 1，则为奇数。

```js
function isOdd(num){
}
```

以下是完整的代码：

```javascript
function isOdd(num) {
  return num % 2 !== 0; // 如果余数不为0，则为奇数，返回true；否则返回false
}

```



## 总结

这一讲我们介绍了 JavaScript 的条件语句，包括 `if`，`if-else`，`else-if`，和三元运算符。它们可以丰富程序的逻辑性。

# 7. 循环

我们经常需要重复执行一些操作，比如将列表中的商品逐个输出。这一讲，我们将介绍 JavaScript 中的循环语句，让程序重复执行某些操作。

## for 循环



![img](https://www.wtf.academy/assets/images/7-1-c790baba7b235117ead7f5074a041dd2.png)



`for` 循环是最常使用的循环形式，它可以指定循环的起点、终点和终止条件。其基本结构如下：

```js
for (循环变量初始化; 循环结束条件; 增量表达式) {
  执行语句
}
```



其中

- 循环变量初始化：初始化循环计数器，比如我们初始化一个变量来记录循环次数 `let i = 0`。
- 循环结束条件：它是一个表达式，用于判断是否结束循环。每轮循环开始时，都会计算这个条件表达式的值，若为 `true`，才继续进行循环；否则停止循环。比如，我们让循环十次，即 `i < 10`。
- 增量表达式：每轮循环执行的最后一个操作，通常用来更新循环变量。一般会将循环变量加一 `i++`。
- 执行语句: 每次循环重复的动作。比如打印出当前 `i` 的值。

下面是循环打印 `i` 的代码：

```js
for (let i = 0; i < 10; i++) {
  console.log(`i 当前的值为：${i}`);
}

// i 当前的值为：0
// i 当前的值为：1
// ...
// i 当前的值为：9
```



## while 循环



![img](https://www.wtf.academy/assets/images/7-2-165b4986cc6b417db574cc93027f436b.png)



`while` 语句包括一个循环条件和一段代码块，每次循环会先检查循环条件，若为 `ture`，就继续执行代码块。它的基本结构如下：

```js
while (条件) {
  语句
}
```



与 `for` 循环相比，它没有循环变量及其自增，需要在语句中自己定义。我们将上面的例子改写为 `while` 循环：

```js
let i = 0
while (i < 10) {
  console.log(`i 当前的值为：${i}`)
  i++
}
```



## do-while 循环



![img](https://www.wtf.academy/assets/images/7-3-af0ad4261a90af9b0ffc8d2e59739a98.png)



`do-while` 循环与 `while` 循环类似，唯一的不同在于`do-while` 循环会首先执行循环体，然后检查条件，当条件为 `true`，重复执行循环体。其基本结构如下：

```js
do {
  语句
} while (条件)
```



这种结构的特点是不管条件是否为真，循环体至少执行一次。将前面 `while` 循环中打印 `i` 的例子改成 `do-while` 循环如下：

```js
let i = 0
do {
  console.log(`i 当前的值为：${i}`);
  i++;
} while (i < 9)
```



> 思考一下为什么这里的条件是 `i < 9` 而不是 `i < 10`？如果改为 `i < 10`，结果会有什么变化？

## break 语句

`break` 语句用于跳出代码块或循环。

下面的例子只会执行两次循环，当 `i` 等于 2 时，就会跳出循环：

```js
for (let i = 0; i < 3; i++) {
  console.log(`i 当前的值为：${i}`);
  if (i === 2) break;
}

// i 当前的值为：0
// i 当前的值为：1
// i 当前的值为：2
```



## continue 语句

`continue` 语句也用于跳出循环，与 `break` 语句不同的是，它不会中止整个循环，只会终止本轮循环，然后返回循环结构的头部，开始下一轮循环。

下面的代码会打印 10 以内的奇数：

```js
for (let i = 0; i < 10; i++) {
  if (i % 2 === 0) continue
  console.log(`i 当前的值为：${i}`)
}
// i 当前的值为：1
// i 当前的值为：3
// i 当前的值为：5
// i 当前的值为：7
// i 当前的值为：9
```



## 习题

补全下面的 `sum` 函数，完成逻辑: 返回从 1 到正整数 `num` 所有数的和。比如 `num` 为 5 时，返回 15.

```js
function sum(num) {
  let sum = 0;
  for (let i = 0; i <= num; i++) {
    sum += i;
  }
  return sum;
}

console.log(sum(5)); // 应该返回 15
console.log(sum(9)); // 应该返回 45

```



## 总结

这一讲我们介绍了 JavaScript 的循环语句，主要介绍了 `for` 和 `while` 两种循环结构，以及跳出循环的方法。

# 8. 数组

这一讲，我们会介绍 Javascript 最常见的复杂类型：数组（Array)。它可以把多个数据有序的存储在一起。

## 定义

数组类型支持在单个变量名下存储多个元素。创建数组最简单的方式，就是在一对中括号 `[]` 内部用逗号 `,` 分割的列表，例如：

```js
// 没有元素的空数组
const empty = [];
// 存储三个字符串的数组
const courses = ["Solidity", "Etherjs", "JavaScript"];
// 存储不同数据类型的数组
const mix = [1,'WTF',true];
```



数组中的元素可以使基础类型，也可以是另外一个数组。你可以通过数组存储比较复杂的嵌套数据。下面，`complex` 数组包含了 `courses` 和 `mix` 两个数组：

```js
// complex是一个数组，包含两个元素，每个元素都是另外一个数组
const complex = [courses, mix];
const nested = [[1, 2], [1, 1, 1]];
```



## 读写数组



![img](https://www.wtf.academy/assets/images/8-1-f1dc8ed16f3bef44ffd52756d696074e.png)



### 读取

我们可以在变量上使用索引（中括号 `[]`）来读取数组元素。注意数组的索引是从 0 开始计算的：

```js
const arr = [1,2,3,["Solidity",true]]
// 读取第 0 个元素
console.log(arr[0])  // 1
// 读取嵌套数组第 0 个元素
console.log(arr[3][0]) // "Solidity"
```



### 写入

你可以利用索引对某个元素进行赋值，从而修改数组：

```js
// 修改数组的第1个元素
arr[1] = 6
console.log(arr) //[1, 6, 3, Array(2)]
```



数组变量还有一些属性可以读取，例如 `length` 属性会返回数组的长度：

```js
// 输出数组长度
console.log(arr.length) // 4
```



## 遍历数组

一个数组存储着多个数据，我们可以用循环来遍历数组内部的所有元素。下面的例子中，我们使用 for 循环来计算 `numArr` 数组的平均值。

```js
const numArr = [5, 8, 9, 11, 55];
let average = 0;
for(let i = 0; i < numArr.length; i++){
  average += numArr[i] / numArr.length
    //average = average + (numArr[i] / numArr.length);
}
console.log(`平均值为: ${average}`) // 17.6
```



## 增加和删除

数组中内置了很多方法，其中 `push`, `pop` 用于增加，删除元素。

### push



![img](https://www.wtf.academy/assets/images/8-2-3c9b865291a59037c97a2ca814f9e068.png)



数组中我们可以使用 `push` 方法在数组最后 `推入` （新增）一个元素。这个方法会使数组长度加一。

```js
const nums = [1,2,3]
nums.push(4)
console.log(nums) // [1, 2, 3, 4]
```



### pop



![img](https://www.wtf.academy/assets/images/8-3-af1429cfdb2f5d528f64762e33f1ffbb.png)



我们可以使用 `pop` 方法从数组的末尾 `弹出` 一个元素。这个方法会使数组长度减一，同时返回被弹出的元素。

```js
// pop方法会返回被弹出的元素
const last = nums.pop()
console.log(last) // 4  弹出
console.log(nums) // [1, 2, 3]
```



更多的数组操作方法可以参考 [MDN教程](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array#实例方法)，可以着重看一下 `slice`, `splice`, `indexOf` 方法。

## 习题

补全下面的 `sumOdd` 函数，完成逻辑: 计算输入数组 `arr` 中所有奇数的和。

```js
function sumOdd(arr){
	sum=0;
    for(let i=0;i<=arr.length;i++){
        if arr[i]%2===1{
          sum+=arr[i];  
        }
    }
    return sum;
}

console.log(sumOdd([1, 2, 3, 4, 5])) // 应该返回 9
console.log(sumOdd([2, 4, 6, 8, 10])) // 应该返回0
console.log(sumOdd([1, 3, 5, 7, 9])) // 应该返回 25
```

修正说明：

1. **循环条件**: `for(let i=0; i <= arr.length; i++)` 应该改为 `for(let i=0; i < arr.length; i++)`。因为 `arr.length` 的索引是从 `0` 开始的，最大索引为 `arr.length - 1`。
2. **if 语句的语法**: `if arr[i] % 2 === 1` 应该写为 `if (arr[i] % 2 === 1)`，即需要加上括号来包含条件表达式。

```js
function sumOdd(arr) {
  let sum = 0; // 初始化 sum
  for (let i = 0; i < arr.length; i++) {
    // 循环条件应该是 < 而不是 <=
    if (arr[i] % 2 === 1) {
      // if 语句需要加上括号
      sum += arr[i];
    }
  }
  return sum; // 返回总和
}

console.log(sumOdd([1, 2, 3, 4, 5])); // 应该返回 9
console.log(sumOdd([2, 4, 6, 8, 10])); // 应该返回 0
console.log(sumOdd([1, 3, 5, 7, 9])); // 应该返回 25

```



## 总结

这一讲我们介绍了 Javascript 中的数组，包括数组的定义，读取，写入，和遍历。数组是日常开发中经常用到的数据结构，我们将在后续的教程不断见到，一定要好好掌握。

# 9. 对象

上一讲我们学习了可以存储多个数据的数组，这一讲我们学习另外一种复杂数据类型：对象（Object），包括对象的定义，读写，遍历，和增减。JavaScript 中的所有事物都是对象，包括字符串、数值、数组、函数，你一定哟好好掌握。

## 定义

JavaScript 中的对象类型是一系列属性和方法的集合。比如一辆车，它有`颜色`，`排量`，`品牌`等属性，且有`启动`，`转向`，`刹车`等方法；每辆车都有这些属性和方法，但他们的值不同。

创建对象变量的方式很简单，把对象的键值对（key-value pair）列表用大括号 `{}` 包裹起来，键值对之间用逗号 `,` 分割。你可以把对象理解为一个字典，`key` 就是字，`value` 就是字对应的含义。

```js
// 空对象
const empty = {};
// 包含 3 个属性的对象
const intro = {
  name: '0xAA',
  age: 1,
  isDeveloper: true,
};
```



对象也可以包含方法（函数）:

```js
// 包含方法的对象
const wtf = {
  name: `WTF JavaScript`,
  hello: function(){
    return "Hello JavaScript!";
  }
};
```

> [!TIP]
>
> 在 JavaScript 中，对象和其他编程语言中的结构体（如 C/C++、Go 等）有一些相似之处，但也有明显的区别。下面是它们的比较：
>
> ### 相似之处
>
> 1. **键值对**：
>    - 对象和结构体都可以用来存储多个属性，每个属性都有一个名称（键）和一个对应的值。
>
> 2. **组织数据**：
>    - 两者都用于组织和表示复合数据类型，能够将不同类型的数据组合在一起。
>
> ### 区别
>
> 1. **语言特性**：
>    - **对象**：JavaScript 的对象是动态的，属性可以在运行时添加、删除或修改。它们可以包含方法（函数），支持更复杂的行为。
>    - **结构体**：大多数编程语言的结构体是静态的，定义时就确定了结构，不能随意修改。结构体主要用于存储数据，不支持方法。
>
> 2. **数据类型**：
>    - **对象**：在 JavaScript 中，对象可以包含任意类型的数据，包括其他对象、数组、函数等。
>    - **结构体**：在其他语言中，结构体通常定义了固定的属性类型，且其成员的数据类型在编译时确定。
>
> 3. **内存管理**：
>    - **对象**：在 JavaScript 中，对象是引用类型，使用引用来访问内存中的数据。
>    - **结构体**：在 C/C++ 中，结构体通常是值类型，直接存储在栈上或分配在堆上，内存管理相对复杂。
>
> 4. **继承**：
>    - **对象**：JavaScript 对象支持原型继承，允许对象通过原型链继承其他对象的属性和方法。
>    - **结构体**：大多数编程语言的结构体不支持继承，结构体的功能相对简单。
>
> ### 总结
>
> - JavaScript 对象提供了更灵活的结构，适合用于动态数据和复杂行为的场景。
> - 结构体则更适合用于定义固定格式的数据，常用于数据存储和传递。
>
> 在选择使用对象还是结构体时，通常需要根据编程语言的特点和具体的应用场景来决定。

> [!NOTE]
>
> JavaScript 对象和 Python 字典之间也有许多相似之处，但它们在某些方面存在显著的差异。以下是两者的比较：
>
> ### 相似之处
>
> 1. **键值对**：
>    - 两者都使用键值对的方式来存储数据，可以通过键来快速访问对应的值。
>
> 2. **动态性**：
>    - 两者都是动态类型的数据结构，可以在运行时添加、删除或修改键值对。
>
> 3. **无序性**：
>    - 在 JavaScript 对象和 Python 字典中，键的顺序是非保证的（虽然在实际使用中，Python 3.7+ 的字典保留插入顺序）。
>
> ### 区别
>
> 1. **数据类型**：
>    - **对象**：JavaScript 对象的键是字符串（或 Symbol），而值可以是任何数据类型（包括对象、数组、函数等）。
>    - **字典**：Python 字典的键可以是不可变类型（如字符串、数字、元组），而值可以是任何数据类型。
>
> 2. **继承和方法**：
>    - **对象**：JavaScript 对象可以有方法，也就是可以包含函数，这使得对象不仅仅用于数据存储，还可以封装行为。
>    - **字典**：Python 字典主要用于存储数据，没有内置的方法来定义行为。
>
> 3. **内存管理**：
>    - 两者都在内存中以引用的方式存储对象，但在使用时，JavaScript 对象和 Python 字典的内部实现可能会有所不同。
>
> 4. **使用场景**：
>    - **对象**：通常用于创建数据结构和面向对象编程（如类实例）。
>    - **字典**：通常用于快速查找和存储数据，如配置、数据表等。
>
> ### 示例
>
> **JavaScript 对象**：
> ```javascript
> const person = {
>     name: "Alice",
>     age: 30,
>     greet: function() {
>         console.log(`Hello, my name is ${this.name}`);
>     }
> };
> 
> console.log(person.name); // 输出 "Alice"
> person.greet(); // 输出 "Hello, my name is Alice"
> ```
>
> **Python 字典**：
> ```python
> person = {
>     "name": "Alice",
>     "age": 30
> }
> 
> print(person["name"])  # 输出 "Alice"
> ```
>
> ### 总结
>
> - JavaScript 对象更像是具有行为的复杂数据结构，而 Python 字典则专注于存储和快速查找数据。根据具体的需求，选择适合的数据结构可以提高代码的可读性和性能。



## 读取

你可以使用索引 `对象名['key']` 来读取对象的值；也可以直接用 `对象.key` 来读取。

```js
// 读取属性
console.log(intro['name']); // 注意 `name` 是个字符串，有引号
console.log(intro.name); // 注意这种写法没有引号
```



对象内部的方法可以用 `对象.函数名()` 的方式调用：

```js
// 使用函数
console.log(wtf.hello()); // "Hello JavaScript!"
```



## 写入

我们可以利用索引来编辑对象的值：

```js
intro.age = 99;
console.log(intro.age); // 99
```



我们可以使用不存在的索引在对象里引入新的键值对。

```js
// 在 intro 对象中添加 gender 键值对
intro.gender = "male";
console.log(intro.gender); // "male"
```



## 遍历

我们可以使用 `for-in` 循环来实现遍历 `key`，语法与之前学的循环稍有不同：

```js
for(let key in intro){
  console.log('data '+ key + ': ' + intro[key])
}
// data name: 0xAA
// data age: 99
// data isDeveloper: true
// data gender: male
```



我们也可以使用 `Object.keys(对象)` 来获取对象中所有键，然后通过 `for` 循环遍历所有键值对。这个方法比较复杂，不推荐。

```js
const keys = Object.keys(intro);
for(let i = 0; i < keys.length; i++){
  console.log('data '+ keys[i] + ': ' + intro[keys[i]])
}
```



## 删除

你可以使用 `delete` 关键字来删除对象中的键值对

```js
delete wtf.name;
// 或 delete wtf["name"];
console.log(Object.keys(wtf)); // hello
```



## 习题

补全下面的 `isDev` 函数，完成逻辑，当输入的对象 `obj` 的 `isDeveloper` 属性为 `true` 时，返回 `true`，否则返回 `false`。

```js
function isDev(obj){
	if(obj.isDeveloper===true){
        return true;
    }
    else return false;
}

const obj1 = {
  name: "0xAA",
  isDeveloper: true,
}
const obj2 = {
  name: "Trump",
}
console.log(isDev(obj1)); // 应该输出 true
console.log(isDev(obj2)); // 应该输出 false
```



## 总结

这一讲我们介绍了 Javascript 中的对象，包括定义，读取，写入，遍历，和删除。JavaScript 中的所有事物都是对象，包括字符串、数值、数组、函数，你一定哟好好掌握。

# 10. 异步

这一讲，我们介绍 JavaScript 中的异步，着重讲 `async/await` 语法。

## 异步编程



![img](https://www.wtf.academy/assets/images/10-1-5ce61b9b89a9caf5dbb79843de8b5c7e.png)



JavaScript 是单线程的编程语言，浏览器按照我们代码的顺序一行一行地执行程序。如果执行到一个耗时很长的任务，后面的任务就会被阻塞，拖延整个程序的执行。异步编程技术允许我们执行一个长时间任务时，程序不需要进行等待，而是继续执行后面的代码，直到任务完成之后再回来通知。这大大提高了程序的效率，尤其是对于输入输出密集的程序，比如文件读取，数据库查询，网络访问。

### 回调函数

在 JavaScript 中，函数也是对象，可以作为参数传入另一个函数，这也被称为回调函数。它曾经是 JavaScript 中实现异步函数的主要方式。下面是一个经典的例子，我们定义了一个 `callback()` 函数，并作为参数传给了 `setTimeout()` 定时器函数：

```js
function callback() {
  console.log('Hello, JavaScript!');
}

setTimeout(callback, 1000);
console.log('hello');
// hello
// Hello, JavaScript! (1 秒后输出)
```



上面的程序会先输出 `hello`，然后再等待 1 秒后执行 `callback` 函数，输出`“Hello, JavaScript!”`，即使 `setTimeout` 函数在 `console.log("hello")` 之前。对 `setTimeout` 更详细的介绍请阅读[MDN教程](https://developer.mozilla.org/zh-CN/docs/Web/API/setTimeout)。

但如果异步任务数量很多时，这种方案容易出错，下面是使用回调函数维护 3 个异步任务的例子：

```js
setTimeout(() => {
  console.log('Hello, WTF JavaScript!'); // 第一步，输出这条消息
  setTimeout(() => {
    console.log('Hello, WTF HTML!'); // 第二步，输出这条消息
    setTimeout(() => {
      console.log('Hello, WTF CSS!'); // 第三步，输出这条消息
    }, 1000); // 此消息在第二条消息之后1秒输出
  }, 1000); // 第二条消息在第一条消息之后1秒输出
}, 1000); // 第一条消息在1秒后输出

```

这种代码极难维护，也被称为 “回调地狱” （callback hell），现已被 `Promise` 方案取代。

### Promise



![img](https://www.wtf.academy/assets/images/10-2-b56a4f7336d1299b96d545e866bdae2b.png)



`Promise` （承诺）是异步编程的现代解决方案，比回调函数方案更强大。它由社区最早提出和实现，ES6 将其写进语言标准并统一用法，原生提供了 `Promise` 对象。

`Promise` 对象有三种状态：`pending`（进行中）、`fulfilled`（已成功）和 `rejected`（已失败）。初始状态为 `pending`，最终状态由异步操作的结果决定。`Promise` 对象的状态改变，只有两种可能：从 `pending` 变为 `fulfilled` 和从 `pending` 变为 `rejected`。下面我们用 `Promise` 重写第一个示例:

```js
// 定义 promise 实例
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Hello, JavaScript Promise!'); // 经过 1 秒后，调用 resolve，传递消息
  }, 1000)
})

// 运行 Promise 实例
promise.then((value) => {
  console.log(value); // 当 promise 被解析时，输出传递的消息
})

console.log('hello Promise'); // 立即输出这条消息

// hello Promise
// Hello, JavaScript Promise! (1 秒后输出)
```



由于 `Promise` 比较复杂，我们在后面的教程中再详细讲解。这一讲我们着重介绍在它之上建立的 `async/await` 语法。

## async/await

async/await 是 `Promise` 的语法糖，让异步编程更易于理解和使用。

### async 函数

我们可以在一个函数前面加上 `async` 关键字 ，将它变为异步函数，它的返回值会被自动包装为一个 `Promise`。与普通函数不同，异步函数不会阻塞程序的运行，让 JavaScript 引擎同时处理其他任务：执行其他脚本，处理事件等。

```js
async function hello() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('Hello, JavaScript async!');
    }, 1000)
  })
}
```



### await 关键字

`await` 关键字**只能在** `async` 函数内工作，一般情况下，`await` 后跟随一个 `Promise` 对象，作用是让 JavaScript 引擎等待直到 `Promise` 完成并返回结果。

```js
async function helloAwait() {
  const value = await hello();
  console.log(value);
  console.log('hello await');
}
helloAwait()
// Hello, JavaScript async! (1 秒后输出)
// hello await
```



注意，上面的代码会等待 1 秒后输出 `Hello async`，然后才是 `hello await`。

### async/await 例子



![img](https://www.wtf.academy/assets/images/10-3-21319392c68efd9c5a49e91eb238458b.png)



下面，我们演示如何使用 `async/await` 语法来读取非常流行的无聊猿（BAYC）NFT的元数据。

1. NFT 元数据是构成 NFT 内容的一组数据，通常以 [JSON](https://zh.wikipedia.org/wiki/JSON) 格式保存在网络上。比如下面 `url` 中的 [ipfs](https://gateway.ipfscdn.io/ipfs/QmeSjSinHpPnmXmspMjwiXyN6zS4E9zccariGR3jxcaWtq/1) 链接保存着 `id = 1` 的BAYC元数据，包括小图片网址和属性（嘴、头发、衣服等特征）。

   ```js
   const url = `https://ipfs.io/ipfs/QmeSjSinHpPnmXmspMjwiXyN6zS4E9zccariGR3jxcaWtq/1`;
   // 数据形式
   // {"image":"ipfs://QmPbxeGcXhYQQNgsC6a36dDyYUcHgMLnGKnF8pVFmGsvqi","attributes":[{"trait_type":"Mouth","value":"Grin"},{"trait_type":"Clothes","value":"Vietnam Jacket"},{"trait_type":"Background","value":"Orange"},{"trait_type":"Eyes","value":"Blue Beams"},{"trait_type":"Fur","value":"Robot"}]}
   ```

   

2. 你可以使用 `fetch()` 函数来进行 HTTP 访问，获取网络数据。它会返回一个包装成 `Promise` 的 HTTP 响应，因此你需要使用 `await` 关键字来获取结果 `response`。然后，你需要用 `json()` 方法获取 JSON 的内容，也就是元数据。

   ```js
   const response = await fetch(url);
   const BaycMetadata = await response.json();
   ```

   

3. 将上面的代码组合成一个 `async` 函数 `getBaycMetadata`:

```js
// async/await 示例
async function getBaycMetadata(){
  const url = `https://ipfs.io/ipfs/QmeSjSinHpPnmXmspMjwiXyN6zS4E9zccariGR3jxcaWtq/1`;
  const response = await fetch(url);
  const BaycMetadata = await response.json();
  console.log(BaycMetadata);
}
getBaycMetadata()
// image: "ipfs://QmPbxeGcXhYQQNgsC6a36dDyYUcHgMLnGKnF8pVFmGsvqi"
// attributes...
```

> [!TIP]
>
> ### 代码功能
>
> 1. **定义异步函数**: `async function getBaycMetadata()` 定义了一个异步函数，可以使用 `await` 关键字。
> 2. **发送请求**: `fetch(url)` 发送 HTTP GET 请求到指定的 URL，返回一个 Promise。
> 3. **等待响应**: `await fetch(url)` 会等待 `fetch` 的 Promise 被解析，并将响应结果赋值给 `response` 变量。
> 4. **解析 JSON**: `await response.json()` 将响应内容解析为 JSON 格式，并赋值给 `BaycMetadata` 变量。
> 5. **输出结果**: `console.log(BaycMetadata)` 输出解析后的数据。



## 习题

基于这一讲的例子，写一个根据用户输入的 tokenId（1~10000）来获取相应的无聊猿的元数据。

> 提示: 示例中url的最后一位的代表 tokenId，可以使用 `{$tokenId}` 进行替换。

```jsx
function getBaycMetadataById(tokenId) {
  
}
```

GPT

```js
async function getBaycMetadataById(tokenId) {
  // 检查 tokenId 是否在有效范围内
  if (tokenId < 1 || tokenId > 10000) {
    console.log('请提供有效的 tokenId（1~10000）');
    return;
  }

  // 构建 URL，替换 tokenId
  const url = `https://ipfs.io/ipfs/QmeSjSinHpPnmXmspMjwiXyN6zS4E9zccariGR3jxcaWtq/${tokenId}`;

  try {
    // 使用 await 等待 fetch 的响应
    const response = await fetch(url);
    
    // 检查响应是否成功
    if (!response.ok) {
      throw new Error('网络错误或资源未找到');
    }

    // 解析响应为 JSON
    const baycMetadata = await response.json();

    // 输出元数据
    console.log(baycMetadata);
  } catch (error) {
    // 捕获并输出错误信息
    console.error('获取元数据时出错:', error);
  }
}

// 示例：获取用户输入的 tokenId（假设为 5）
const tokenIdInput = prompt('请输入 tokenId（1~10000）:'); // 用户输入
getBaycMetadataById(Number(tokenIdInput)); // 转换为数字并调用函数

```



## 总结

这一讲我们介绍了 JavaScript 的异步编程，包括回调函数，Promise，以及重点讲的 async/await，并且利用它获取了无聊猿NFT的元数据。Promise 是现代 JavaScript 异步编程的基础。它避免了深度嵌套回调，使表达和理解异步操作序列变得更加容易。async/await 使得从一系列连续的异步函数调用中建立一个操作变得更加容易，避免了创建显式 Promise 链，并允许你像编写异步代码那样编写同步代码。

# 11. Node.js

Node.js 或 Node 是一个开源的、跨平台的 JavaScript 运行环境，它让 JavaScript 可以脱离浏览器环境在服务器上运行。在这一章中，我们将介绍 Node.js 的基础知识，包括如何安装和使用 Node.js，以及如何使用 npm（Node 包管理器）管理项目的依赖。

## 安装Node.js

首先，你需要在你的电脑上安装 Node.js。你可以从 Node.js 的官方网站（https://nodejs.org/zh-cn） 下载对应你的操作系统的安装包，并按照提示进行安装。

安装完成后，你可以在命令行中输入 `node -v` 来查看你的 Node.js 版本：

```bash
$ node -v
v18.16.0
```



## Node.js REPL

Node.js 提供了一个交互式运行环境，叫做 REPL（Read-Eval-Print Loop）。在 REPL 中，你可以输入并执行 JavaScript 代码，查看代码的执行结果。

要启动 Node.js REPL，你只需要在命令行中输入 `node`，然后就可以开始输入 JavaScript 代码了：

```bash
$ node
> console.log('Hello, WTF Node.js!');
Hello, WTF Node.js!
```



## Node.js 模块

在 Node.js 中，每个文件都是一个模块。你可以使用 `require` 函数导入其他模块，使用 `module.exports` 或 `exports` 导出模块：

```javascript
// lib.js
module.exports = 'Hello, WTF Node.js!';

// app.js
let message = require('./lib');
console.log(message);  // 输出 'Hello, WTF Node.js!'
```

> [!TIP]
>
> 在 `lib.js` 文件中，我们使用 `module.exports` 导出一个字符串。这使得其他模块可以导入这个字符串并使用它。
>
> 在 `app.js` 文件中，我们使用 `require('./lib')` 导入 `lib.js` 模块。`require` 函数会返回 `lib.js` 中导出的内容，然后我们将其赋值给 `message` 变量。最后，使用 `console.log(message)` 输出消息。

在上面的例子中，我们创建了两个 `js` 文件 `lib.js` 和 `app.js`，你可以在命令行输入 `node app.js`，会得到输出 'Hello, WTF Node.js!'。

> [!TIP]
>
> ### 运行示例
>
> 1. 创建两个文件 `lib.js` 和 `app.js`，并将上面的代码复制到相应的文件中。
>
> 2. 在命令行中，导航到包含这两个文件的目录。
>
> 3. 输入以下命令运行 `app.js`：
>
>    ```bash
>    node app.js
>    ```
>
> ### 输出结果
>
> 运行 `node app.js` 后，你将看到控制台输出：
>
> ```
> Hello, WTF Node.js!
> ```



## npm（Node 包管理器）

npm 是 Node.js 的默认包管理器。你可以使用 npm 来安装和管理你的项目的依赖。在命令行中输入 `npm -v` 可以查看你的 npm 版本：

```bash
$ npm -v
8.11.0
```



要使用 npm 创建一个新的项目，你可以使用 `npm init` 命令。这个命令会引导你创建一个 `package.json` 文件，这个文件用来保存你的项目的配置和依赖信息。

要安装一个新的依赖，你可以使用 `npm install` 命令：

```bash
$ npm install express
```



## 总结

这一讲，我们介绍了 Node.js 的基础知识。掌握 Node.js，你就可以使用 JavaScript 来创建服务器端的应用/脚本，这将大大扩展你的 JavaScript 编程能力。

# 12. 闭包

闭包是 JavaScript 中的一种重要概念和关键特性。了解和理解闭包对于编写高效且高质量的 JavaScript 代码十分关键。在这一章，我们将详细讲解闭包的概念，理解它的运作方式以及它在实际开发中的应用。

## 什么是闭包

在 JavaScript 中，闭包是一个函数和其所在的作用域的组合。这个环境包含了这个闭包创建时所能访问的所有局部变量。换句话说，闭包可以让你从内部函数访问到外部函数作用域。

在 JavaScript 中，函数是一级公民，这意味着函数可以作为参数传递，也可以作为返回值返回。当函数在其声明的作用域之外执行时，会形成闭包。

举个例子：

```javascript
function outerFunction(outerVariable) {
  return function innerFunction(innerVariable){
    console.log('outerVariable:', outerVariable);
    console.log('innerVariable:', innerVariable);
  }
}

const newFunction = outerFunction('outside');
newFunction('inside'); 
//outerVariable: outside
//innerVariable: inside

```

> [!TIP]
>
> **外部函数 `outerFunction`**:
>
> - 接受一个参数 `outerVariable`。
> - 返回一个内部函数 `innerFunction`，这个内部函数可以访问 `outerVariable`。
>
> **创建闭包**:
>
> - 当调用 `outerFunction('outside')` 时，返回的 `innerFunction` 仍然可以访问 `outerVariable` 的值（即 `'outside'`）。这个访问能力即构成了闭包。
>
> **调用内部函数**:
>
> - `newFunction('inside')` 实际上是在调用 `innerFunction`，传递的参数 `innerVariable` 是 `'inside'`。
> - 在 `innerFunction` 中，`outerVariable` 和 `innerVariable` 都被打印出来。

在上述代码中，`innerFunction` 保持对 `outerFunction` 的 `outerVariable` 的引用，即使 `innerFunction` 在其声明的环境之外执行。这种情况就形成了一个闭包。

## 闭包的规则和行为

闭包的行为和规则主要受 JavaScript 的作用域和变量生命周期影响。下面是几点需要注意的地方：

1. 闭包有权访问外部函数的变量和参数，但是并不会复制这些数据，而是通过引用的方式使用它们。也就是说，闭包可以修改这些变量的值。
2. 闭包拥有外部函数的所有变量，直到外部函数结束执行，这些变量才会被垃圾收集器回收。
3. 闭包可以形成在循环中。例如，如果你在一个循环中创建函数，并且这个函数访问了循环的计数器变量，那么每个函数都会创建一个新的闭包，并分别保存各自的计数器值。
4. 由于闭包可以访问外部函数的变量，因此它们也可以用于实现私有变量和方法，这在构造函数和对象方法中特别有用。

使用闭包时需要注意，由于闭包可以访问外部函数的变量，且这些变量不会被垃圾回收，如果不恰当地使用闭包，可能会导致内存泄露。

## 应用

闭包的应用非常广泛，其中最常见的用途是创建私有变量和实现数据封装。假设我们有这样一个场景：领导让你统计一个业务函数累计被调用的次数。于是你撸起袖子写出了以下代码

```js
let count = 0; // 用于统计func函数被调用次数

function func() {
  count++;
  // 业务逻辑
  return count;
}

console.log(count);
```



正当你胸有成竹地测试时，发现 `count` 的值出现了一些问题，有时候甚至会变少，这时候你就开始排查问题，终于发现了这么一段代码：

```js
var count = 0; // 用于统计xxx的数量

function func2() {
  count = xxx; // 改变 count 的业务代码
}
```



这时候你恍然大悟，原来同事之前就在全局定义了一个 `count` 用于统计其他业务。第一时间你想到了给自己的 `count` 改个名，改成 `count2` 。当然，这样也可以解决眼下的问题，但是，有没有更好的办法呢。这时候，闭包就可以发挥它的作用了，下面是用闭包实现

```js
function func2() {
  let count = 0;
  return function () {
    count++;
    return count;
  };
}

let addCount = func2();

console.log(addCount()); // 1
console.log(addCount()); // 2
```

> [!TIP]
>
> **创建私有变量**:
>
> - 在 `func2` 中定义的 `count` 是一个局部变量，外部无法直接访问。通过闭包的方式，这个变量在 `func2` 的返回函数中得以保留。
>
> **返回内部函数**:
>
> - `func2` 返回的内部函数可以访问其外部作用域中的 `count` 变量。当你调用 `addCount()` 时，内部函数中的 `count` 将被递增。
>
> **避免全局污染**:
>
> - 由于 `count` 是局部变量，它不会与全局作用域中的同名变量发生冲突，从而避免了意外修改的问题。

通过以上代码，每次调用 `addCount` 函数都会使 `count` 的值递增1，并且返回最新的 `count` 值。通过以上代码，无需改变变量名，保证了代码可读性的同时解决了业务问题。

## 总结

闭包是 JavaScript 中的一个重要特性，就是函数不在定义的词法作用域内被调用，但是仍然可以访问词法作用域中定义的变量。它的最大用处有两个，一个是前面提到的可以==防止变量被污染==，另一个就是让这些变量的值始终保持在内存中。理解并熟练掌握闭包对于编写高效且高质量的 JavaScript 代码是非常关键的。

# 13. 引用类型

在 JavaScript 中，变量可以被定义为值类型（也称为基础类型）或引用类型。

## 值类型

值类型包括 Boolean、null、undefined、String、Number、BigInt 和 Symbol。这些类型的数据被存储在栈内存中。当你把一个值类型的变量赋值给另一个变量时，新变量会获得原始变量的一个完整复制。

让我们来看一个例子：

```javascript
let a = 10;
let b = a; // b 是 a 的复制
a = 20;
console.log(b); // 输出 10, b 的值并没有改变
```



## 引用类型

引用类型包括 Object、Array、Function、Map、Set 等。这些类型的数据被存储在堆内存中，变量实际上存储的是指向堆内存中的该值的指针。当你把一个引用类型的变量赋值给另一个变量时，新变量得到的是对原始数据的一个引用，而不是一个完整的复制。这就意味着，如果我们改变了其中一个变量，另一个变量也会受到影响。

```javascript
let obj1 = { value: 10 };
let obj2 = obj1;
obj2.value = 20;
console.log(obj1.value); // 20
```



那么如果你想要复制一个对象，且让新的对象和原始对象没有任何关联该怎么办？这就需要进行深拷贝。

## 如何复制

对于值类型的变量，我们可以通过简单赋值的方式进行复制。

对于引用类型，如果你想要得到一个新的，完全独立的复制，而不是一个引用，你需要进行深拷贝。深拷贝就是将一个对象的所有元素，包括属性和子对象都进行复制，新的对象和原来的对象没有任何关联。在 JavaScript 中，我们可以通过 `JSON.parse` 和 `JSON.stringify` 方法：

```js
// 深拷贝
let x = {
  name: "wtf",
  age: 18,
  arr: [],
  obj: {
    a: 1,
  },
};

let y = JSON.parse(JSON.stringify(a));

y.obj.a = 2;

console.log("x: ", x);
console.log("y: ", y);
```

> [!TIP]
>
> - 使用 `JSON.stringify(x)` 将对象 `x` 转换为 JSON 字符串。
> - 然后，使用 `JSON.parse(...)` 将这个 JSON 字符串转换回一个新的对象 `y`。
> - 此时，`y` 是 `x` 的深拷贝，它包含所有的属性和嵌套对象，但与 `x` 完全独立。

虽然大多数时候这么使用是没有问题的，但这种方式还是有很多缺点的

1. 对象中有字段值为 `undefined`，转换后字段会直接消失
2. 对象如果有字段值为 `RegExp` 对象，转换后字段值会变成 `{}`
3. 对象如果有字段值为 `NaN`、`+-Infinity`，转换后字段值变成 `null`
4. 对象如果有 `环引用`，转换直接报错。

对于更复杂的对象，你可以使用第三方库如 `lodash` 的 `_.cloneDeep` 方法。

## 总结

这一讲，我们介绍了 JavaScript 中的引用类型，了解了如何复制值类型和引用类型的变量，并且探讨了深拷贝的方法和其局限性。在 JavaScript 编程中，理解值类型和引用类型的区别以及如何进行正确的复制是非常重要的。

# 14. 原型链

JavaScript 是一种基于原型的语言，这意味着对象之间的关系不是通过类（class）来建立的，而是通过原型（prototype）。

## 原型（Prototype）

原型是 JavaScript 中的一个内部对象，它可以让我们共享方法和属性。每当创建一个新对象时，我们实际上都是在复制一个存在的原型对象。新对象继承了原型对象的属性。这种继承是动态的，如果我们改变原型对象，那么所有基于该原型的对象都将受到影响。

原型（`Prototype`）、原型链（`__proto__`）、函数、对象是密切相关的概念，简单来说：

1. 每个函数在创建时都会有一个名为 `prototype` 的属性，它指向函数的原型对象。当以构造函数方式调用（即通过 `new` 关键字）时，新创建的对象会继承该函数的原型。

   ```javascript
   // 定义构造函数 Animal
   function Animal(name) {
       this.name = name; // 实例属性
   }
   
   // 在 Animal 的原型上添加 breathe 方法
   Animal.prototype.breathe = function() {
       console.log(this.name + " can breathe."); // 使用 this 访问实例属性
   }
   
   // 创建 Animal 的一个实例 dog
   let dog = new Animal('Dog');
   
   // 调用 dog 的 breathe 方法
   dog.breathe(); // 输出：Dog can breathe.
   
   ```

   

2. 每一个 JavaScript 对象（函数也是对象）都有一个通过 `__proto__` 属性关联的原型对象，从它那里继承属性，这也被称为原型链。

   ```js
   // 定义一个对象 animal
   let animal = {
       eats: true
   };
   
   // 创建一个新对象 rabbit，使用 animal 作为其原型
   let rabbit = Object.create(animal);
   
   // 输出 rabbit 对象的 eats 属性
   console.log(rabbit.eats); // true
   
   // 检查 rabbit 的 __proto__ 是否指向 animal
   console.log(rabbit.__proto__ === animal); // true
   
   ```

   

下面我们展开讲一下。

## 原型和构造函数

在 JavaScript 中，函数也是对象。当我们使用 `new` 关键字来调用一个函数（此时我们称之为构造函数）时，JavaScript 会创建一个新的对象，并将这个对象的原型设置为构造函数的`prototype`属性。如果按照面向对象的方式编写代码，那么这个属性将非常有用。

```javascript
// 声明函数对象 Person
function Person(name, age) {
  this.name = name; // 设置实例的 name 属性
  this.age = age;   // 设置实例的 age 属性
}

// 在 Person 的原型上添加 greet 方法
Person.prototype.greet = function() {
  console.log(`Hello, 我叫 ${this.name}, 我 ${this.age} 岁了。`); // 使用模板字符串输出
};

// 创建 Person 的一个实例 alice
const alice = new Person('Alice', 25);

// 调用 alice 的 greet 方法
alice.greet();  // 输出: Hello, 我叫 Alice, 我 25 岁了.

```



在上述代码中，`Person`是一个构造函数，我们创建了一个新的`Person`实例`alice`。`alice` 的原型就是 `Person.prototype`，即`alice.__proto__ === Person.prototype`。因此`alice`可以访问在`Person.prototype`上定义的所有属性和方法。

## 原型链

在 JavaScript 中，几乎所有的对象在创建的时候都会关联到另一个对象，这个被关联的对象就是原型对象。当我们试图访问一个对象的某个属性时，JavaScript 首先在这个对象本身上查找这个属性。如果找不到，那么 JavaScript 就会去这个对象的原型对象中寻找。如果原型对象中也没有，那么 JavaScript 就会继续在原型对象的原型对象上查找，一直这样查找下去，直到找到这个属性，或者查找到原型链的顶端 `null` 为止。这就形成了一条原型链。

```javascript
// 声明函数对象 Person
function Person(name, age) {
  this.name = name; // 将参数赋值给实例属性
  this.age = age;
}

// 在原型上添加 greet 方法
Person.prototype.greet = function() {
  console.log(`Hello, 我叫 ${this.name}, 我 ${this.age} 岁了。`);
};

// 创建 Person 的一个实例 alice
const alice = new Person('Alice', 25);

// 检查原型关系
console.log(alice.__proto__ === Person.prototype); // true
console.log(Person.prototype.__proto__ === Object.prototype); // true
console.log(Object.prototype.__proto__ === null); // true

```



在上述代码中，实例`alice`是由 Person 构造函数创建而来，对象可以通过`__proto__`属性访问该对象的原型对象，所以`alice.__proto__ === Person.prototype`。由于`Person.prototype`也是一个对象，同样具备`__proto__`属性，而该对象是`Object`的实例，所以`Person.prototype.__proto__ === Object.prototype`。`Object.prototype.__proto__`是原型链的顶端，即`null`。

```javascript
console.log(alice.toString());  // [object Object]
```



在上述代码中，`toString`方法并不在`alice`或`Person.prototype`上，但 JavaScript 在`Object.prototype`上找到了它，因为`Person.prototype`的原型就是`Object.prototype`，即`Person.prototype.__proto__ === Object.prototype`。

通过原型链，所有的对象都可以访问`Object.prototype`上的属性和方法，这就是我们为什么可以在任何对象上调用`toString`或`hasOwnProperty`等方法的原因。

## 总结

本节我们学习了原型（`prototype`）和原型链（`__proto__`）的相关知识。原型和原型链在 JavaScript 中是非常重要的概念，它们是实现 JavaScript 继承和属性查找机制的核心。

# 15. 继承

继承是一种在更为普遍、通用的类（父类）的基础上创建更为特定、专用类（子类）的方法。子类可以通过父类那里继承属性和方法。JavaScript 是一种基于原型的语言，这意味着对象可以从其他对象继承属性和方法。这种机制使我们可以在不同的对象之间共享代码，提高代码重用性。

## 原型链继承

JavaScript 最原始的继承方式是通过原型链。如果一个对象的属性在该对象上不存在，JavaScript 将会在该对象的原型（即 `__proto__` 属性或其构造函数的 `prototype` 属性）上寻找该属性，如果仍然找不到，就会去原型的原型上找，以此类推，直到找到该属性或者到达原型链的尽头（`null`）。

```javascript
function Parent() {
  this.name = 'Parent';
}

Parent.prototype.getName = function() {
  return this.name;
}

function Child() {
  this.name = 'Child';
}

// 设置 Child 的原型为 Parent 的实例
Child.prototype = new Parent();
Child.prototype.constructor = Child;

const child = new Child();
console.log(child.getName());  // 输出 "Child"
```



在上述代码中，`Child` 的原型被设置为 `Parent` 的一个实例，即`Child.prototype.__proto__ === Parent.prototype`。所以 `Child` 的实例可以通过原型链访问 `Parent` 的原型上的 `getName` 方法。

## 类继承

ES6 引入了类（class）语法，使得基于原型的继承看起来更像传统的基于类的继承。我们可以使用 `extends` 关键字来创建一个子类。

```javascript
class Parent {
  constructor() {
    this.name = 'Parent';
  }

  getName() {
    return this.name;
  }
}

class Child extends Parent {
  constructor() {
    super();  // 调用父类的 constructor
    this.name = 'Child';
  }
}

const child = new Child();
console.log(child.getName());  // 输出 "Child"
```



在上述代码中，`Child` 继承自 `Parent`，`Child` 的实例可以访问 `Parent` 中定义的 `getName` 方法。一般来说，当一个类继承自另一个类时，子类的构造函数会首先通过`super()`调用父类的构造函数，然后再进行自己的初始化。具体来说，父类构造函数被调用时，`this.name` 被设置为`Parent`，但是这个值在子类构造函数中被覆盖了。

需要注意的是，JavaScript 的类实际上仍然是基于原型的。`Child extends Parent` 实际上是设置了 `Child.prototype` 的原型为 `Parent.prototype`，即`Child.prototype.__proto__ === Parent.prototype`。所以 `Child` 的实例可以访问 `Parent.prototype` 上的属性和方法。

## 总结

JavaScript 的继承是一个非常重要的概念，理解它将帮助你编写出更优雅、更高效的代码。

# 16. DOM

在 JavaScript 中，DOM（文档对象模型）和 BOM（浏览器对象模型）是两个重要的概念。DOM 用于访问和操作 HTML 文档中的元素，而 BOM 则提供了与浏览器窗口进行交互的方法和属性。本节将介绍 DOM 和 BOM 的基本概念，帮助您更好地理解和运用它们。

这一讲所使用的 HTML 代码:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>DOM And BOM</title>
</head>
<body>
  <div id="myId"></div>
  <div class="myClass"></div>
  <div class="myClass"></div>
  <script src="./DOMAndBOM.js"></script>
</body>
</html>
```

> [!NOTE]
>
> 你的代码是一个基本的 HTML 文件结构，其中包括了一个标题和一些 `<div>` 元素。接下来是对这个 HTML 代码的详细解析，以及在 `DOMAndBOM.js` 文件中可以实现的 DOM 操作示例。
>
> ### HTML 结构解析
>
> 1. **文档类型声明**:
>    ```html
>    <!DOCTYPE html>
>    ```
>    - 这是文档类型声明，告知浏览器使用 HTML5 解析该文档。
>
> 2. **HTML 标签**:
>    ```html
>    <html lang="en">
>    ```
>    - 这是根元素，表示该文档使用英语。
>
> 3. **头部部分**:
>    ```html
>    <head>
>      <meta charset="UTF-8">
>      <meta http-equiv="X-UA-Compatible" content="IE=edge">
>      <meta name="viewport" content="width=device-width, initial-scale=1.0">
>      <title>DOM And BOM</title>
>    </head>
>    ```
>    - `<meta charset="UTF-8">` 指定文档使用 UTF-8 字符编码。
>    - `<meta http-equiv="X-UA-Compatible" content="IE=edge">` 确保 IE 浏览器使用最新的渲染引擎。
>    - `<meta name="viewport" content="width=device-width, initial-scale=1.0">` 使网页在移动设备上更好地响应。
>    - `<title>` 设置网页的标题，在浏览器标签中显示。
>
> 4. **主体部分**:
>    ```html
>    <body>
>      <div id="myId"></div>
>      <div class="myClass"></div>
>      <div class="myClass"></div>
>      <script src="./DOMAndBOM.js"></script>
>    </body>
>    ```
>    - `<body>` 包含了页面的主要内容。
>    - 第一个 `<div>` 使用 `id` 选择器（`#myId`），可以通过 JavaScript 轻松访问。
>    - 接下来的两个 `<div>` 使用相同的 `class` 名称（`.myClass`），可以通过 `class` 选择器访问。
>    - 最后，`<script>` 标签引入了外部 JavaScript 文件 `DOMAndBOM.js`，用来执行 DOM 和 BOM 的操作。
>



## DOM

DOM（文档对象模型）是一种用于表示和操作 HTML 和 XML 文档的 API。它将文档表示为由节点和对象（包括元素，属性，文本等）组成的树形结构。通过操作 DOM，JavaScript 能够动态地添加、删除和修改 HTML。

### 选择元素

首先，你需要知道如何选择你要操作的元素。JavaScript 提供了多种方式来选择元素：

| 方法                   | 描述                                                         |
| ---------------------- | ------------------------------------------------------------ |
| getElementById         | 根据元素的 id 选择元素。                                     |
| getElementsByClassName | 根据元素的类名选择元素，返回一个包含所有匹配元素的 NodeList。 |
| getElementsByTagName   | 根据元素的标签名选择元素，返回一个包含所有匹配元素的 NodeList。 |
| querySelector          | 使用 CSS 选择器选择元素，只返回第一个匹配的元素。            |
| querySelectorAll       | 使用 CSS 选择器选择元素，返回一个包含所有匹配元素的 NodeList。 |

例如：

```javascript
const el = document.getElementById('myId') // 选择 id 为 'myId' 的 div 元素
const elBySelector = document.querySelector('#myId') // 选择 selector 为 'myId' 的 div 元素，值返回第一个匹配的元素

const els = document.getElementsByClassName('myClass') // 选择所有 class 为 'myClass' 的 div 元素
const elsByTag = document.getElementsByTagName('div')
const elsBySelectorAll = document.querySelectorAll('.myClass')
```



### 修改内容

选择元素后，你就可以修改它的内容。你可以通过 `innerHTML` 或 `textContent` 属性来修改元素的 HTML 或文本内容。

```javascript
const el = document.querySelector('#myId')
el.innerHTML = '<strong>Hello, WTF JavaScript!</strong>' // 修改 HTML 内容
el.textContent = 'Hello, WTF JavaScript!' // 修改文本内容
```

> [!NOTE]
>
> 在 JavaScript 中，`const` 声明的变量表示的是常量，即其引用不能被重新赋值，但并不意味着引用的对象本身是不可变的。对于使用 `const` 声明的对象或 DOM 元素来说，虽然不能更改该常量的引用，但可以修改其内部的属性或方法。
>
> 在你的例子中：
>
> ```javascript
> const el = document.querySelector('#myId');
> ```
>
> `el` 作为一个 DOM 元素的引用，它的引用不能被重新赋值为其他元素。然而，这并不影响你对这个元素内部内容的修改。例如，你可以通过 `innerHTML` 或 `textContent` 修改它的内容：
>
> - `el.innerHTML` 修改的是元素的 HTML 内容，可以插入 HTML 标签；
> - `el.textContent` 修改的是纯文本内容，不会解析 HTML 标签。
>
> 示例：
>
> ```javascript
> const el = document.querySelector('#myId');
> 
> // 修改为带 HTML 的内容
> el.innerHTML = '<strong>Hello, WTF JavaScript!</strong>'; 
> 
> // 修改为纯文本内容
> el.textContent = 'Hello, WTF JavaScript!';
> ```
>
> 在这两个操作中，`el` 的引用没有被修改，因此它是符合 `const` 的约束的。



### 修改样式

你也可以通过操作 `style` 属性来修改元素的样式。注意，所有的 CSS 属性名都需要转换为驼峰命名法。

```javascript
const el = document.querySelector('#myId')
el.style.color = 'red' // 修改文本颜色
el.style.backgroundColor = 'black' // 修改背景颜色
```

> [!NOTE]
>
> 在 JavaScript 中，通过操作 DOM 元素的 `style` 属性，可以动态修改元素的内联样式（即通过 HTML `style` 属性直接设置的样式）。例如，设置颜色、背景、宽度等 CSS 属性。
>
> **关键点：**
> - 在 JavaScript 中操作 CSS 属性时，CSS 属性名中的短横线（`-`）需要转换为 **驼峰命名法**。
> - **驼峰命名法**：将 CSS 属性的短横线去掉，并把后面单词的首字母大写。例如：
>   - `background-color` → `backgroundColor`
>   - `font-size` → `fontSize`
>
> 这样，JavaScript 可以识别这些属性并对元素应用相应的样式。
>
> ### 示例
>
> ```javascript
> const el = document.querySelector('#myId');
> 
> // 修改文本颜色为红色
> el.style.color = 'red';
> 
> // 修改背景颜色为黑色
> el.style.backgroundColor = 'black';
> ```
>
> **解释：**
> - `el.style.color = 'red'`：修改了元素文本的颜色为红色。
> - `el.style.backgroundColor = 'black'`：将元素的背景颜色设置为黑色。
>
> 通过这种方式，你可以在 JavaScript 中动态控制 DOM 元素的样式。



### 添加和删除元素

使用 `createElement`，`appendChild` 和 `removeChild` 方法，你可以动态地添加和删除元素。

```javascript
const newEl = document.createElement('div') // 创建新元素
document.body.appendChild(newEl) // 添加新元素

const oldEl = document.querySelector('#myId')
document.body.removeChild(oldEl) // 删除元素
```



## BOM

BOM（浏览器对象模型）是一个表示浏览器及其组件的编程接口。BOM 允许开发者控制浏览器的行为和交互，如弹出新窗口、获取浏览器窗口的尺寸等。BOM 的核心对象是 window，它表示浏览器窗口或者一个框架。以下是一些常见的 BOM 操作示例：

### 打开新窗口

你可以通过 `window.open` 方法打开一个新窗口。

```javascript
window.open('https://wtf.academy', '_blank') // 在新窗口中打开 WTF Academy
```



### 获取和设置窗口尺寸

你可以通过 `window.innerWidth` 和 `window.innerHeight` 属性获取窗口的宽度和高度。

```javascript
const width = window.innerWidth // 获取窗口宽度
const height = window.innerHeight // 获取窗口高度

console.log(`窗口宽度：${width}，窗口高度：${height}`)
```



### 设置定时器

你可以通过 `setTimeout` 和 `setInterval` 方法设置定时器。

```javascript
setTimeout(() => { //箭头函数
  console.log('Hello, WTF JavaScript!')
}, 1000) // 1 秒后输出 Hello, WTF JavaScript!

setInterval(() => {
  console.log('Hello, WTF JavaScript!')
}, 1000) // 每隔 1 秒输出 Hello, WTF JavaScript!
```

> [!TIP]
>
> `setTimeout()` 是 JavaScript 中用于延迟执行代码的函数。它允许你在指定的时间之后运行一次函数或代码片段。
>
> ### 语法：
>
> ```js
> setTimeout(function, delay, param1, param2, ...)
> ```
>
> - **`function`**：要在延迟后执行的函数。可以是匿名函数或已定义的函数。
> - **`delay`**：延迟的时间（以毫秒为单位），在此时间之后执行 `function`。1秒 = 1000毫秒。
> - **`param1, param2, ...`**：可选参数，这些参数会在执行的函数中传入。
>
> ### 返回值：
> - `setTimeout()` 返回一个**定时器 ID**。你可以使用这个 ID 来清除定时器，防止它的执行（通过 `clearTimeout()`）。
>
> ### 基本用法：
>
> ```js
> setTimeout(() => {
>     console.log("3秒后执行的代码");
> }, 3000);
> ```
>
> 这段代码会在 3 秒后输出 `"3秒后执行的代码"`。
>
> ### 传递参数：
>
> 你可以在调用 `setTimeout` 时传递参数给延迟执行的函数：
>
> ```js
> function greet(name) {
>     console.log(`Hello, ${name}`);
> }
> 
> setTimeout(greet, 2000, "Peyton");
> // 2秒后输出: Hello, Peyton
> ```
>
> ### 使用 `clearTimeout()` 取消定时：
>
> 如果你想在定时器触发前取消它，可以使用 `clearTimeout()`：
>
> ```js
> let timerId = setTimeout(() => {
>     console.log("不会执行");
> }, 5000);
> 
> // 在定时器触发前清除
> clearTimeout(timerId);
> ```
>
> 这里 `clearTimeout(timerId)` 阻止了延迟执行的代码，所以 `"不会执行"` 不会被打印。
>
> ### 用途：
>
> 1. **延迟操作**：例如，延迟显示提示信息。
> 2. **轮询操作**：每隔一段时间进行一次数据检查或更新。
> 3. **防抖与节流**：与 `setTimeout` 配合使用，限制事件的频繁触发。
>
> `setTimeout` 提供了一种简单的方式来处理异步操作和延时执行。



## 总结

本节我们介绍了 DOM 和 BOM 的基本概念以及一些常见的操作。通过掌握 DOM 和 BOM，您将能够更有效地使用 JavaScript 进行 Web 开发，创建更丰富的用户界面和交互体验。

# 17. 事件

在 Web 开发中，事件是用户或浏览器自身执行的某种动作，例如点击按钮，提交表单，或者触发鼠标悬停效果等等。理解事件处理是创建交互式网站的关键。

这一讲所使用的 HTML 代码:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Event</title>
</head>
<body>
  <button>点击我！</button>

  <ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
  </ul>
  <script src="./Event.js"></script>
</body>
</html>
```



## 事件三要素

在JavaScript中，处理事件主要包含三个要素：事件源、事件类型和事件处理程序。

1. **事件源(Event Source)**: 事件源是指触发事件的对象，也就是用户进行交互的那个HTML元素，例如一个按钮、一个链接、一个文本框等。
2. **事件类型(Event Type)**: 事件类型表示事件的具体行为，如 click、mouseover、keydown 等。这些事件类型由浏览器预定义，我们只需要使用就行。
3. **事件处理程序(Event Handler)**: 事件处理程序是当事件被触发时，我们希望进行的操作，即用于响应某个事件的函数。这个函数会在事件发生时被调用。

这三个元素共同作用才能完成一个完整的事件处理。比如，当用户点击一个按钮（事件源）时（事件类型为点击事件），我们希望能弹出一个提示框（事件处理程序）。

以下是一个具体的示例：

```javascript
const btn = document.getElementById('myButton'); // 事件源

// 事件类型为 'click'
btn.onclick = function() {   // 事件处理程序
    alert('你点击了按钮!'); // 执行的操作
}; 
```



在这个示例中，按钮是事件源，点击按钮（'click'）是事件类型，弹出一个警告框是事件处理程序。

## 事件监听器

在 JavaScript 中，我们使用事件监听器（Event Listener）来处理这些事件。事件监听器是一个函数，它会在特定事件发生时被触发。我们使用 `addEventListener` 方法来指定事件监听器。以下是一个简单的点击事件监听器示例：

```javascript
const button = document.querySelector('button')
button.addEventListener('click', function () {
  alert('按钮被点击！')
})
```



在这个例子中，当用户点击按钮时，会弹出一个警告窗口。

## 事件对象

当事件被触发时，浏览器会创建一个事件对象，并将其作为参数传递给事件监听器。事件对象包含了关于事件的详细信息，例如鼠标的位置，或者用户按下的键等。例如：

```javascript
button.addEventListener('click', function (event) {
  console.log('事件类型：', event.type)
  console.log('目标元素：', event.target)
  console.log(`鼠标点击位置 (${event.clientX}, ${event.clientY})`)
})
```



在这个例子中，我们打印出了事件类型、目标元素和鼠标点击时的位置。

## 事件冒泡与捕获

在 DOM 树中，事件不仅仅会在它被触发的元素上进行处理，还会向上或向下传播到其他元素。这种现象称为事件冒泡（从内到外）和事件捕获（从外到内）。我们可以使用第三个参数来设置事件监听器是在冒泡阶段还是捕获阶段处理事件。

```javascript
// 在冒泡阶段处理事件
button.addEventListener(
  'click',
  function () {
    alert('按钮在冒泡阶段被点击！')
  },
  false
)

// 在捕获阶段处理事件
button.addEventListener(
  'click',
  function () {
    alert('按钮在捕获阶段被点击！')
  },
  true
)
```

> [!TIP]
>
> 在 JavaScript 中，事件处理有两个阶段：**捕获阶段**和**冒泡阶段**。这两个阶段解释了事件从最外层元素到目标元素（捕获阶段）以及从目标元素再返回最外层元素（冒泡阶段）的传播路径。
>
> ### 事件捕获和冒泡的概念：
> 1. **捕获阶段（Event Capturing）**：
>    - 事件从最外层（通常是 `document` 或 `window`）向内层传递，直到目标元素。
>    - 在捕获阶段，事件处理器有机会在事件到达目标元素之前捕获并处理该事件。
>
> 2. **冒泡阶段（Event Bubbling）**：
>    - 事件从目标元素向外层元素传递，直到最外层元素。
>    - 冒泡阶段是事件到达目标元素后，从目标元素逐层向外传递的过程。
>
> ### `addEventListener` 的第三个参数解释：
> - 当使用 `addEventListener` 监听事件时，第三个参数决定事件处理器在哪个阶段执行。
>   - `false`（默认）：事件处理器在冒泡阶段执行。
>   - `true`：事件处理器在捕获阶段执行。
>
> ### 代码解释：
> ```javascript
> // 在冒泡阶段处理事件
> button.addEventListener(
>   'click',
>   function () {
>     alert('按钮在冒泡阶段被点击！');
>   },
>   false // false 表示事件处理器在冒泡阶段执行
> );
> 
> // 在捕获阶段处理事件
> button.addEventListener(
>   'click',
>   function () {
>     alert('按钮在捕获阶段被点击！');
>   },
>   true // true 表示事件处理器在捕获阶段执行
> );
> ```
>
> ### 运行逻辑：
> - 当点击按钮时，两个事件处理器都会执行，但执行的顺序不同：
>   - **捕获阶段**的处理器会先执行，因为它在事件从外层元素向目标元素传递的过程中捕获了事件。
>   - **冒泡阶段**的处理器会在捕获阶段处理完成后执行，因为事件已经传递到目标元素并从内层向外传播。
>
> ### 运行效果：
> 1. **捕获阶段的处理器**会首先弹出 `"按钮在捕获阶段被点击！"`。
> 2. **冒泡阶段的处理器**会接着弹出 `"按钮在冒泡阶段被点击！"`。
>
> ### 总结：
> - `addEventListener` 的第三个参数决定事件处理器是在**捕获阶段**还是**冒泡阶段**处理事件。
> - 捕获阶段从外层元素向内传递，冒泡阶段从内层元素向外传递。



## 事件委托

由于事件的冒泡特性，我们可以将事件监听器添加到父元素，而不是直接添加到实际的目标元素。这种技术称为事件委托。这样可以减少事件监听器的数量，并且使得对动态添加的元素的处理变得更加容易。以下是一个事件委托的示例：

```javascript
const ul = document.querySelector('ul')
ul.addEventListener('click', function (event) {
  if (event.target.tagName.toLowerCase() === 'li') {
    alert(`第 ${event.target.textContent} 个 li 被点击了！`)
  }
})
```



在这个例子中，我们给 ul 元素添加了一个事件监听器，而不是给每个 li 元素单独添加。

> [!TIP]
>
> ### 事件委托的概念：
> **事件委托**是一种将事件监听器添加到父元素，而不是直接添加到目标元素的技术。这是通过利用事件冒泡机制来实现的。当目标元素触发事件时，事件会冒泡到父元素，父元素的事件处理器可以捕获到事件并做出响应。
>
> ### 为什么使用事件委托：
> 1. **减少事件监听器的数量**：不需要为每个子元素单独添加事件监听器，从而减少内存开销，提升性能。
> 2. **处理动态元素**：当子元素是动态添加到页面的（即在事件监听器绑定之后生成的元素），可以通过事件委托来确保这些新元素的事件也能被捕捉到。
>
> ### 代码解析：
> ```javascript
> const ul = document.querySelector('ul');
> 
> ul.addEventListener('click', function (event) {
>   // 检查点击的目标是否是 li 元素
>   if (event.target.tagName.toLowerCase() === 'li') {
>     alert(`第 ${event.target.textContent} 个 li 被点击了！`);
>   }
> });
> ```
>
> ### 代码运行逻辑：
> 1. **父元素 `ul` 绑定了 `click` 事件监听器**，而没有给每个 `li` 元素单独绑定事件。
> 2. 当点击 `ul` 内的任何 `li` 元素时，事件会冒泡到 `ul`，触发 `ul` 的 `click` 事件处理器。
> 3. **`event.target`** 是点击的具体目标元素，`event.target.tagName` 用于获取目标元素的标签名。
> 4. 判断 `event.target.tagName` 是否为 `li`，确保只有点击 `li` 元素时才会触发 `alert`。
> 5. `alert` 中通过 `event.target.textContent` 获取点击的 `li` 元素的文本内容，输出提示信息。
>
> ### 优点：
> - **减少代码重复**：你只需在父元素（`ul`）上绑定一个事件处理器，而不是为每个 `li` 绑定。
> - **处理动态子元素**：如果以后动态添加了新的 `li` 元素，仍然能够响应点击事件，因为事件委托是基于父元素的。
>
> ### 示例解释：
> 如果点击第一个 `li` 元素，假设其文本是 `1`，那么会弹出提示框显示：
> ```
> 第 1 个 li 被点击了！
> ```
>
> ### 适用场景：
> - **列表或表格中的行点击事件**：你可以在 `ul`、`table` 等父级元素上使用事件委托，处理子级元素的点击事件。
> - **动态添加的元素**：事件委托适合处理那些在事件绑定之后动态添加到页面的元素，比如通过 JavaScript 添加的 `li` 项。



## 自定义事件

除了浏览器自带的事件，我们还可以创建自定义事件。自定义事件可以用来在不同的组件之间进行通信。以下是一个自定义事件的示例：

```javascript
const customEvent = new CustomEvent('myEvent', {
  detail: { message: '这是一个自定义事件' },
})

document.addEventListener('myEvent', (event) => {
  console.log('自定义事件被触发了：', event.detail.message)
})

document.dispatchEvent(customEvent) // 触发事件
```

> [!IMPORTANT]
>
> 这段代码展示了如何在 JavaScript 中创建、监听和触发自定义事件。
>
> ### 代码解析：
>
> 1. **创建自定义事件**：
>    
>    ```javascript
>    const customEvent = new CustomEvent('myEvent', {
>      detail: { message: '这是一个自定义事件' },
>    });
>    ```
>    - 通过 `new CustomEvent` 方法，我们创建了一个名为 `'myEvent'` 的自定义事件。
>    - `detail` 属性可以包含一些额外的数据，在这里我们传递了一个对象 `{ message: '这是一个自定义事件' }`，这个对象将作为事件的详细信息随事件一起传递。
>    
> 2. **监听自定义事件**：
>    ```javascript
>    document.addEventListener('myEvent', (event) => {
>      console.log('自定义事件被触发了：', event.detail.message);
>    });
>    ```
>    - 我们使用 `addEventListener` 监听名为 `'myEvent'` 的事件。
>    - 当该事件被触发时，传入的回调函数会执行。
>    - `event.detail` 是包含我们在事件创建时传递的额外数据，`event.detail.message` 即 `'这是一个自定义事件'`。
>
> 3. **触发自定义事件**：
>    ```javascript
>    document.dispatchEvent(customEvent); // 触发事件
>    ```
>    - 使用 `dispatchEvent` 方法在 `document` 对象上触发了我们创建的 `customEvent` 自定义事件。
>    - 触发事件后，之前绑定的监听器会接收到事件，并执行回调函数。
>
> ### 输出：
> 当自定义事件 `myEvent` 被触发时，控制台会输出：
> ```
> 自定义事件被触发了： 这是一个自定义事件
> ```
>
> ### 自定义事件的应用场景：
> - **模块通信**：不同模块之间可以通过触发自定义事件来进行通信。
> - **页面交互**：某些交互场景可能并不依赖于 DOM 本身变化，而是业务逻辑的变动，此时自定义事件可以发挥作用。
> - **解耦事件逻辑**：你可以让某个模块触发事件，而不用关心哪个模块会监听它，事件监听和触发相互独立，降低耦合度。

在这个例子中，我们创建了一个名为 myEvent 的自定义事件，并在 document 上触发了这个事件。然后我们在 document 上添加了一个事件监听器，当 myEvent 事件被触发时，会打印出事件的详细信息。

## 总结

本节介绍了 JavaScript 事件的基本概念，包括事件监听器、事件对象、事件冒泡与捕获、事件委托和自定义事件。通过了解这些概念，您可以利用 JavaScript 事件来增强网页交互。

# 8. 异常处理

在 JavaScript 编程中，错误处理和调试是必备的技能。无论你的代码编写得多么完美，错误总是难以避免的。JavaScript 提供了一套完善的错误处理机制，我们可以通过它来处理运行时的错误。在这一章节中，我们将介绍JavaScript 中的错误处理机制，以及如何使用浏览器的开发者工具调试程序。

## JavaScript 错误对象

JavaScript 有一种特殊的对象类型，名为 `Error`，它用于表示在程序执行过程中发生的错误。当 JavaScript 引擎遇到错误时，会抛出一个 `Error` 对象。

`Error` 对象包含两个主要的属性：`name` 和 `message`。`name` 属性表示错误的名称，`message` 属性则包含了错误的详细信息。

创建 `Error` 对象的语法如下：

```javascript
let error = new Error("This is an error message");
console.log(error.name); // "Error"
console.log(error.message); // "This is an error message"
```



## 抛出错误

在 JavaScript 中，我们可以使用 `throw` 关键字来手动抛出一个错误。当我们抛出一个错误时，程序的执行会立即停止，JavaScript 引擎会寻找处理这个错误的代码。如果没有找到任何错误处理代码，程序就会完全停止执行。

```javascript
throw new Error("This is an error message");
console.log("This will not be logged"); // 该行代码不会被执行
```



## 捕获错误

JavaScript 提供了 `try...catch` 语句来捕获和处理错误。在 `try` 块中的代码发生错误时，控制流会立即跳到对应的 `catch` 块。

```javascript
try {
  // 可能会抛出错误的代码
  const a = 1
  a() // 这里会抛出一个 TypeError
} catch (error) {
  // 处理错误
  console.log(error.message) // 输出 'a is not a function'
}
```



在这个例子中，我们在 `try` 块中抛出了一个错误，然后在 `catch` 块中捕获并处理了这个错误。

## finally 语句

`try...catch` 结构还可以包含一个 `finally` 块。无论 `try` 块中的代码是否抛出错误，`finally` 块中的代码总是会被执行。

```javascript
try {
  // 可能会抛出错误的代码
  const a = 1
  a() // 这里会抛出一个 TypeError
} catch (error) {
  // 处理错误
  console.log(error.message) // 输出 'a is not a function'
} finally {
  // 无论是否抛出错误，这里都会被执行
  console.log('执行完毕')
}
```



在上面的例子中，无论 `try` 块中的代码是否抛出错误，`finally` 块中的代码总是会被执行。

## 调试：浏览器的开发者工具

大部分的浏览器都有内置的开发者工具，你可以使用它们来调试你的 JavaScript 代码。开发者工具提供了许多强大的功能，包括断点、单步执行、查看变量值等等。

你可以通过以下步骤来打开开发者工具：

### 快捷键

`F12` （笔记本用户使用 `Fn+F12`）

### 手动打开

1. 打开浏览器。
2. 右键点击网页，选择 “检查” 或 “审查元素”。
3. 切换到 “Console” 或 “Sources” 标签。

在开发者工具中，你可以查看到所有的 JavaScript 错误，包括错误的类型、错误的信息，以及错误发生的位置。



![img](https://www.wtf.academy/assets/images/18-1-f6b8d966cf17dd91e4a9f75dbd705146.png)



你还可以在代码中的任何位置设置断点。当代码执行到断点的时候，它将会暂停，你可以查看变量的值，或者单步执行代码。

## 总结

在本教程中，我们详细介绍了 JavaScript 中的错误处理机制，包括如何创建和抛出错误，以及如何捕获和处理错误。当我们编写 JavaScript 代码时，应该时刻考虑错误处理，并编写适当的代码来处理可能出的错误。另外，我们还可以借助浏览器的开发者工具来调试我们的代码。

# 19. 单元测试

所有人都会写出有 bug 的代码，如何测试你写的程序是否能正常运行就非常重要了。在 JavaScript 中，有多种测试框架可以帮助你进行单元测试（Unit Test），其中包括 Jest, Mocha 和 Chai。在这一章中，我们将介绍如何使用这些工具进行单元测试。

## 什么是单元测试

单元测试（Unit Testing）是软件测试的一种方法，它的基本原理是将程序分解成独立的可测试的模块（或者称为“单元”），然后对这些模块进行单独和独立的测试。这些模块一般是函数、方法、类、模块等代码组织单元。

在 JavaScript 中，单元测试通常涉及到对单个函数或对象方法的测试，以验证其是否正常工作。这些测试一般会检查函数的返回值、副作用、错误抛出等情况，以确保函数的行为符合预期。

## 为什么需要单元测试

单元测试有许多优点，以下是其中的一些：

1. **确保代码质量**：单元测试可以帮助我们发现代码的缺陷和问题，从而提高代码的质量。对每个模块进行详细的测试可以确保每个组件都按照预期工作。
2. **简化重构**：当我们需要修改或重构代码时，如果有一套完整的单元测试，就可以迅速检查修改后的代码是否仍然符合预期，这大大降低了重构的风险。
3. **提升开发速度**：虽然编写单元测试需要时间，但长期来看，它可以帮助我们更快地开发和维护代码。有了单元测试，我们可以更有信心地进行修改和优化，而不必担心无意中破坏了现有的功能。
4. **文档化代码**：良好的单元测试可以作为一种形式的文档，显示函数或方法应该如何使用，以及在给定输入时应该返回什么。

单元测试是一种预防性的工作，它能够提前发现并修复问题，从而防止问题在产品中出现，对于任何想要保证代码质量的项目来说，都是必不可少的一环。

## Jest

Jest 是由 Facebook 开发的一个 JavaScript 测试框架，它提供了包括断言、模拟和覆盖率信息等在内的一整套测试功能。

要使用 Jest，首先你需要通过 yarn 或 npm 安装它：

```shell
yarn add --dev jest
## 或者
npm install --save-dev jest
```



然后我们写一个求和函数，保存为 `sum.js` 用来测试：

```javascript
function sum(a, b) {
    return a + b;
  }

module.exports = sum;
```



在测试代码中，引入想要测试的 `sum` 函数，然后定义一个测试案例来描述测试的情况。`expect` 函数用于对结果进行断言，`toBe` 是一个比较函数，用于比较 `expect` 的参数和 `toBe` 的参数是否相等。将测试代码保存为 `sum.test.js`

```javascript
const sum = require('./sum');

test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
});
```



接下来，我们要修改 `package.json` 文件，加上下面这项：

```json
{
  "scripts": {
    "test": "jest"
  }
}
```



添加完后，你的 `package.json` 可能长这样:

```json
{
    "name": "wtf-javascript",
    "version": "1.0.0",
    "type": "module",
    "scripts": {
        "test": "jest"
    },
    "dependencies": {
        "jest": "^29.5.0"
    }
}
```



最后，你可以在命令行运行 `yarn test` 或 `npm test` 开始测试，你会看到测试通过的信息:

```shell
> wtf-javascript@1.0.0 test
> jest

 PASS  19_UnitTest/sum.test.js
  ✓ adds 1 + 2 to equal 3 (2 ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        0.366 s, estimated 1 s
```



注意，Jest 仅支持 `CommonJS` 语法，默认不支持 `ES` 的语法，包括 `import` 和 `export`。

## Mocha

Mocha 是另一种流行的 JavaScript 测试框架，它的主要特点是灵活性高，可以和多种断言库（如 Chai）和模拟工具一起使用。

首先，你需要安装 `mocha` 包:

```shell
npm install mocha
```



在根目录下创建一个 `test` 文件夹，将下面代码保存到 `mocha_test.js` 文件中：

```javascript
import assert from 'assert';

function sum(a, b) {
  return a + b;
}

describe('sum', () => {
    it('adds 1 + 2 to equal 3', () => {
      assert(sum(1, 2) === 3);
    });
  });
```



在这个例子中，我们使用 `describe` 来分组相关的测试案例，`it` 则用来定义一个具体的测试案例。断言是通过 Node.js 的内置 `assert` 模块进行的。

接下来，我们要修改 `package.json` 文件，加上下面这项：

```json
{
  "scripts": {
    "test": "mocha"
  }
}
```



然后运行 `npm test` 进行测试：

```shell
> wtf-javascript@1.0.0 test
> mocha



  sum
    ✔ adds 1 + 2 to equal 3


  1 passing (4ms)
```



## Chai

[Chai](https://www.chaijs.com/) 是一个流行的断言库，它可以配合任何 JavaScript 测试框架使用。Chai 提供了一系列的断言方法，让你的测试代码更加语义化和易读。你可以使用 npm 安装 Chai：

```bash
npm install chai
```



Chai 提供了三种断言风格：Should、Expect 和 Assert。下面我们分别介绍他们。

### Should

Should 风格将断言函数绑定到被测试对象的原型上。因此，你可以在任何对象上调用 should 方法。以下是一个例子：

```javascript
const chai = require('chai');
const should = chai.should();

(5).should.be.a('number');
```



### Expect

Expect 风格提供了一种更传统的、功能更强大的方式来编写断言。它允许更具描述性的断言，以及更深层次的比较。以下是一个例子：

```javascript
const chai = require('chai');
const expect = chai.expect;

expect(5).to.be.a('number');
```



### Assert

Assert 风格是对 Node.js 的内置 assert 模块的扩展。这种风格的断言更符合传统的编程观念，非常适合那些喜欢使用类似于 Node.js 的 assert 函数的开发者。以下是一个例子：

```javascript
const chai = require('chai');
const assert = chai.assert;

assert.typeOf(5, 'number');  // 直接通过静态方法调用断言

```

> [!IMPORTANT]
>
> - **Should 风格**: 偏向自然语言风格，适合喜欢链式、描述性断言的开发者，但有可能修改对象的原型。
> - **Expect 风格**: 提供灵活性和链式调用，适合需要复杂断言的场景，不修改原型链，是更现代的风格。
> - **Assert 风格**: 类似传统的断言语法，适合简单断言和习惯 Node.js 原生 `assert` 的开发者。



## 总结

这一讲，我们介绍了 JavaScript 中的单元测试，它可以帮助你保证代码的质量和稳定性。Jest, Mocha 和 Chai 是 JavaScript 开发者常用的一些测试工具，可以帮助你更方便地编写和管理测试案例。

# 20. ES6

ES6（也被称为 ECMAScript 2015）是 JavaScript 语言的一个重要的更新，引入了许多新的特性和语法，使得 JavaScript 更加强大和灵活。在这一章中，我们将介绍一些 ES6 的主要特性。

## let 和 const

在 ES6 之前，JavaScript 中只有 `var` 用来声明变量，但它的作用域规则经常会引发一些混淆。ES6 引入了 `let` 和 `const` 两种新的声明方式，使得变量的作用域更加清晰。

- `let`：用来声明一个块级作用域的变量。
- `const`：用来声明一个块级作用域的常量，这个常量的值不能被重新赋值。

```javascript
let x = 10;
if (true) {
  let x = 20;  // 这个 x 是一个新的变量
  console.log(x);  // 输出 20
}
console.log(x);  // 输出 10

const y = 30;
y = 40;  // 报错，y 的值不能被改变
```



## 箭头函数

箭头函数是一种新的函数语法，它更简洁，而且不绑定 `this`。

```javascript
const arr = [1, 2, 3, 4];
const squares = arr.map(x => x * x);
console.log(squares);  // 输出 [1, 4, 9, 16]
```



## 模板字符串

模板字符串提供了一种方便的方式来嵌入变量或表达式到字符串中。

```javascript
let name = 'Alice';
console.log(`Hello, ${name}!`);  // 输出 "Hello, Alice!"
```



## 扩展运算符

ES6中可以通过三个点（...）将一个可迭代对象（如数组或字符串）展开，将其元素或字符序列分别提取出来，用于函数调用、数组字面量等场景。

```javascript
function addNumbers(x, y, z) {
  return x + y + z;
}

const numbers = [1, 2, 3];

// 使用扩展运算符将数组中的元素展开作为函数的参数
const result = addNumbers(...numbers);

console.log(result); // 输出: 6
```



## 解构赋值

解构赋值允许我们将数组或对象的属性赋值给单独的变量。

```javascript
let [a, b, c] = [1, 2, 3];
console.log(a, b, c);  // 输出 1 2 3

let {x, y} = {x: 10, y: 20};
console.log(x, y);  // 输出 10 20
```



## Promises 和异步函数

ES6 引入了 Promises，它提供了一种更好的方式来处理异步操作。此外，ES6 也引入了 async/await 语法，使得异步代码更像同步代码。

```javascript
// 使用Promise封装一个异步操作
function fetchUser() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const user = { id: 1, name: 'John' };
      resolve(user);
    }, 2000);
  });
}

// 使用async/await来处理异步任务
async function getUser() {
  try {
    const user = await fetchUser();
    console.log('User:', user);
  } catch (error) {
    console.log('Error:', error);
  }
}

// 调用异步函数
getUser();//2s后输出 User: {id: 1, name: 'John'}
```



## 总结

以上只是 ES6 的一部分特性。ES6 还引入了许多其他新特性，如类（class），模块（module），生成器（generator），迭代器（iterator），Symbol 类型，新的数据结构如 Map 和 Set，以及许多新的数组和对象的方法。

ES6 的所有这些特性都使 JavaScript 成为一个更强大，更现代化的编程语言。

#  21. Promise

JavaScript 是一种异步编程语言，这意味着它可以在等待某个操作（如网络请求）完成的同时，执行其他任务。在第10讲，我们介绍了异步编程和 `async/await`语法糖，这一讲，我们介绍 Promise（承诺）。

## 什么是 Promise？

Promise 是一种在 JavaScript 中处理异步操作的方法，让异步代码更易于理解和管理。它代表一个未来可能会得到的结果的对象，可能是一个成功的值，或者一个发生的错误。Promise 在它们被解析（resolve，代表成功）或拒绝（reject，代表失败）之前，处于待定（pending）状态。

以下是 Promise 的三种状态：

- **待定（Pending）**：初始状态，既不是成功，也不是失败。
- **已实现（Fulfilled）**：操作成功完成。
- **已拒绝（Rejected）**：操作失败。

Promise 是一次性的 —— 它们只能从待定状态转移到实现或拒绝状态，一旦改变，状态就无法再次改变。这意味着，如果一个 Promise 被解析，你就不能再次解析或拒绝它，反之亦然。



![img](https://www.wtf.academy/assets/images/21-1-885f869ae05fc3b57eaaea6eefeb9925.jpeg)



- JavaScript程序: 我知道你现在还没准备好（Pending），但你能不能给我一个承诺（Promise）？
- 0xAA: 好的，我给你一个承诺（Promise），等我准备好的时候，我会调用你的 `resolve` 回调函数；但是如果准备失败，我会调用你的 `reject` 回调函数，并告诉你失败的原因。

## 创建 Promise

在 JavaScript 中，你可以使用 `new Promise` 构造函数创建一个新的 Promise，该构造函数接收一个函数作为参数，这个函数又接收两个参数：一个 `resolve` 函数和一个 `reject` 函数，分别用于改变 Promise 的状态为 Fulfilled 或 Rejected。

```javascript
const promise = new Promise((resolve, reject) => {
  // 异步操作代码
});
```



在执行器函数内部，我们通常会进行一些异步操作，例如读取文件、发起网络请求等。当异步操作成功完成，我们调用 `resolve` 函数并传入结果值，当操作失败时，我们调用 `reject` 函数并传入错误。

例如，以下是一个简单的 Promise，它使用 `setTimeout` 来模拟异步操作：

```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('WTF Promise resolved');
  }, 1000);
});

// 1秒后输出 'WTF Promise resolved'
promise.then(value => console.log(value));
```

> [!TIP]
>
> 这段代码使用了 JavaScript 的 `Promise` 对象来处理异步操作。它展示了如何创建一个 `Promise` 实例，并在 1 秒后通过 `resolve` 函数完成这个 `Promise`，然后通过 `then` 方法处理返回的值。
>
> ### 代码解析：
>
> 1. **创建 `Promise`**:
>    ```javascript
>    const promise = new Promise((resolve, reject) => {
>      setTimeout(() => {
>        resolve('WTF Promise resolved');
>      }, 1000);
>    });
>    ```
>    - 这里通过 `new Promise` 创建了一个 `Promise` 对象。
>    - `Promise` 接受一个执行函数作为参数，执行函数包含两个参数：`resolve` 和 `reject`，它们分别用于表示异步操作成功或失败。
>    - 在这段代码中，`setTimeout` 被用于模拟异步操作，1 秒后调用 `resolve('WTF Promise resolved')`，表示异步操作成功，并传递结果 `'WTF Promise resolved'`。
>
> 2. **处理 `Promise` 的结果**:
>    ```javascript
>    promise.then(value => console.log(value));
>    ```
>    - 使用 `promise.then()` 方法来处理异步操作完成后的结果。
>    - 当 `Promise` 被 `resolve` 时，它会返回我们传递的值 `'WTF Promise resolved'`，然后 `then` 方法中的回调函数会被执行，并打印该值到控制台。
>
> ### 输出：
> 在 1 秒后，控制台会输出：
> ```
> WTF Promise resolved
> ```
>

在上述代码中，我们创建了一个新的 Promise，它将在 1 秒后被解析，并返回字符串 `'Promise resolved'`。我们使用 `.then` 方法注册了一个回调函数，当 Promise 解析时，该函数将被调用并接收解析的值。

## 使用 Promise

Promise 的优势在于你可以使用链式 `.then` 调用来组织和管理你的异步代码。`.then` 方法接受两个可选参数：一个用于处理解析值的回调函数，和一个用于处理拒绝原因（即错误）的回调函数。

```js
promise.then(
  value => {
    // 处理解析后的值
  },
  error => {
    // 处理错误
  }
);
```



`.then` 方法返回一个新的 Promise，这使得你可以将多个 `.then` 调用链接在一起。

```javascript
promise
  .then(value => {
    console.log(value);
    return value + ' WTF';
  })
  .then(newValue => console.log(newValue));
```

> [!TIP]
>
> 这段代码展示了如何通过 `Promise` 的链式调用来处理异步操作的多个步骤。每个 `then` 方法可以在上一个异步操作成功后，接收其结果，并返回一个新的值供下一个 `then` 使用。
>
> ### 代码解析：
>
> 1. **第一步: 初始 `Promise`**:
>    ```javascript
>    promise
>      .then(value => {
>        console.log(value);
>        return value + ' WTF';
>      })
>    ```
>    - 这是第一个 `then` 方法，用来处理 `promise` 完成后的结果。
>    - `then` 的回调函数接受 `resolve` 的值，即 `value`，并打印出来。
>    - 回调函数还返回一个新的字符串 `value + ' WTF'`，这个返回值会被传递给下一个 `then`。
>
> 2. **第二步: 处理第一个 `then` 的返回值**:
>    ```javascript
>    .then(newValue => console.log(newValue));
>    ```
>    - 在第二个 `then` 中，回调函数接收上一个 `then` 返回的新值，即 `value + ' WTF'`。
>    - 这个 `newValue` 会被打印到控制台。
>
> ### 示例代码：
>
> 假设 `promise` 是如下定义的：
>
> ```javascript
> const promise = new Promise((resolve, reject) => {
>   setTimeout(() => {
>     resolve('WTF Promise resolved');
>   }, 1000);
> });
> ```
>
> ### 预期输出：
>
> 1. 在第一个 `then` 中，输出 `WTF Promise resolved`。
> 2. 在第二个 `then` 中，输出 `WTF Promise resolved WTF`。
>
> 完整的输出如下：
> ```
> WTF Promise resolved
> WTF Promise resolved WTF
> ```
>
> ### 总结：
> - 每个 `then` 可以接受上一个 `then` 返回的结果，并继续处理新的逻辑。
> - 这实现了一个清晰的、链式的异步操作流程。

`.catch` 方法可以用来捕获错误。它和 `.then` 方法类似，都返回一个新的 Promise。你可以将它们链接在一起，如果其中一个 Promise 被拒绝，`catch` 会处理它：

```js
promise
  .then(value => {
    throw new Error('WTF Something went wrong');
  })
  .catch(error => console.error(error));
```



在这个例子中，我们首先在 `then` 方法中处理解析值，然后在 `catch` 方法中处理错误。这是一种常见的错误处理模式。

`finally` 方法不管 `Promise` 对象最后状态如何，都会被执行。`finally` 方法的回调函数不接受任何参数，这意味着没有办法知道，前面的 `Promise` 状态到底是 `resolved` 还是 `rejected`。这表明，`finally` 方法里面的操作，应该是与状态无关的，不依赖于 `Promise` 的执行结果。

```js
const p = new Promise((resolve, reject) => {
  resolve('Hello, WTF JavaScript!')
})

p.then((value) => {
  console.log(value)
}).finally(() => {
  console.log('finally')
})

// Hello, WTF JavaScript!
// finally
```

> [!TIP]
>
> 这段代码展示了 `Promise` 的基本用法，以及如何使用 `finally` 方法来在 `Promise` 完成后执行清理代码或其他操作。
>
> ### 代码解析：
>
> 1. **创建 Promise**:
>    ```javascript
>    const p = new Promise((resolve, reject) => {
>      resolve('Hello, WTF JavaScript!');
>    });
>    ```
>    - 创建一个新的 `Promise` 实例 `p`。
>    - 在这个 `Promise` 的执行函数中，直接调用 `resolve`，并传入字符串 `'Hello, WTF JavaScript!'`。这意味着这个 `Promise` 将在异步操作完成后进入“解决”状态。
>
> 2. **处理 Promise 结果**:
>    ```javascript
>    p.then((value) => {
>      console.log(value);
>    })
>    ```
>    - 使用 `then` 方法来处理 `Promise` 成功的结果。
>    - 回调函数的参数 `value` 接收 `resolve` 时传入的值，因此这里会输出 `Hello, WTF JavaScript!`。
>
> 3. **使用 finally 方法**:
>    ```javascript
>    .finally(() => {
>      console.log('finally');
>    });
>    ```
>    - `finally` 方法不论 `Promise` 是被 `resolve` 还是 `reject`，都会执行。
>    - 在这里，它将打印 `'finally'`，这表示无论 `Promise` 的最终状态如何，都会执行这段代码。
>
> ### 预期输出：
> 执行该代码后，控制台将输出：
>
> ```
> Hello, WTF JavaScript!
> finally
> ```
>
> ### 总结：
> - `Promise` 的 `then` 方法用于处理成功的结果。
> - `finally` 方法用于在 `Promise` 完成时执行清理代码，这使得可以在 `Promise` 被解决或拒绝时执行相同的逻辑。



## Promise API

Promise API 提供了一些用于处理 Promise 的便捷方法：

- `Promise.resolve(value)`：返回一个以给定值解析后的 Promise。如果该值是一个 Promise，返回的 Promise 将具有相同的状态和值。
- `Promise.reject(reason)`：返回一个用给定的原因拒绝的 Promise。
- `Promise.all(iterable)`：返回一个新的 Promise，它在 iterable 中的所有 Promise 都解析后解析，或者在 iterable 中的任何 Promise 被拒绝后拒绝。

> [!NOTE]
>
> `Promise.all(iterable)`并行执行所有 Promise，当所有 Promise 都解析成功时，`Promise.all` 返回一个新的 Promise，并将所有 Promise 的结果作为数组传递给 `then` 处理。如果其中任何一个 Promise 失败，`Promise.all` 会直接进入 `catch`，并返回第一个被拒绝的 Promise 的错误信息。

- `Promise.race(iterable)`：返回一个新的 Promise，它在 iterable 中的任何 Promise 解析或拒绝后具有相同的解析值或拒绝原因。

> [!NOTE]
>
> **`Promise.race`**：并行执行所有 Promise，并返回第一个完成的 Promise，无论是成功还是失败。

- `Promise.allSettled(iterable)`: 有时我们希望等到一组异步操作都结束了，不管每一个操作是成功还是失败，再进行下一步操作。但是，`Promise.all` 方法只适合所有异步操作都成功的情况，如果有一个操作失败，就无法满足要求。这时我们需要使用 `Promise.allSettled` 方法。
- `Promise.any`: 与 `Promise.race` 类似，区别在于只要有一个 `Promise` 实例变成 `fulfilled` 状态，包装实例就会变成 `fulfilled` 状态；所有 `Promise` 实例都变成 `rejected` 状态，包装实例才会变成 `rejected` 状态。

## 高级 Promise 模式

在处理复杂的异步操作时，我们可能需要使用一些更高级的 Promise 模式。

- **链式 Promise**：`then` 和 `catch` 方法都会返回新的 Promise，这使我们可以创建一个 Promise 链，依次处理多个异步操作。

```javascript
fetch('https://api.example.com/data') // 返回一个 Promise
  .then(response => response.json()) // 返回一个新的 Promise
  .then(data => console.log(data)) // 返回一个新的 Promise
  .catch(error => console.error(error)); // 返回一个新的 Promise
```

> [!TIP]
>
> #### **步骤解读**：
>
> 1. `fetch('https://api.example.com/data')`：
>    - `fetch` 函数发起一个网络请求，返回一个 Promise，该 Promise 代表网络请求的异步操作。
>    - 当请求成功时，Promise 进入 "resolved" 状态，触发后续的 `then` 操作。
> 2. `.then(response => response.json())`：
>    - 一旦 `fetch` 请求成功，我们使用 `then` 方法处理响应。这里 `response.json()` 是异步的，它会将服务器的响应解析为 JSON 格式，返回一个新的 Promise。
>    - 该 Promise 的结果是解析后的 JSON 数据。
> 3. `.then(data => console.log(data))`：
>    - 在上一个 `then` 中返回的 Promise 解析成功后，这里的 `then` 方法会处理解析后的数据，并将其打印到控制台。
> 4. `.catch(error => console.error(error))`：
>    - 如果 Promise 链中的任何一步出错，例如网络请求失败或者 JSON 解析失败，这个 `catch` 方法会捕获错误并输出错误信息。



- **并行 Promise**：使用 `Promise.all` 或 `Promise.race` 方法，我们可以并行执行多个 Promise，并按照它们的解析顺序或速度来解析最终的 Promise。

```javascript
Promise.all([
  fetch('https://api.example.com/data1'),
  fetch('https://api.example.com/data2')
])
  .then(([response1, response2]) => Promise.all([response1.json(), response2.json()]))
  .then(([data1, data2]) => {
    console.log('Data 1:', data1);
    console.log('Data 2:', data2);
  })
  .catch(error => console.error(error));
```

> [!NOTE]
>
> ### **步骤解析**：
>
> 1. **`Promise.all`**：
>    - 将两个 `fetch` 请求传入 `Promise.all` 数组中，并行发起这两个网络请求。
>    - `Promise.all` 会等待两个请求都成功完成，之后才会进入下一步的 `then`。
> 2. **第一个 `then`**：
>    - 当两个请求都成功后，`response1` 和 `response2` 是两个 `Response` 对象。我们将这两个响应通过 `Promise.all` 再次并行处理，使用 `response.json()` 将它们的结果解析为 JSON。
> 3. **第二个 `then`**：
>    - 在解析完成后，`data1` 和 `data2` 是解析后的 JSON 数据。我们将这些数据分别输出到控制台。
> 4. **`catch`**：
>    - 如果在任意一个 `fetch` 请求或 JSON 解析过程中出现错误，`catch` 将会捕获并输出错误信息。

在这个例子中，我们并行获取两个 API 的数据，然后同时处理两个响应。

## 总结

这一讲，我们介绍了 JavaScript 中的一个重要概念，Promise，方便我们处理异步操作。通过深入理解和使用 Promise，你可以写出更干净、更容易维护的异步代码。

# 22. 网络请求

在这一章节，我们将讨论如何使用 JavaScript 发送网络请求。重点关注 GET 和 POST 请求，并介绍如何使用 AJAX，Fetch API 和 axios 发送这些请求。

## GET 请求

GET 请求是最常见的 HTTP 请求类型，通常用于获取服务器上的数据。

在 JavaScript 中，可以使用 `fetch` 函数发送 GET 请求，如下例所示：

```javascript
fetch('https://api.github.com/search/users?q=amazingang', {
  method: 'GET',
})
.then(response => response.json())
.then(data => console.log(data))
.catch((error) => console.error('Error:', error));
```



在上述代码中，我们使用 `fetch` 函数向 URL `https://api.github.com/search/users?q=amazingang` 发送了一个 GET 请求。然后，我们使用 `.then` 来处理返回的响应并将其转换为 JSON 格式。最后，我们打印出返回的数据或捕获并打印出任何错误。

## POST 请求

POST 请求用于向服务器发送数据。这种请求类型通常用于提交表单。

发送 POST 请求与发送 GET 请求类似，但是需要在 `fetch` 函数的第二个参数中提供一些额外的选项。具体来说，我们需要设置 `method` 为 `'POST'`，并提供一个 `body`，该 `body` 包含我们要发送的数据。

以下是一个示例：

```javascript
fetch('https://api.example.com/data', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    username: '0xAA',
    password: 'pwd',
  }),
})
.then(response => response.json())
.then(data => console.log(data))
.catch((error) => console.error('Request failure:', error));
```



在上述代码中，我们向同样的 URL 发送了一个 POST 请求，但是这次我们包含了一个请求体，该请求体包含 `username` 和 `password` 两个字段的 JSON 数据。请注意，我们也设置了 `Content-Type` 头部为 `application/json`，以告诉服务器我们正在发送 JSON 数据。

## AJAX

AJAX（Asynchronous JavaScript and XML）是一种在无需刷新整个页面的情况下，与服务器交换数据并更新部分网页的技术。AJAX 不是一种新的编程语法，而是使用已有的标准，如 XMLHttpRequest 对象，组合在一起的一种新方式。

以下是一个 AJAX 的例子：

```javascript
// 创建 XMLHttpRequest 对象
let xhr = new XMLHttpRequest();

// 指定请求的方法和 URL
xhr.open("GET", 'https://api.github.com/search/users?q=amazingang', true);

// 设置回调函数，处理请求的响应
xhr.onreadystatechange = function () {
  // 请求成功
  if (xhr.readyState == 4 && xhr.status == 200)
    // 处理响应数据
    console.log(JSON.parse(xhr.responseText));
}
// 发送请求
xhr.send();
```



在浏览器的console中执行以上代码，会打印出名字中包含`amazingang`的github用户



![ajax](https://www.wtf.academy/assets/images/22-1-53a05f426a592a2fd9bdca11a9d25529.png)



## Fetch API

Fetch API 提供了一种简单、合理的方式来跨网络异步获取资源。它比旧的 XMLHttpRequest 接口更加强大和灵活。Fetch API 返回一个 Promise 对象，表示一个异步操作的最终完成（或失败）及其结果的值。

以下是一个 Fetch API 的例子：

```javascript
fetch('https://api.github.com/search/users?q=amazingang')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

> [!TIP]
>
> ### Fetch API 的工作机制：
>
> 1. **发起请求**： `fetch` 函数会发出一个 HTTP 请求。你可以指定请求的方法（`GET`、`POST`等），但如果没有明确指定，默认使用 `GET`。
> 2. **返回 Promise**： `fetch` 返回的 `Promise` 表示请求操作的结果。如果请求成功完成，Promise 会被解决，并返回一个 `Response` 对象。你可以通过 `then()` 方法处理该 `Response`。
> 3. **处理响应**： 使用 `response.json()` 可以将返回的 JSON 格式的数据转换为 JavaScript 对象。这个过程也是异步的，因此需要通过 `then()` 进一步处理。
> 4. **错误处理**： 如果请求发生错误，比如网络问题，`fetch` 的 Promise 会被拒绝，可以通过 `catch()` 捕获并处理这些错误。



![fetch](https://www.wtf.academy/assets/images/22-2-702b62644adeb924363b9a5df89d1f68.png)



## Axios

Axios 是一个基于 Promise 的 HTTP 库，可以用在浏览器和 node.js 中。Axios 的主要特点包括：可以拦截请求和响应，转换请求和响应数据，取消请求，自动转换 JSON 数据，客户端支持防御 XSRF 等。

> [!TIP]
>
> **拦截请求和响应**：Axios 可以在请求发送前和响应接收后拦截并处理数据，这可以用于例如自动添加认证令牌、处理错误或者记录日志等操作。
>
> **请求和响应数据转换**：在请求发送和响应接收时，Axios 可以自动将数据转换为合适的格式，例如自动转换 JavaScript 对象为 JSON 字符串或将返回的 JSON 自动解析为 JavaScript 对象。
>
> **取消请求**：Axios 提供了取消请求的功能，适合在需要终止长时间运行的请求时使用。
>
> **自动处理 JSON 数据**：Axios 会自动将请求中的 JavaScript 对象转换为 JSON 格式，同时将响应的 JSON 数据自动解析为对象，因此不用手动调用 `.json()`。
>
> **XSRF 防御**：在客户端，Axios 允许配置 XSRF 防御，增强安全性，防止跨站点请求伪造攻击。

以下是一个 axios 的例子：

```javascript
// 导入 axios 库
const axios = require('axios');

// 发送 GET 请求
axios.get('https://api.github.com/search/users?q=amazingang')
  .then(function (response) {
    // 处理成功的响应，response.data 是服务器返回的数据
    console.log(response.data);
  })
  .catch(function (error) {
    // 处理请求中的错误
    console.log(error);
  });

```





![axios](https://www.wtf.academy/assets/images/22-3-d6cf1a4ae0bad62fca527c911b741581.png)



## 总结

以上是 AJAX，Fetch API 和 axios 的简单介绍。在实际开发中，你可以根据你的需求和场景，选择最适合你的技术进行网络请求。

# 23. 事件循环

尽管 JavaScript 是单线程的编程语言，但是它可以通过事件循环机制处理并发操作，使 JavaScript 能够进行异步处理。JavaScript 将代码分为同步任务和异步任务，通过事件循环，异步任务在等待（如网络请求）期间不会阻塞主线程，可以同时执行其他任务。

> [!TIP]
>
> **同步任务**：直接按照代码顺序立即执行，例如变量声明、函数调用等。这些任务立即进入 **调用栈** 执行。
>
> **异步任务**：不立即执行的任务，例如 `setTimeout`、`fetch` 或者 `Promise`。这些任务在一定条件满足时会被推到 **任务队列** 中，等待执行。



## 调用栈和任务队列

在我们深入研究事件循环之前，我们需要理解以下两个概念：

- **调用栈（Call Stack）**：JavaScript只有一个调用栈，用于在代码执行时跟踪函数调用的位置。当函数被调用时，它被添加到堆栈的顶部。当函数返回时，它从堆栈中被移除。同步任务会直接进入调用栈。

> [!TIP]
>
> 1. **调用栈** 是一个后进先出（LIFO）的数据结构，用来跟踪当前正在执行的函数。当函数被调用时，它被添加到调用栈的顶部；当函数执行完毕后，它从调用栈移除。
> 2. 只要调用栈中还有任务要执行，JavaScript 就会继续执行这些任务。
> 3. 同步任务会立即进入调用栈，按照顺序执行。

- **任务队列（Task Queue）**：当异步任务（如setTimeout或fetch）完成时，它们的回调函数被添加到任务队列中。如果调用栈为空，事件循环会将这些回调函数一个接一个地移到调用栈中以便执行。

> [!TIP]
>
> 1. **任务队列** 是一个先进先出（FIFO）的数据结构，存储那些等待执行的异步任务。当一个异步任务完成（例如，网络请求响应或 `setTimeout` 达到时间），其回调函数就会被推入任务队列中。
> 2. 任务队列中的任务只有在调用栈清空时才会被执行。事件循环会不断检查调用栈是否为空，如果为空，就将任务队列中的第一个任务移动到调用栈执行。

![img](https://www.wtf.academy/assets/images/23-1-0a9e358174f208832687e58538cc132f.png)



## 宏任务和微任务

在 JavaScript 的事件循环机制中，任务被分为两种类型：宏任务和微任务。

- **宏任务（Macrotask）**：由 JavaScript 引擎线程直接执行的任务，包括整个脚本（main script），setTimeout 和 setInterval 的回调，setImmediate（Node.js环境）等。
- **微任务（Microtask）**：微任务是在当前宏任务结束后立即执行的任务，包括 Promise 的 then 和 catch 的回调，process.nextTick（Node.js环境），MutationObserver的回调（浏览器环境）等。

> [!TIP]
>
> 宏任务和微任务并不完全等价于同步任务和异步任务，虽然它们之间有一定的关系。以下是它们的区别和联系：
>
> ### 同步任务 vs. 异步任务
> - **同步任务**：在 JavaScript 中，同步任务是按照代码的顺序依次执行的任务，当前任务完成后才会执行下一个任务。这意味着，如果一个任务需要很长时间来完成，后面的任务将会被阻塞，直到前一个任务执行完成。
>
> - **异步任务**：异步任务是那些不会立即执行的任务，可以在等待某些操作完成时，继续执行其他任务。异步任务通常涉及到网络请求、定时器等操作。在异步任务完成后，会通过回调、Promise 或者事件来通知主线程。
>
> ### 宏任务 vs. 微任务
> - **宏任务（Macrotask）**：是异步任务中的一种，包括整个脚本（main script）、`setTimeout`、`setInterval`、`I/O` 等。宏任务会在事件循环的每个循环中逐一执行。
>
> - **微任务（Microtask）**：是另一种异步任务，主要包括 Promise 的 `then`、`catch` 回调、`MutationObserver` 的回调等。微任务的优先级高于宏任务，它们会在当前宏任务结束后立即执行，确保在事件循环的每个循环中尽可能早地处理微任务。
>
> ### 总结
> - **关系**：所有的宏任务和微任务都是异步任务，但并不是所有的异步任务都是宏任务或微任务。 
> - **区别**：宏任务和微任务在事件循环中的执行顺序和优先级不同。微任务总是在当前宏任务完成后优先执行，而宏任务则在事件循环的每一轮中被处理。
>

## 事件循环过程

事件循环的过程可以简化为以下几个步骤：

1. 从宏任务队列中取出一个任务来执行。
2. 执行完这个任务后，执行所有的微任务。
3. 当微任务队列清空后，进入下一次事件循环，执行下一个宏任务。

来看一个例子，展示了宏任务和微任务的执行顺序：

```javascript
console.log('script start');  // Macrotask

setTimeout(function() {
  console.log('setTimeout');  // Macrotask
}, 0);

Promise.resolve().then(function() {
  console.log('promise1');  // Microtask
}).then(function() {
  console.log('promise2');  // Microtask
});

console.log('script end');  // Macrotask
```



上述代码的输出顺序为：

```js
script start
script end
promise1
promise2
setTimeout
```



解释：

1. 首先，代码执行到`console.log('script start')`，输出 "script start"。
2. 然后，遇到`setTimeout`，将其回调函数推入宏任务队列中。
3. 接着，遇到`Promise.resolve().then()`，将第一个`then`回调函数推入微任务队列中。
4. 继续执行，遇到第二个`then`回调函数，将其推入微任务队列中。
5. 执行到`console.log('script end')`，输出 "script end"。
6. 当前宏任务（script主线程代码）执行完毕，事件循环开始处理微任务队列，按顺序执行微任务。
7. 执行第一个微任务，输出 "promise1"。
8. 执行第二个微任务，输出 "promise2"。
9. 微任务执行完毕，事件循环开始处理下一个宏任务。
10. 从宏任务队列中取出`setTimeout`的回调函数，输出 "setTimeout"。

> [!IMPORTANT]
>
> 以下是代码执行过程中调用栈和任务队列的状态变化：
>
> ### 初始状态
> - **调用栈**：空
> - **宏任务队列**：空
> - **微任务队列**：空
>
> ### 步骤 1
> 执行 `console.log('script start')`：
> - **输出**：`script start`
> - **调用栈**：空
> - **宏任务队列**：空
> - **微任务队列**：空
>
> ---
>
> ### 步骤 2
> 执行 `setTimeout`：
> - 将 `setTimeout` 的回调函数推入宏任务队列。
> - **调用栈**：空
> - **宏任务队列**：`['setTimeout']`
> - **微任务队列**：空
>
> ---
>
> ### 步骤 3
> 执行 `Promise.resolve().then(...)`：
> - 将第一个微任务（`promise1`）推入微任务队列。
> - **调用栈**：空
> - **宏任务队列**：`['setTimeout']`
> - **微任务队列**：`['promise1']`
>
> ---
>
> ### 步骤 4
> 执行 `console.log('script end')`：
> - **输出**：`script end`
> - **调用栈**：空
> - **宏任务队列**：`['setTimeout']`
> - **微任务队列**：`['promise1']`
>
> ---
>
> ### 步骤 5
> 处理微任务：
> - 从微任务队列中取出 `promise1` 执行。
> - **输出**：`promise1`
> - 在执行 `promise1` 时，将第二个微任务（`promise2`）添加到微任务队列。
> - **调用栈**：空
> - **宏任务队列**：`['setTimeout']`
> - **微任务队列**：`['promise2']`
>
> ---
>
> ### 步骤 6
> 处理宏任务：
> - 从宏任务队列中取出 `setTimeout` 执行。
> - **输出**：`setTimeout`
> - **调用栈**：空
> - **宏任务队列**：空
> - **微任务队列**：空
>
> ---
>
> ### 最终状态
> - **调用栈**：空
> - **宏任务队列**：空
> - **微任务队列**：空
>
> 通过这个过程，我们可以看到，JavaScript 如何通过事件循环机制协调宏任务和微任务的执行，使得异步操作不会阻塞主线程。

建议你在 [jsv9000](https://www.jsv9000.app/) 网站上体验一下事件循环的可视化，可以更直观的理解事件循环的过程。



![img](https://www.wtf.academy/assets/images/23-2-07e0e02a07c989869b373cc297937253.png)



## 总结

在这一讲，我们深入学习了 JavaScript 中的事件循环，包括宏任务和微任务。这是理解 JavaScript 异步编程的基础，能帮助我们更好地理解和控制代码的执行顺序。