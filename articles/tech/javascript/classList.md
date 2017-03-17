# 使用 classList API

## 一、classList API 是什么

1. 属于 DOM API，HTML5 引入，用来操作 HTML 标签的 `class` 属性值。
2. `classList` 属性是一个只读的类数组对象，“实时”地代表了元素的类名集合。
3. `classList` 对象上定义了 6 个实用的操作 `class` 属性值的方法。

## 二、`classList` 对象上的属性和方法

属性：

`length`：返回当前类列表中类的个数。

方法：

1. `add(class1, class2, ...)`：添加类
2. `remove(class1, class2, ...)`：删除类
3. `toggle(class[, force])`：当前类列表中如果不存在指定的类，则执行添加类操作，返回 `true`；否则执行删除类操作，返回 `false`。force 是一个函数，决定 `toggle` 方法最终执行何种操作——当函数返回 `true` 时，执行添加类操作，返回 `false`，执行删除类操作。
4. `contains(class)`：是否包含指定类。
5. `item(index)`：返回当前类列表中指定位置的类名。
6. `toString()`：返回当前类列表的字符串表示。

接下来会举些使用上述方法和属性的例子（这里有一个 [线上的例子](https://www.audero.it/demo/classlist-api-demo.html) ），这些例子都会用到下面这段 HTML 代码。

```html
<span id="element" class="description"></span>
```

### 2.1 `add()` 方法

添加一个类名：

```javascript
document.getElementById('element').classList.add('red');
// class="description red"
```

添加多个类名：

```javascript
document.getElementById('element').classList.add('red', 'bold');
// class="description red bold"
```

> {提示} 如果提供的类名已存在，就不会重复添加。

### 2.2 `remove()` 方法

删除一个类名：

```javascript
document.getElementById('element').classList.remove('description');
// class=""
```

删除多个类名：

```javascript
document.getElementById('element').classList.remove('description', 'red');
// class=""
```

### 2.3 `toggle()` 方法

```javascript
document.getElementById('element').classList.toggle('description');
// class=""

document.getElementById('element').classList.toggle('description');
// class="description"
```

### 2.4 `item()` 方法

```javascript
document.getElementById('element').classList.item(0);
// 返回 "description"

document.getElementById('element').classList.item(2);
// 返回 null
```

### 2.5 `contains` 方法

```javascript
if (document.getElementById('element').classList.contains('description')) {
   // 一些逻辑代码……
} else {
   // 不同的逻辑代码……
}
```

### 2.6 `toString()` 方法

```javascript
console.log(document.getElementById('element').classList.toString());
// 打印 "description"

document.getElementById('element').classList.add('red', 'bold');
console.log(document.getElementById('element').classList.toString());
// 打印 "description red bold"
```

### 2.7 `length` 属性

```javascript
console.log(document.getElementById('element').classList.length);
// 打印 1
```

## 浏览器兼容性

[IE10+ 和其他所有浏览器](http://caniuse.com/#search=classList)。其中 IE10+（包括土鳖 UC）属于部分支持，不支持的内容包括：

1. 不支持 SVG 或 MathML 元素。
2. 不支持 `toggle` 方法的第二个参数。
3. 不支持多参数形式的 `add()` 和 `remove()` 方法。

不过都是小事，可以使用 [polyfill](https://github.com/eligrey/classList.js) 解决。

## 参考链接

https://www.sitepoint.com/exploring-classlist-api/

（完）