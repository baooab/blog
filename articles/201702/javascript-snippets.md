# JavaScript 奇妙物语

## 目录

- 立即执行函数表达式
- ECMAScript `Function` 对象
- 如何做到 jQuery Free
- ES6
    - `rest` 参数和扩展运算符
- 辨析 `call()`、`apply` 和 `bind()`
- `Array.prototype.slice()` 将类数组转换成数组
- `Function.prototype.bind()` 参数绑定

---

## 立即执行函数表达式

```javascript
var a = 2;
(function foo() {
    var a = 3;
    console.log(a); // 3
})(); 
console.log(a); // 2
```

立即执行函数利用地就是函数表达式。这样带来的好处：避免函数名污染全局；避免显式调用函数。

`(function foo() { .. })` 作为函数表达式意味着 `foo` 只能在 `..` 所代表的位置中被访问。函数表达式可以是匿名的，而函数声明不可以省略函数名。始终给函数表达式命名是一个最佳实践。

## ECMAScript `Function` 对象

用户 `Function` 类创建函数的语法：

```javascript
var function_name = new function(arg1, arg2, ..., argN, function_body);
```

最后一个参数是函数主体，前面都是函数形参。

举个例子：

```javascript
function sayHi(sName, sMessage) {
  alert("Hello " + sName + sMessage);
}

// 相当于

var sayHi 
= 
new Function("sName", "sMessage", "alert(\"Hello \" + sName + sMessage);");
```

## 如何做到 jQuery Free

> 本文转载自[这里](http://www.ruanyifeng.com/blog/2013/05/jquery-free.html)。

### DOM 选择器

```javascript
function $(selector, context) {
  context = context || document;
  if (selector.indexOf('#') === 0) {
    return context.querySelectorAll(selector)[0];
  }
  return context.querySelectorAll(selector);;
}
```

### DOM 操作

```javascript
// 尾部追加
parent.appendChild(child);

// 之前插入
parent.insertBefore(child, parent.childNodes[0]);

// 删除
child.parentNode.removeChild(child)
```

### CSS 操作

```javascript
// className
document.body.className = 'hasJS';

// classList（IE 9不支持）
document.body.classList.add('hasJS');
document.body.classList.remove('hasJS');
document.body.classList.toggle('hasJS');
document.body.classList.contains('hasJS');

// DOM 元素的 style 属性
element.style.color = "red";
element.style.cssText += 'color:red';
```

### 事件处理

```javascript
// 监听
Element.prototype.on = Element.prototype.addEventListener;
NodeList.prototype.on = function (event, fn) {
    [].forEach.call(this, function (el) {
        el.on(event, fn);
    });
    return this;
};
// 触发
Element.prototype.trigger = function (type, data) {
    var event = document.createEvent('HTMLEvents');
    event.initEvent(type, true, true);
    event.data = data || {};
    event.eventName = type;
    event.target = this;
    this.dispatchEvent(event);
    return this;
};
NodeList.prototype.trigger = function (event) {
    [].forEach.call(this, function (el) {
      el['trigger'](event);
    });
    return this;
};
```

如何自定义事件和相关代码可以看[这里](http://www.zhangxinxu.com/wordpress/2012/04/js-dom%E8%87%AA%E5%AE%9A%E4%B9%89%E4%BA%8B%E4%BB%B6/)。

### Ajax 方法

```javascript
function request(type, url, opts, callback) {
  var xhr = new XMLHttpRequest();
  if (typeof opts === 'function') {
    callback = opts;
    opts = null;
  }
  xhr.open(type, url);
  var fd = new FormData();
  if (type === 'POST' && opts) {
    for (var key in opts) {
      fd.append(key, JSON.stringify(opts[key]));
    }
  }
  xhr.onload = function () {
    callback(JSON.parse(xhr.response));
  };
  xhr.send(opts ? fd : null);
}

var get = request.bind(this, 'GET');
var post = request.bind(this, 'POST');
```

## ES6

### `rest` 参数和扩展运算符

`rest` 参数的形式为 `...变量名`；扩展运算符是三个点 `...`。

#### `rest` 参数

```
function add(...values) {
  console.log(values);
} 

add([2, 3, 5]); // [Array[3]]
```

传递给 `add` 函数的一组参数值，被整合成了数组 `values`。没错，`rest` 参数搭配的变量是一个数组。这样就不需要使用 `arguments` 对象了。

需要注意的是，`rest` 参数后面不能再有其他参数

```
function f(a, ...b, c) {...} // 报错！
```

#### 扩展运算符

扩展运算符是 `rest`参数的逆运算，将数组转化为用逗号分隔的参数列表。

```
console.log(1, ...[2, 3, 5], 6); // 1 2 3 5 6
console.log(1, ...[2, 3, [5]], 6); // 1 2 3 [5] 6
```

## 辨析 `call()`、`apply` 和 `bind()`

`call()` 和 `apply` 指函数调用。`call()` 和 `apply()` 的区别仅是第二个参数的类型，`call()` 的第二个参数是一组值，`apply()` 的第二个参数是一
个数组。

```javascript
fn.call(ctx, arg1, arg2, arg3...);
fn.apply(ctx, [arg1, arg2, arg3...]);
```
`bind()` 是函数绑定，不会立即执行。若要执行函数代码，需要显式调用。

```javascript
fn.bind(ctx)(arg1, arg2, arg3...);
fn.bind(ctx)([arg1, arg2, arg3...]);
```

下面是例子：

```javascript
function sayHi() {
    let words = "我的名字叫" + this.name + ", 我" + this.age + "岁了。";
    if (arguments.length > 0) { words += "我喜欢吃"}
    for (let arg of arguments) {
        words += arg
    }
    console.log(words);
}

var name = "baooab";
var age = 25;
var me = {name, age};

// 皆输出：我的名字叫baooab, 我25岁了。我喜欢吃苹果梨子
sayHi.bind(me)("苹果","梨子");
sayHi.call(me, "苹果","梨子");
sayHi.apply(me, ["苹果","梨子"]);
```

## 使用 `slice` 将类数组转换成数组

`slice(start, end)` 可以用来截取数组（方式是返回一个新数组，不改变原数组），也可以将**类数组转换成数组**。类数组对象（array-like object）指有
数字索引和 `length` 属性的对象。比如：`NodeList` 集合以及函数内部的 `arguments` 对象。

```javascript
Array.prototype.slice.call(arguments);
Array.prototype.slice.call(myNodeList);
```

`slice` 方法的内部实现机制：当前上下文对象类型不是数组时，就当做类数组对象进行遍历，将遍历结果存入一个新建数组，最后返回该新数组。

## `bind` 方法的参数绑定

```javascript
function request(a, b) {
  console.log(a + ' ' + b);
}
var get = request.bind(this, 'GET');
var post = request.bind(this, 'POST');
get('/blog/1');
post('/user/create')
```

输出结果为

```
GET /blog/1
POST /user/create
```

可以发现：使用 `bind` 方法时，除了可以**指定上下文对象**，还可以**预赋参数**。以 `get` 方法为例，`request` 方法执行环境绑定到当前对象（`this`）后，又将被绑定方法的第一个参数赋值为 `GET`，然后调用 `get('/blog/1')`，
这相当于调用 `request('GET', '/blog/1')`（且 `request` 方法里的 `this` 指当前执行环境），所以打印结果为`GET /blog/1`。
