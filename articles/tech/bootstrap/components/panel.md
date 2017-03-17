# Bootstrap 组件之 Panel

## 一、简介

Panel 指面板。[这里](http://codepen.io/zhangbao/full/WpZaYO/) 有例子。

一个典型的面板的代码结构是这样的：

```
.panel.panel-default
    .panel-heading
        .panel-title
            Title Text
    .panel-body
        Body Text
    .panel-footer
        Footer Text
```

除了使用 `.panel-default` 这个默认样式，还可以使用的样式有：

1. `panel-primary`。
2. `panel-success`。
3. `panel-info`。
4. `panel-warning`。
5. `panel-danger`。

Panel 强大得还有一点，就是能搭配其它组件使用，这些组件包括：表格（tables）和列表（list groups）。

## 二、搭配表格

```html
<div class="panel panel-default">
    <div class="panel-heading">Panel heading</div>
    <table class="table">
        <!-- ... -->
    </table>
</div>
```

> {提示} `<table>` 与 `.panel-heading` 是在一个层次的。

## 三、搭配列表

```html
<div class="panel panel-default">
    <div class="panel-heading">Panel heading</div>
    <div class="panel-body">
        <p>some text</p>
    </div>
    <ul class="list-group">
        <li class="list-group-item">Cras justo odio</li>
        <li class="list-group-item">Dapibus ac facilisis in</li>
        <li class="list-group-item">Morbi leo risus</li>
        <li class="list-group-item">Porta ac consectetur ac</li>
        <li class="list-group-item">Vestibulum at eros</li>
    </ul>
</div>
```

> {提示} `.list-group` 与 `.panel-heading`、`.panel-body` 是在一个层次的。

## 四、参考链接

http://getbootstrap.com/components/#panels

（完）