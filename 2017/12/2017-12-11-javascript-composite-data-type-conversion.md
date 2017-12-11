JavaScript 中的数据类型包括：基本数据类型和复合数据类型。

1. 基本数据类型：数字、字符串、布尔值、`null`、`undefined`。
2. 复合数据类型：对象、数组和函数。

复合数据类型转换就是转换为基本数据类型。包含  3 类情况：

1. 转换成布尔值。
2. 转换成数字。
3. 转换成字符串。

## 1 转换为布尔值

复合数据类型转换为布尔值都为 `true`。

```javascript
Boolean({}); // true
Boolean([]); // true
Boolean(function () {}); // true
```

## 2 转换成数字

### 2.1 对象&函数转换成数字

对象、函数都会转换成 `NaN`。

```javascript
Number({}); // NaN
Number(function () {}); // NaN
```

### 2.2 数组转换成数字

数组转换分 3 类情况：

1. 空数组。
	* 转换成 `0`。
2. 包含一个成员的数组。
	* 成员值能转换成数字，则数组最终转为这个数字。
	* 否则，转换成 `NaN`。
3. 其他情况。
	* 转换成 `NaN`。

```javascript
Number([]); // 0
Number(['18']); // 18
Number(['18x']); // NaN
Number(['18', '18x']); // NaN
```
 
## 3 转换成字符串

### 3.1 数组转换成字符串

数组转换为字符串的原理是调用了数组对象内部的 `.join(',')` 方法。所以结果是用 `,` 连接地、包含所有数组元素的一个字符串值。

```javascript
String([1,2,3]); // "1,2,3"
```

### 3.2 对象转换成字符串

除了日期对象（`Date`），其它情况都转换为 `"[object Object]"`。

```javascript
String({}); // "[object Object]"
```

### 3.3 函数转换成字符串

函数转为字符串的结果是把函数的整个内容作为字符串原样输出了。

```javascript
String(function () { console.log('keep'); });
// 输出："function () { console.log('keep'); }"

function foo() {
  return ;
}
String(foo);
// 输出：
// "function foo() {
//   return ;
// }"
```

