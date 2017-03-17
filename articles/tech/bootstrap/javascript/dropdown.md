# Bootstrap 的 Dropdown

## 一、简介

Dropdown 就是下拉列表，[这里](http://codepen.io/zhangbao/full/GWvwaG/) 有一个例子。

Dropdown 的完整代码如下：

```html
<div id="dropdownWrapper">
    <button class="btn btn-default dropdown-toggle" type="button" id="btnTargetDropdownMenu" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
        Dropdown <span class="caret"></span>
    </button>
    <ul class="dropdown-menu" aria-labelledby="btnTargetDropdownMenu">
        <li class="dropdown-header">Dropdown header</li>
        <li><a href="#">Action</a></li>
        <li><a href="#">Another action</a></li>
        <li class="disabled"><a href="#">Something else here</a></li>
        <li role="separator" class="divider"></li>
        <li><a href="#">Separated link</a></li>
    </ul>
</div>
```

> {提示}
> 1. `.dropdown-toggle` 这个类不是必须的，不过稍后讲到 Dropdown 的 JavaScript 代码调用时要使用它，所以为了方便，先在这里一并写入。
> 2. `#dropdownWrapper` 表示 Dropdown 的容器，可根据具体情况命名，稍后讲到事件回调时，要用到它。

默认的 Dropdown 是隐藏的，让它出现有两种方式：

1. 标签 API
2. JavaScript 代码

## 二、通过标签 API

1. 在 `.dropdown-toggle` 上添加 `data-toggle="dropdown"`（重申：`.dropdown-toggle` 不是必须添加的）。
2. 下拉菜单 `<ul>` 添加 `.dropdown-menu`。

## 三、通过 JavaScript 代码

使用 `$('.dropdown-toggle').dropdown('toggle');` 可以让下拉框展开。

> {注意} 无论是使用标签 API 还是 JavaScript 代码，**`data-toggle="dropdown"` 始终要写上**。

## 四、Dropdown 的事件回调

**Dropdown 回调事件总是在 `.dropdown-menu` 的父元素上触发（此处指  `#dropdownWrapper`）**。事件种类主要有四个：

1. `show.bs.dropdown` ：在 Dropdown 显示时触发。
2. `shown.bs.dropdown` ：在 Dropdown 显示之后触发。
3. `hide.bs.dropdown` ：在 Dropdown 隐藏时触发。
4. `hidden.bs.dropdown` ：在 Dropdown 隐藏之后触发。

举个例子：

```javascript
$('#dropdownWrapper').on('shown.bs.dropdown', function showDropdown() {
    console.log('Dropdown is showed!');
});
```

## 五、设备可访问性

为了提高代码的设备可访问性，我们给 Dropdown 添加一些额外代码。

1. 在 `#btnTargetDropdownMenu` 上：添加 `aria-haspopup="true"`，表示有子菜单。
2. 在 `#btnTargetDropdownMenu` 上：添加 `aria-expanded="false"`，表示菜单现在没有展开。
3. 在 `.dropdown-menu` 上：添加 `aria-labelledby="..."`，值为受指向标签的 `id`，在这里等同于设置 `aria-label="Dropdown"`，屏幕阅读器读到这里时，就会读出 `Dropdown` 这个单词。

## 六、参考链接

http://getbootstrap.com/javascript/#dropdowns

（完）