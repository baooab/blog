# Bootstrap 组件之 Nav

## 一、简介

Nav 指导航页。[这里](http://codepen.io/zhangbao/full/YZrOKr/) 是一个线上例子。

使用了 `.nav` 的标签就是一个 Nav。下面举例。

> {注意} 记住，下面的几种导航页都依赖 `.nav`。

## 二、导航页

添加 `.nav-tabs`。

```html
<ul class="nav nav-tabs">
  <li role="presentation" class="active"><a href="#">Home</a></li>
  <li role="presentation"><a href="#">Profile</a></li>
  <li role="presentation"><a href="#">Messages</a></li>
</ul>
```

## 三、胶囊式导航页

将 `.nav-tabs` 换为 `nav-pills`。

```html
<ul class="nav nav-pills">
  <li role="presentation" class="active"><a href="#">Home</a></li>
  <li role="presentation"><a href="#">Profile</a></li>
  <li role="presentation"><a href="#">Messages</a></li>
</ul>
```

## 四、堆叠胶囊式导航页

添加 `.nav-stacked`.

```html
<ul class="nav nav-pills nav-stacked">
  <li role="presentation" class="active"><a href="#">Home</a></li>
  <li role="presentation"><a href="#">Profile</a></li>
  <li role="presentation"><a href="#">Messages</a></li>
</ul>
```

## 五、禁用的链接

在 `<li>` 上添加 `.disabled`。

> {注意} `.disabled` 只改变 `<a>` 的外观，不改变功能——链接依然有效。

## 六、带下拉菜单的导航页

```html
<ul class="nav nav-pills">
    <li role="presentation" class="active"><a href="#">Home</a></li>
    <li role="presentation"><a href="#">Profile</a></li>
    <li role="presentation">
        <a class="dropdown-toggle" data-toggle="dropdown" href="javascript:void(0);" role="button" aria-haspopup="true" aria-expanded="false">
            Messages <span class="caret"></span>
        </a>
        <ul class="dropdown-menu">
            <li><a href="#">1</a></li>
            <li><a href="#">2</a></li>
            <li><a href="#">3</a></li>
            <li role="separator" class="divider"></li>
            <li><a href="#">4</a></li>
        </ul>
    </li>
</ul>
```

实现下拉菜单必需的两个标签属性：

1. 在 `<a>` 上，添加 `data-toggle="dropdown"`。
2. 在 `<ul>` 上，添加 `class="dropdown-menu"`。

## 七、参考链接

http://getbootstrap.com/components/#nav

（完）