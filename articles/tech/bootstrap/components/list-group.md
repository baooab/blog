# Bootstrap 组件之 List group

## 一、简介

List group 指列表。当然，Bootstrap 列表不局限于由 `<ul>` 和 `<li>` 标签构成的。

Bootstrap 中一共三种列表的构成方式，[这里](http://codepen.io/zhangbao/full/MpEqBe/) 有一个例子：

1. `ul > li`。
2. `div > a`。
3. `div > button`。

列表就是“父与子”的关系。在 Bootstrap 中，“父”要标记上 `list-group`，“子”要标记上 `list-group-item`。

## 二、`ul > li`

```html
<ul class="list-group">
    <li class="list-group-item acive">1</li>
    <li class="list-group-item">2</li>
    <li class="list-group-item">3</li>
</ul>
```

稍复杂些的：

```html
<ul class="list-group">
    <li class="list-group-item active"><span class="badge">14</span>1</li>
    <li class="list-group-item">2</li>
    <li class="list-group-item">3</li>
</ul>
```

## 三、`div > a`

```html
<ul class="list-group">
    <a href="javascript:void(0);" class="list-group-item">1</a>
    <a href="javascript:void(0);" class="list-group-item active"><span class="badge">14</span>2</a>
    <a href="javascript:void(0);" class="list-group-item">3</a>
</ul>
```

## 四、`div > button`

```html
<ul class="list-group">
    <button type="button" class="list-group-item">1</button>
    <button type="button" class="list-group-item">2</button>
    <button type="button" class="list-group-item active"><span class="badge">14</span>3</button>
</ul>
```

## 五、参考链接

http://getbootstrap.com/components/#list-group

（完）