# JavaScript 奇妙物语

## 目录

- `Array.prototype.slice()` 将类数组转换成数组
- `Function.prototype.bind()` 参数绑定

---

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
