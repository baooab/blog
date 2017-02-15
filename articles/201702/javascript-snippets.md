# JavaScript 奇妙物语

## 目录

- `bind` 方法的参数绑定

---

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
