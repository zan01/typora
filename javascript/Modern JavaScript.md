# Modern JavaScript

## 学习要点

1. ES6 简介
2. ECMAScript 历史
3. 块级作用域
4. 数组的扩展
5. 箭头函数
6. rest 参数
7. 展开运算符
8. 解构赋值
9. 模板字符串
10. Class 和传统构造函数有何区别
11. Promise 的基本使用和原理
12. await 和 async
13. Map 和 Set
14. Iterator 和 for...of 循环
15. ES6 模块化

## ES6 简介

1. ECMAScript6 简称 ES6，是 JavaScript 语言的下一代标准；
2. ES6 的目标是为了实现更加复杂的应用，成为企业级的开发语言；
3. ECMAScript 属于标准制定，而 JavaScript 属于语法实现；
4. ES6 于 2015 年 6 月发布，正式名称为 ECMAScript2015；
5. 也就是说 ES6 是 ECMAScript 的一个版本，但却没有 6.x 的说法；
6. ES2016(ES7)、ES2017(ES8)、ES2018(ES9)、ES2019(ES10)版本路线；
7. 初学者可能会蒙圈，到底学哪个版本？这个问题，根本不重要~；
8. 因为它和软件版本不同，需要各大浏览器兼容性保持一致和兼容，超花时间；
9. 我们可以通过这个链接查看 ES6 兼容性情况，并且还有 ES5 和 ES2016+： http://kangax.github.io/compat-table/es6/
10. 经过五年多的发展兼容，ES6 大部分标准得以稳定，或者说 ES6 只是一个泛指；
11. 泛指下一代的标准，可以理解为涵盖 ES2015、ES2016、ES2017、ES2018 等；
12. 及时快到 2020 年，很多 JS 工具为了更好兼容，有 ES6 转换 ES5 的选项；

## ECMAScript 历史

| 版本  | 说明                                           |
| ----- | ---------------------------------------------- |
| ES1.0 | 1997 年发布                                    |
| ES2.0 | 1998 年 6 月份发布                             |
| ES3.0 | 1999 年 12 月份发布                            |
| ES4.0 | 2000 年没发布的了(废弃了)                      |
| ES4.0 | 2007 年 10 月草案发布(预计次年 8 月发布正式版) |
| ES3.1 | 2008 年 7 月发布(吵架把 ES4.0 吵成 3.1 了)     |
| ES5.0 | 2009 年 12 月发布(3.1 改成了 5.0)              |
| ES5.1 | 2011 年 6 月份发布                             |
| ES6   | 2013 年 3 月草案冻结                           |
| ES6   | 2013 年 12 月草案发布                          |

## 一、块级作用域

ES5 只有全局作用域和函数作用域（例如，我们必须将代码包在函数内来限制作用域），这导致很多问题：

**情况 1：内层变量覆盖外层变量**

```javascript
var tmp = new Date();
function f() {
  console.log(tmp); //undefined
  if (false) {
    var tmp = "hello world";
  }
}
```

**情况 2：变量泄露，成为全局变量**

```javascript
var s = "hello";
for (var i = 0; i < s.length; i++) {
  console.log(s[i]);
}
console.log(i); // 5
```

ES6 提供 let 和 const 来代替 var 声明变量，新的声明方式支持用大括号表示的块级作用域，这会带来一些好处：

**1.不再需要立即执行的函数表达式(IIFE)**

在 ES5 中，我们需要构造一个立即执行的函数表达式去保证我们不污染全局作用域。在 ES6 中， 我们可以使用更简单的大括号（{}），然后使用 const 或者 let 代替 var 来达到同样的效果。

**2.循环体中的闭包不再有问题**

在 ES5 中，如果循环体内有产生一个闭包，访问闭包外的变量，会产生问题。在 ES6，你可以使用 “let” 来避免问题。

**3.防止重复声明变量**

ES6 不允许在同一个作用域内用 let 或 const 重复声明同名变量。这对于防止在不同的 js 库中存在重复声明的函数表达式十分有帮助。

## 二、数组的扩展

**1. Array.from() : 将伪数组对象或可遍历对象转换为真数组**

**如果一个对象的所有键名都是正整数或零，并且有 length 属性**，那么这个对象就很像数组，称为**伪数组**。典型的伪数组有函数的 arguments 对象，以及大多数 DOM 元素集，还有字符串。

```html
<button>测试1</button>
<br />
<button>测试2</button>
<br />
<button>测试3</button>
<br />
<script type="text/javascript">
  let btns = document.getElementsByTagName("button");
  console.log("btns", btns); //得到一个伪数组
  btns.forEach((item) => console.log(item));
  // Uncaught TypeError: btns.forEach is not a function
</script>
```

针对伪数组，没有数组一般方法，直接遍历便会出错（所以使用 forEach 会报错）,ES6 新增 Array.from()方法来提供一种明确清晰的方式以解决这方面的需求。

```javascript
Array.from(btns).forEach((item) => console.log(item)); //将伪数组转换为数组
```

**2.Array.of(v1, v2, v3) : 将一系列值转换成数组**

当调用 new Array( )构造器时，根据传入参数的类型与数量的不同，实际上会导致一些不同的结果， 例如：

```javascript
let items = new Array(2);
console.log(items.length); // 2
console.log(items[0]); // undefined
console.log(items[1]);

let items = new Array(1, 2);
console.log(items.length); // 2
console.log(items[0]); // 1
console.log(items[1]); // 2
```

当使用单个数值参数来调用 Array 构造器时，数组的长度属性会被设置为该参数。 如果使用多个参数(无论是否为数值类型)来调用，这些参数也会成为目标数组的项。数组的这种行为既混乱又有风险，因为有时可能不会留意所传参数的类型。

ES6 引入了 Array.of( )方法来解决这个问题。该方法的作用非常类似 Array 构造器，但在使用单个数值参数的时候并不会导致特殊结果。**Array.of( )方法总会创建一个包含所有传入参数的数组，而不管参数的数量与类型**：

```javascript
let items = Array.of(1, 2);
console.log(items.length); // 2
console.log(items[0]); // 1
console.log(items[1]); // 2
items = Array.of(2);
console.log(items.length); // 1
console.log(items[0]); // 2
```

**Array.of 基本上可以用来替代 Array()或 newArray()，并且不存在由于参数不同而导致的重载，而且他们的行为非常统一。**

**3.数组实例的 find() 和 findIndex()**

数组实例的 find 方法，用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为 true 的成员，然后返回该成员。如果没有符合条件的成员，则返回 undefined。

```javascript
[1, 4, -5, 10].find((n) => n < 0); // -5
```

数组实例的 findIndex 方法的用法与 find 方法非常类似，返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回-1。

```javascript
[1, 5, 10, 15].findIndex(function (value, index, arr) {
  return value > 9;
}); // 2
```

**4.数组实例的 includes()**

Array.prototype.includes 方法返回一个布尔值，表示某个数组是否包含给定的值。该方法的第二个参数表示搜索的起始位置，默认为 0。如果第二个参数为负数，则表示倒数的位置，如果这时它大于数组长度（比如第二个参数为-4，但数组长度为 3），则会重置为从 0 开始。

```javascript
[1, 2, 3].includes(2); // true
[(1, 2, 3)].includes(3, -1); // true
[1, 2, 3, 5, 1].includes(1, 2); // true
```

没有该方法之前，我们通常使用数组的 indexOf 方法，检查是否包含某个值。indexOf 方法有两个缺点，一是不够语义化，它的含义是找到参数值的第一个出现位置，所以要去比较是否不等于-1，表达起来不够直观。二是，它内部使用严格相等运算符（===）进行判断，这会导致对 NaN 的误判。

```javascript
[NaN].indexOf(NaN); // -1
[NaN].includes(NaN); // true
```

**5.数组实例的 entries()，keys() 和 values()**

ES6 提供 entries()，keys()和 values(),用于遍历数组。它们都返回一个遍历器对象，可以用 for...of 循环进行遍历，唯一的区别是 keys()是对键名的遍历、values()是对键值的遍历，entries()是对键值对的遍历。

```javascript
for (let index of ["a", "b"].keys()) {
  console.log(index);
}
// 0
// 1

for (let elem of ["a", "b"].values()) {
  console.log(elem);
}
// 'a'
// 'b'

for (let [index, elem] of ["a", "b"].entries()) {
  console.log(index, elem);
}
// 0 "a"
// 1 "b"
```

## 三、箭头函数

ES6 允许使用“箭头”（=>）定义函数。它主要有两个作用：缩减代码和改变 this 指向，接下来我们详细介绍：

**1. 缩减代码**

```javascript
const double1 = function (number) {
  return number * 2; //ES5写法
};
const double2 = (number) => {
  return number * 2; //ES6写法
};
const double4 = (number) => number * 2; //可以进一步简化
```

**多个参数记得加括号**

```javascript
const double6 = (number, number2) => number + number2;
```

**如果箭头函数的代码块部分多于一条语句，就要使用大括号将它们括起来，并且使用 return 语句返回。**

```javascript
const double = (number, number2) => {
  sum = number + number2;
  return sum;
};
```

由于大括号被解释为代码块，所以**如果箭头函数直接返回一个对象，必须在对象外面加上括号，否则会报错。**

```javascript
// 报错
let getTempItem = id => { id: id, name: "Temp" };
// 不报
let getTempItem = id => ({ id: id, name: "Temp" });
```

**此外还有个好处就是简化回调函数**

```javascript
// 正常函数写法
[1, 2, 3].map(function (x) {
  return x * x;
});
// 箭头函数写法
[1, 2, 3].map((x) => x * x); //[1, 4, 9]
```

**2. 改变 this 指向**

长期以来，JavaScript 语言的 this 对象一直是一个令人头痛的问题，在对象方法中使用 this，必须非常小心。箭头函数”绑定”this，很大程度上解决了这个困扰。我们不妨先看一个例子：

```javascript
const team = {
  members: ["Henry", "Elyse"],
  teamName: "es6",
  teamSummary: function () {
    return this.members.map(function (member) {
      return `${member}隶属于${this.teamName}小组`; // this不知道该指向谁了
    });
  },
};
console.log(team.teamSummary()); //["Henry隶属于undefined小组", "Elyse隶属于undefined小组"]
```

teamSummary 函数里面又嵌了个函数，这导致内部的 this 的指向发生了错乱。

**那如何修改：**

方法一、let self = this

```javascript
const team = {
  members: ["Henry", "Elyse"],
  teamName: "es6",
  teamSummary: function () {
    let self = this;
    return this.members.map(function (member) {
      return `${member}隶属于${self.teamName}小组`;
    });
  },
};
console.log(team.teamSummary()); //["Henry隶属于es6小组", "Elyse隶属于es6小组"]
```

方法二、bind 函数

```javascript
const team = {
  members: ["Henry", "Elyse"],
  teamName: "es6",
  teamSummary: function () {
    return this.members.map(
      function (member) {
        // this不知道该指向谁了
        return `${member}隶属于${this.teamName}小组`;
      }.bind(this)
    );
  },
};
console.log(team.teamSummary()); //["Henry隶属于es6小组", "Elyse隶属于es6小组"]
```

方法三、 箭头函数

```javascript
const team = {
  members: ["Henry", "Elyse"],
  teamName: "es6",
  teamSummary: function () {
    return this.members.map((member) => {
      // this指向的就是team对象
      return `${member}隶属于${this.teamName}小组`;
    });
  },
};
console.log(team.teamSummary()); //["Henry隶属于es6小组", "Elyse隶属于es6小组"]
```

**3.使用注意点**

（1）函数体内的 this 对象，就是定义时所在的对象，而不是使用时所在的对象。

（2）不可以当作构造函数，也就是说，不可以使用 new 命令，否则会抛出一个错误。

（3）不可以使用 arguments 对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。

（4）不可以使用 yield 命令，因此箭头函数不能用作 Generator 函数。

## 四、rest 参数

**ES6 引入 rest 参数（形式为...变量名），用于获取函数的多余参数，这样就不需要使用 arguments 对象了。**

**rest 参数搭配的变量是一个数组，该变量将多余的参数放入数组中。**

我们举个例子：如何实现一个求和函数？

**【传统写法】**

```javascript
function addNumbers(a, b, c, d, e) {
  var numbers = [a, b, c, d, e];
  return numbers.reduce((sum, number) => {
    return sum + number;
  }, 0);
}
console.log(addNumbers(1, 2, 3, 4, 5)); //15
```

**【ES6 写法】**

```javascript
function addNumbers(...numbers) {
  return numbers.reduce((sum, number) => {
    return sum + number;
  }, 0);
}
console.log(addNumbers(1, 2, 3, 4, 5)); //15
```

**也可以与解构赋值组合使用**

```javascript
var array = [1, 2, 3, 4, 5, 6];
var [a, b, ...c] = array;
console.log(a); //1
console.log(b); //2
console.log(c); //[3, 4, 5, 6]
```

**rest 参数还可以与箭头函数结合**

```javascript
const numbers = (...nums) => nums;
numbers(1, 2, 3, 4, 5); // [1,2,3,4,5]
```

注意：

① 每个函数最多只能声明一个 rest 参数，而且 rest 参数必须是最后一个参数，否则报错。

②rest 参数不能用于对象字面量 setter 之中

```javascript
let object = {
  set name(...value) {
    //报错
    //执行一些逻辑
  },
};
```

## 五、展开运算符

与剩余参数关联最密切的就是扩展运算符。剩余参数允许你把多个独立的参数合并到一个数组中；而扩展运算符则允许将一个数组分割，并将各个项作为分离的参数传给函数。

**当用在字符串或数组前面时称为扩展运算符,个人觉得可以理解为 rest 参数的逆运算，用于将数组或字符串进行拆解**。有些时候，函数不允许传入数组，此时使用展开运算符就很方便，不信的话，咱们看个例子：Math.max()方法，它接受任意数量的参数，并会返回其中的最大值。

```javascript
let value1 = 25;
let value2 = 50;
console.log(Math.max(value1, value2)); //	50
```

但若想处理数组中的值，此时该如何找到最大值？Math.max()方法并不允许你传入一个数组。其实你可以像使用 rest 参数那样在该数组前添加...,并直接将其传递给 Math.max()。

```javascript
let values = [25, 50, 75, 100];
//等价于console.log(Math.max(25,50,75,100));
console.log(Math.max(...values)); //100
```

**扩展运算符还可以与其他参数混用**

```javascript
let values = [-25, -50, -75, -100];
console.log(Math.max(...values, 0)); //0
```

**扩展运算符拆解字符串与数组**

```javascript
var array = [1, 2, 3, 4, 5];
console.log(...array); //1 2 3 4 5
var str = "String";
console.log(...str); //S t r i n g
```

**还可以实现拼接**

```javascript
var defaultColors = ["red","greed"];
var favoriteColors = ["orange","yellow"];
var fallColors = ["fire red","fall orange"];
console.log(["blue","green",...fallColors,...defaultColors,...favoriteColors]
//["blue", "green", "fire red", "fall orange", "red", "greed", "orange", "yellow"]
```

## 六、解构赋值----更方便的数据访问

ES6 新增了解构，这是将一个数据结构分解为更小的部分的过程。

**1.解构为何有用？**

在 ES5 及更早版本中，从对象或数组中获取信息、并将特定数据存入本地变量，需要书写许多并且相似的代码。例如：

```javascript
var expense = {
  type: "es6",
  amount: "45",
};
var type = expense.type;
var amount = expense.amount;
console.log(type, amount);
```

此代码提取了 expense 对象的 type 与 amount 值，并将其存在同名的本地变量上。虽然 这段代码看起来简单，但想象一下若有大量变量需要处理，你就必须逐个为其赋值；并且若有一个嵌套的数据结构需要遍历以寻找信息，你可能会为了一点数据而挖掘整个结构。

这就是 ES6 为何要给对象与数组添加解构。当把数据结构分解为更小的部分时，从中提取你要的数据会变得容易许多。

**2.对象**

上个例子中如果采用对象解构的方法，就很容易获取 expense 对象的 type 与 amount 值。

```javascript
const { type, amount } = expense;
console.log(type, amount);
```

我们再来看个例子：

```javascript
let node = { type: "Identifier", name: "foo" },
  type = "Literal",
  name = 5;
({ type, name } = node); //	使用解构来分配不同的值
console.log(type); //	"Identifier"
console.log(name); //	"foo"
```

**注意:你必须用圆括号包裹解构赋值语句**，这是因为暴露的花括号会被解析为代码块语句，而块语句不允许在赋值操作符（即等号）左侧出现。圆括号标示了里面的花括号并不是块语句、而应该被解释为表达式，从而允许完成赋值操作。

**默认值：**

可以选择性地定义一个默认值，以便在指定属性不存在时使用该值。若要这么做，需要在 属性名后面添加一个等号并指定默认值，就像这样：

```javascript
let node = {
  type: "Identifier",
  name: "foo",
};
let { type, name, value = true } = node;
console.log(type); //	"Identifier"
console.log(name); //	"foo"
console.log(value); //	true
```

**嵌套对象解构：**

使用类似于对象字面量的语法，可以深入到嵌套的对象结构中去提取你想要的数据。

```javascript
let node = {
  type: "Identifier",
  name: "foo",
  loc: {
    start: {
      line: 1,
      column: 1,
    },
    end: {
      line: 1,
      column: 4,
    },
  },
};
let {
  loc: { start },
} = node;
console.log(start.line); //	1
console.log(start.column); //	1
```

本例中的解构模式使用了花括号，表示应当下行到 node 对象的 loc 属性内部去寻找 start 属性。

**必须传值的解构参数**

```javascript
function setCookie(name, value, { secure, path, domain, expires }) {
  //	设置cookie的代码
}
setCookie("type", "js"); //报错
```

在此函数内，name 与 value 参数是必需的，而 secure、path、domain 与 expires 则不是。默认情况下调用函数时未给参数解构传值会抛出错误。像上例中如果 setCookie 不传第三个参数，就会报错。若解构参数是可选的，可以给解构的参数提供默认值来处理这种错误。

```javascript
function setCookie(name, value, { secure, path, domain, expires } = {}) {}
setCookie("type", "js"); //不会报错
```

**3.数组**

```javascript
const names = ["Henry", "Bucky", "Emily"];
const [name1, name2, name3] = names;
console.log(name1, name2, name3); //Henry Bucky Emily
const [name, ...rest] = names; //结合展开运算符
console.log(rest); //["Bucky", "Emily"]
```

**用{}解构返回数组个数**

```javascript
const { length } = names;
console.log(length); //3
```

**数组解构也可以用于赋值上下文，但不需要用小括号包裹表达式**。这点跟对象解构的约定不同。

```javascript
let colors = ["red", "green", "blue"],
  firstColor = "black",
  secondColor = "purple";
[firstColor, secondColor] = colors;
console.log(firstColor); //	"red"
console.log(secondColor); // "green"
```

**默认值**：数组解构赋值同样允许在数组任意位置指定默认值。当指定位置的项不存在、或其值为 undefined，那么该默认值就会被使用。

```javascript
let colors = ["red"];
let [firstColor, secondColor = "green"] = colors;
console.log(firstColor); //	"red"
console.log(secondColor); //	"green"
```

**与 rest 参数搭配**

在 ES5 中常常使用 concat()方法来克隆数组，例如：

```javascript
//在ES5中克隆数组
var colors = ["red", "green", "blue"];
var clonedColors = colors.concat();
console.log(clonedColors); //"[red,green,blue]"
```

在 ES6 中，你可以使用剩余项的语法来达到同样效果

```javascript
//在ES6中克隆数组
let colors = ["red", "green", "blue"];
let [...clonedColors] = colors;
console.log(clonedColors); //[red,green,blue]
```

接下我们看个例子：如何将数组转化为对象

```javascript
const points = [
  [4, 5],
  [10, 1],
  [0, 40],
];
//期望得到的数据格式如下，如何实现？
// [
//   {x:4,y:5},
//   {x:10,y:1},
//   {x:0,y:40}
// ]
let newPoints = points.map((pair) => {
  const [x, y] = pair;
  return { x, y };
});
//还可以通过以下办法，更为简便
let newPoints = points.map(([x, y]) => {
  return { x, y };
});
console.log(newPoints);
```

**混合解构**

```javascript
const people = [
  { name: "Henry", age: 20 },
  { name: "Bucky", age: 25 },
  { name: "Emily", age: 30 },
];
//es5 写法
var age = people[0].age;
console.log(age);
//es6 解构
const [age] = people;
console.log(age); //第一次解构数组 {name:"Henry",age:20}
const [{ age }] = people; //再一次解构对象
console.log(age); //20
```

**4.注意点**

当使用解构来配合 var、let、const 来声明变量时，必须提供初始化程序（即等号右边的值）。下面的代码都会因为缺失初始化程序而抛出语法错误：

```javascript
var { type, name }; // 语法错误！
let { type, name }; // 语法错误！
const { type, name }; // 语法错误！
```

## 七、模板字符串（template string）

模板字符串是增强版的字符串，用反引号（`）标识。**它可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量**。

**模板字符串中嵌入变量和函数，需要将变量名写在\${}之中。**

```javascript
let name = "Henry";
function makeUppercase(word) {
  return word.toUpperCase();
}
let template = `
  <h1>${makeUppercase("Hello")}, ${name}!</h1>//可以存放函数和变量
  <p>感谢大家收看我们的视频, ES6为我们提供了很多遍历好用的方法和语法!</p>
  <ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
  </ul>
  `;
document.getElementById("template").innerHTML = template;
```

再举个例子，工作中常用到 ant-design-vue 库，在自定义一个弹出框时，使用模板字符串就很方便:

```javascript
this.$alert(
  `<p><strong>确认是否升级${this.lectureName}</strong><br>
    (若已存在讲义套件，升级后请重新生成)</p>`
);
```

## 八、Class 和传统构造函数有何区别

从概念上讲，在 ES6 之前的 JS 中并没有和其他面向对象语言那样的“类”的概念。长时间里，人们把使用 new 关键字通过函数（也叫构造器）构造对象当做“类”来使用。由于 JS 不支持原生的类，而只是通过原型来模拟，各种模拟类的方式相对于传统的面向对象方式来说非常混乱，尤其是处理当子类继承父类、子类要调用父类的方法等等需求时。

ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，作为对象的模板。通过 class 关键字，可以定义类。**但是类只是基于原型的面向对象模式的语法糖**。

**对比在传统构造函数和 ES6 中分别如何实现类：**

```javascript
//传统构造函数
function MathHandle(x,y){
  this.x = x;
  this.y = y;
}
MathHandle.prototype.add =function() {
  return this.x + this.y;
};
var m = new MathHandle(1,2);
console.log(m.add());

//class语法
class MathHandle {
  constructor(x,y){
    this.x = x;
    this.y = y;
  }

  add(){
    return this.x + this.y;
  }
}
const m = new MathHandle(1,2);
console.log(m.add())
```

这两者有什么联系？其实这两者本质是一样的，只不过是语法糖写法上有区别。所谓语法糖是指计算机语言中添加的某种语法，这种语法对语言的功能没有影响，但是更方便程序员使用。比如这里 class 语法糖让程序更加简洁，有更高的可读性。

```javascript
typeof MathHandle; //"function"
MathHandle === MathHandle.prototype.constructor; //true
```

**对比在传统构造函数和 ES6 中分别如何实现继承：**

```javascript
//传统构造函数继承
function Animal() {
  this.eat = function () {
    alert("Animal eat");
  };
}
function Dog() {
  this.bark = function () {
    alert("Dog bark");
  };
}
Dog.prototype = new Animal(); // 绑定原型，实现继承
var hashiqi = new Dog();
hashiqi.bark(); //Dog bark
hashiqi.eat(); //Animal eat

//ES6继承
class Animal {
  constructor(name) {
    this.name = name;
  }
  eat() {
    alert(this.name + " eat");
  }
}
class Dog extends Animal {
  constructor(name) {
    super(name); // 有extend就必须要有super，它代表父类的构造函数，即Animal中的constructor
    this.name = name;
  }
  say() {
    alert(this.name + " say");
  }
}
const dog = new Dog("哈士奇");
dog.say(); //哈士奇 say
dog.eat(); //哈士奇 eat
```

Class 之间可以通过 extends 关键字实现继承，这比 ES5 的通过修改原型链实现继承，要清晰和方便很多。

**Class 和传统构造函数有何区别**

- Class 在语法上更加贴合面向对象的写法
- Class 实现继承更加易读、易理解，对初学者更加友好
- 本质还是语法糖，使用 prototype

## 九、Promise 的基本使用和原理

在 JavaScript 的世界中，所有代码都是单线程执行的。由于这个“缺陷”，导致 JavaScript 的所有网络操作，浏览器事件，都必须是异步执行。**Promise 是异步编程的一种解决方案，比传统的解决方案(回调函数和事件)更合理和更强大**。

```javascript
fetch("/api/todos")
  .then((res) => res.json())
  .then((data) => ({ data }))
  .catch((err) => ({ err }));
```

ES6 中的 promise 的出现给我们很好的解决了**回调地狱**的问题，所谓的回调地狱是指当太多的异步步骤需要一步一步执行，或者一个函数里有太多的异步操作，这时候就会产生大量嵌套的回调，使代码嵌套太深而难以阅读和维护。ES6 认识到了这点问题，现在 promise 的使用，完美解决了这个问题。

**Promise 原理**

一旦状态改变，就不会再变，任何时候都可以得到这个结果。Promise 对象的状态改变，只有两种可能：从 pending 变为 fulfilled 和从 pending 变为 rejected。promise 对象初始化状态为 pending ；当调用 resolve(成功)，会由 pending => fulfilled ；当调用 reject(失败)，会由 pending => rejected。具体流程见下图：

![promise-onFulfilled_onRejected](https://tva1.sinaimg.cn/large/007S8ZIlgy1gg7rmqesijj309o057weu.jpg)

Promise 的使用流程

1、new Promise 一个实例，而且要 return

2、new Promise 时要传入函数，函数有 resolve reject 两个参数

3、成功时执行 resolve，失败时执行 reject

4、then 监听结果

```javascript
function loadImg(src){
   const promise=new Promise(function(resolve,reject){
     var img=document.createElement（'img'）
     img.onload=function(){
        resolve(img)
   }
     img.onerror=function（）{
        reject()
   }
    img.src=src
 })
  return promise//返回一个promise实例
}
var src="http://www.imooc.com/static/img/index/logo_new.png"
var result=loadImg(src)
result.then(function(img){
    console.log(img.width)//resolved(成功)时候的回调函数
},function(){
    console.log("failed")//rejected(失败)时候的回调函数
})
result.then(function(img){
    console.log(img.height)
})
```

Promise 会让代码变得更容易维护，像写同步代码一样写异步代码,同时业务逻辑也更易懂

## 十、await 和 async

通过 _async_ 函数，可以使得异步操作变得更加方便。返回值是个 _Promise_

```javascript
async function fetch() {
  await fetchData();
  return "done";
}
```

```javascript
async function logInOrder(urls) {
  // 并发读取远程URL
  const textPromises = urls.map(async (url) => {
    const response = await fetch(url);
    return response.text();
  });

  // 按次序输出
  for (const textPromise of textPromises) {
    console.log(await textPromise);
  }
}
```

## 十一、Map 和 Set

### Map

`Map` 中存储的是 `key-value` 形式的键值对, 其中的 `key` 和 `value` 可以是任何类型的, 即对象也可以作为 `key`。 `Map` 的出现，就是让各种类型的值都可以当作键。`Map` 提供的是 “值-值”的对应。

#### Map 和 Object 的区别

1. `Object` 对象有原型， 也就是说他有默认的 `key` 值在对象上面， 除非我们使用 `Object.create(null)`创建一个没有原型的对象；
2. 在 `Object` 对象中， 只能把 `String` 和 `Symbol` 作为 `key` 值， 但是在 `Map` 中，`key` 值可以是任何基本类型(`String`, `Number`, `Boolean`, `undefined`, `NaN`….)，或者对象(`Map`, `Set`, `Object`, `Function` , `Symbol` , `null`….);
3. 通过 `Map` 中的 `size` 属性， 可以很方便地获取到 `Map` 长度， 要获取 `Object` 的长度， 你只能手动计算

#### Map 的属性

- size: 返回集合所包含元素的数量

```js
const map = new Map();
map.set("foo", ture);
map.set("bar", false);
map.size; // 2
```

#### Map 对象的方法

- `set(key, val)`: 向 `Map` 中添加新元素
- `get(key)`: 通过键值查找特定的数值并返回
- `has(key)`: 判断 `Map` 对象中是否有 `Key` 所对应的值，有返回 `true`，否则返回 `false`
- `delete(key)`: 通过键值从 `Map` 中移除对应的数据
- `clear()`: 将这个 `Map` 中的所有元素删除

```js
const m = new Map();
const o = { p: "Hello World" };

m.set(o, "content");
m.get(o); // "content"

m.has(o); // true
m.delete(o); // true
m.has(o); // false
```

#### 遍历方法

- `keys()`：返回键名的遍历器
- `values()`：返回键值的遍历器
- `entries()`：返回键值对的遍历器
- `forEach()`：使用回调函数遍历每个成员

```javascript
const map = new Map([
  ["a", 1],
  ["b", 2],
]);

for (let key of map.keys()) {
  console.log(key);
}
// "a"
// "b"

for (let value of map.values()) {
  console.log(value);
}
// 1
// 2

for (let item of map.entries()) {
  console.log(item);
}
// ["a", 1]
// ["b", 2]

// 或者
for (let [key, value] of map.entries()) {
  console.log(key, value);
}
// "a" 1
// "b" 2

// for...of...遍历map等同于使用map.entries()

for (let [key, value] of map) {
  console.log(key, value);
}
// "a" 1
// "b" 2
```

#### 数据类型转化

Map 转为数组

```js
let map = new Map();
let arr = [...map];
```

数组转为 Map

```js
Map: map = new Map(arr);
```

Map 转为对象

```js
let obj = {};
for (let [k, v] of map) {
  obj[k] = v;
}
```

对象转为 Map

```js
for( let k of Object.keys(obj)）{
  map.set(k,obj[k])
}
```

#### Map 的应用

在一些 Admin 项目中我们通常都对个人信息进行展示，比如将如下信息展示到页面上。传统方法如下。

```html
<div class="info-item">
  <span>姓名</span>
  <span>{{info.name}}</span>
</div>
<div class="info-item">
  <span>年龄</span>
  <span>{{info.age}}</span>
</div>
<div class="info-item">
  <span>性别</span>
  <span>{{info.sex}}</span>
</div>
<div class="info-item">
  <span>手机号</span>
  <span>{{info.phone}}</span>
</div>
<div class="info-item">
  <span>家庭住址</span>
  <span>{{info.address}}</span>
</div>
<div class="info-item">
  <span>家庭住址</span>
  <span>{{info.duty}}</span>
</div>
```

js 代码

```js
mounted() {
  this.info = {
    name: 'jack',
    sex: '男',
    age: '28',
    phone: '13888888888',
    address: '广东省广州市',
    duty: '总经理'
  }
}
```

我们通过 Map 来改造，将我们需要显示的 label 和 value 存到我们的 Map 后渲染到页面，这样减少了大量的 html 代码

```html
<template>
  <div id="app">
    <div class="info-item" v-for="[label, value] in infoMap" :key="value">
      <span>{{label}}</span>
      <span>{{value}}</span>
    </div>
  </div>
</template>
```

js 代码

```js
data: () => ({
  info: {},
  infoMap: {}
}),
mounted () {
  this.info = {
    name: 'jack',
    sex: '男',
    age: '28',
    phone: '13888888888',
    address: '广东省广州市',
    duty: '总经理'
  }
  const mapKeys = ['姓名', '性别', '年龄', '电话', '家庭地址', '身份']
  const result = new Map()
  let i = 0
  for (const key in this.info) {
    result.set(mapKeys[i], this.info[key])
    i++
  }
  this.infoMap = result
}
```

### WeakMap

`WeakMap` 结构与 `Map` 结构类似，也是用于生成键值对的集合。

- 只接受对象作为键名（`null` 除外），不接受其他类型的值作为键名
- 键名是弱引用，键值可以是任意的，键名所指向的对象可以被垃圾回收，此时键名是无效的
- 不能遍历，方法有 `get`、`set`、`has`、`delete`

### Set

`Set` 本身是一个构造函数，用来生成 `Set` 数据结构。`Set` 函数可以接受一个数组（或者具有 iterable 接口的其他数据结构）作为参数，用来初始化。`Set` 对象允许你存储任何类型的值，无论是原始值或者是对象引用。它类似于数组，但是成员的值都是唯一的，没有重复的值。

```js
const s = new Set()[(2, 3, 5, 4, 5, 2, 2)].forEach((x) => s.add(x));
for (let i of s) {
  console.log(i);
}
// 2 3 5 4
```

#### Set 中的特殊值

`Set` 对象存储的值总是唯一的，所以需要判断两个值是否恒等。有几个特殊值需要特殊对待：

- +0 与 -0 在存储判断唯一性的时候是恒等的，所以不重复
- `undefined` 与 `undefined` 是恒等的，所以不重复
- `NaN` 与 `NaN` 是不恒等的，但是在 `Set` 中认为 `NaN` 与 `NaN` 相等，所有只能存在一个，不重复。

#### Set 的属性：

- `size`：返回集合所包含元素的数量

```js
const items = new Set([1, 2, 3, 4, 5, 5, 5, 5]);
items.size; // 5
```

#### Set 实例对象的方法

- `add(value)`：添加某个值，返回 `Set` 结构本身(可以链式调用)。
- `delete(value)`：删除某个值，删除成功返回 `true`，否则返回 `false`。
- `has(value)`：返回一个布尔值，表示该值是否为 `Set` 的成员。
- `clear()`：清除所有成员，没有返回值。

```js
s.add(1).add(2).add(2);
// 注意2被加入了两次

s.size; // 2

s.has(1); // true
s.has(2); // true
s.has(3); // false

s.delete(2);
s.has(2); // false
```

#### 遍历方法

- `keys()`：返回键名的遍历器。
- `values()`：返回键值的遍历器。
- `entries()`：返回键值对的遍历器。
- `forEach()`：使用回调函数遍历每个成员。

由于 `Set` 结构没有键名，只有键值（或者说键名和键值是同一个值），所以 `keys` 方法和 `values` 方法的行为完全一致。

```js
let set = new Set(["red", "green", "blue"]);

for (let item of set.keys()) {
  console.log(item);
}
// red
// green
// blue

for (let item of set.values()) {
  console.log(item);
}
// red
// green
// blue

for (let item of set.entries()) {
  console.log(item);
}
// ["red", "red"]
// ["green", "green"]
// ["blue", "blue"]
```

#### Array 和 Set 对比

- `Array` 的 `indexOf` 方法比 `Set` 的 `has` 方法效率低下
- `Set` 不含有重复值（可以利用这个特性实现对一个数组的去重）
- `Set` 通过 `delete` 方法删除某个值，而 `Array` 只能通过 `splice`。两者的使用方便程度前者更优
- `Array` 的很多新方法 `map`、`filter`、`some`、`every` 等是 `Set` 没有的（但是通过两者可以互相转换来使用）

#### Set 的应用

1、`Array.from` 方法可以将 `Set` 结构转为数组。

```js
const items = new Set([1, 2, 3, 4, 5]);
const array = Array.from(items);
```

2、数组去重

```js
// 去除数组的重复成员
[...new Set(array)];

Array.from(new Set(array));
```

3、数组的 `map` 和 `filter` 方法也可以间接用于 `Set`

```js
let set = new Set([1, 2, 3]);
set = new Set([...set].map((x) => x * 2));
// 返回Set结构：{2, 4, 6}

let set = new Set([1, 2, 3, 4, 5]);
set = new Set([...set].filter((x) => x % 2 == 0));
// 返回Set结构：{2, 4}
```

4、实现并集 `(Union)`、交集 `(Intersect)` 和差集

```js
let a = new Set([1, 2, 3]);
let b = new Set([4, 3, 2]);

// 并集
let union = new Set([...a, ...b]);
// Set {1, 2, 3, 4}

// 交集
let intersect = new Set([...a].filter((x) => b.has(x)));
// set {2, 3}

// 差集
let difference = new Set([...a].filter((x) => !b.has(x)));
// Set {1}
```

### WeakSet

`WeakSet` 结构与 `Set` 类似，也是不重复的值的集合。

- 成员都是数组和类似数组的对象，若调用 `add()` 方法时传入了非数组和类似数组的对象的参数，就会抛出错误。

```js
const b = [1, 2, [1, 2]];
new WeakSet(b); // Uncaught TypeError: Invalid value used in weak set
```

- 成员都是弱引用，可以被垃圾回收机制回收，可以用来保存 DOM 节点，不容易造成内存泄漏。
- `WeakSet` 不可迭代，因此不能被用在 `for-of` 等循环中。
- `WeakSet` 没有 `size` 属性。

## 十二、Iterator 和 for...of 循环

JavaScript 原有的表示“集合”的数据结构，主要是数组（Array）和对象（Object），ES6 又添加了 Map 和 Set。这样就需要一种统一的接口机制，来处理所有不同的数据结构。遍历器（Iterator）就是这样一种机制。它是一种接口，为各种不同的数据结构提供统一的访问机制。**任何数据结构只要部署 Iterator 接口，就可以完成遍历操作（即依次处理该数据结构的所有成员）**。

**1.Iterator 的作用：**

- 为各种数据结构，提供一个统一的、简便的访问接口；
- 使得数据结构的成员能够按某种次序排列
- ES6 创造了一种新的遍历命令 for...of 循环，Iterator 接口主要供 for...of 消费。

**2.原生具备 iterator 接口的数据(可用 for of 遍历)**

- Array
- set 容器
- map 容器
- String
- 函数的 arguments 对象
- NodeList 对象

```javascript
let arr3 = [1, 2, "kobe", true];
for (let i of arr3) {
  console.log(i); // 1 2 kobe true
}
复制代码;
let str = "abcd";
for (let item of str) {
  console.log(item); // a b c d
}
复制代码;
var engines = new Set(["Gecko", "Trident", "Webkit", "Webkit"]);
for (var e of engines) {
  console.log(e);
}
// Gecko
// Trident
// Webkit
```

**3.几种遍历方式比较**

- for of 循环不仅支持数组、大多数伪数组对象，也支持字符串遍历，此外还支持 Map 和 Set 对象遍历。
- for in 循环可以遍历字符串、对象、数组，不能遍历 Set/Map
- forEach 循环不能遍历字符串、对象,可以遍历 Set/Map

## 十三、ES6 模块化

ES6 在语言标准的层面上，实现了模块功能，而且实现得相当简单，旨在成为浏览器和服务器通用的模块解决方案。其模块功能主要由两个命令构成：export 和 import。export 命令用于规定模块的对外接口，import 命令用于输入其他模块提供的功能。

```javascript
/** 定义模块 math.js **/
var basicNum = 0;
var add = function (a, b) {
  return a + b;
};
export { basicNum, add };
/** 引用模块 **/
import { basicNum, add } from "./math";
function test(ele) {
  ele.textContent = add(99 + basicNum);
}
```

如上例所示，使用 import 命令的时候，用户需要知道所要加载的变量名或函数名，否则无法加载。为了给用户提供方便，让他们不用阅读文档就能加载模块，就要用到 export default 命令，为模块指定默认输出。

```javascript
// export-default.js
export default function () {
  console.log("foo");
}
```

上面代码是一个模块文件 export-default.js，它的默认输出是一个函数。 **其他模块加载该模块时，import 命令可以为该匿名函数指定任意名字。**

```javascript
// import-default.js
import customName from "./export-default";
customName(); // 'foo'
```

上面代码的 import 命令，可以用任意名称指向 export-default.js 输出的方法，这时就不需要知道原模块输出的函数名。**需要注意的是，这时 import 命令后面，不使用大括号。**

## 参考：

- [JavaScript Promise 迷你书](http://liubin.org/promises-book/)
- [ES6 入门教程](https://es6.ruanyifeng.com/)
- [彻底弄懂 ES6 中的 Map 和 Set](https://juejin.im/post/5cece5e9e51d45105e021238)
- [现代 JavaScript 教程](https://zh.javascript.info/)
