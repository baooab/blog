# Bootstrap 的 ScrollSpy

## 一、简介

ScrollSpy 就是滚动监听。设置滚动监听方式有两种：

1. 标签 API
2. JavaScript 代码

监听区域也有两种可能：

1. `body` 标签
2. 自定义标签元素

> {注意} ScrollSpy 需要 [nav 组件的代码](http://getbootstrap.com/components/#nav) 支持，才会正确高亮激活项。

## 二、通过标签 API

通过标签 API 设置滚动监听的方式，就是在要监听区域上：

1. 标记为滚动区域：添加 `data-spy="scroll"`。
2. 指明在滚动过程中受到激活控制的代码单元：`data-target="#navbarWrapper"`。

### 2.1 借助 `body` 标签

```css
body {
    margin-top: 51px;
}

article {
    height: 500px;
}
```

```html
<body data-spy="scroll" data-offset="71" data-target="#navbarWrapper">
    <div id="navbarWrapper" class="navbar navbar-default navbar-fixed-top">
        <div class="navbar-header">
            <a class="navbar-brand" href="#">Project name</a>
        </div>
        <ul class="nav navbar-nav navbar-right">
            <li><a href="#home">Home</a></li>
            <li><a href="#profile">Profile</a></li>
            <li><a href="#messages">Messages</a></li>
        </ul>
    </div>
    <div id="contentWrapper" class="container">
        <article id="home"><h2>Home</h2><P>...</P></article>
        <article id="profile"><h2>Profile</h2><P>...</P></article>
        <article id="messages"><h2>Messages</h2><P>...</P></article>
    </div>
</body>
```

这里使用了 [固定在顶部的导航条](http://v3.bootcss.com/components/#navbar-fixed-top)，导航条本身有高度 `51px`，为了不会遮挡住 `#contentWrapper` 内容区域，需要给 `body` 设置 `margin-top: 51px`；内容区域中，`#home` 中的 `h2` 标签默认有样式 `margin-top: 20px`。

那么页面加载完成后，若想让 `#home` 导航项激活，需要给滚动区域（这里指 `<body>`）添加偏移量 `data-offset="71"`（至少为 `51px` + `20px` = `71px`）。

### 2.2 借助自定义标签

[这里](http://codepen.io/zhangbao/full/zZdeqa/) 是完整的例子。

```css
#scrollableWrapper {
    height:200px;
    overflow:auto;
    position: relative;
}

article {
    height: 500px;
}
```

```html
<div id="navbarWrapper" class="navbar navbar-default navbar-static">
    <div class="navbar-header">
        <a class="navbar-brand" href="#">Project name</a>
    </div>
    <ul class="nav navbar-nav pull-right">
        <li><a href="#home">Home</a></li>
        <li><a href="#profile">Profile</a></li>
        <li><a href="#messages">Messages</a></li>
    </ul>
</div>
<div id="scrollableWrapper" data-spy="scroll" data-offset="20" data-target="#navbarWrapper">
    <article id="home"><h2>Home</h2></article>
    <article id="profile"><h2>Profile</h2></article>
    <article id="messages"><h2>Messages</h2></article>
</div>
```

因为 `#home` 中的 `h2` 标签有默认样式 `margin-top: 20px`，所以还需要给滚动区域（这里指 `#scrollableWrapper`）添加偏移量 `data-offset="20"`。

## 三、通过 JavaScript 代码

### 3.1 借助 `body` 标签

```css
body {
    margin-top: 51px;
}

article {
    height: 500px;
}
```

```html
<body>
    <div id="navbarWrapper" class="navbar navbar-default navbar-fixed-top">
        <!-- some code -->
    </div>
    <!-- some code -->
</body>
```

```javascript
$('body').scrollspy({
    target: '#navbarWrapper',
    offset: 71
})
```

### 3.2 借助自定义标签

```css
#scrollableWrapper {
    height:200px;
    overflow:auto;
    position: relative;
}

article {
    height: 500px;
}
```

```html
<div id="navbarWrapper" class="navbar navbar-default navbar-static">
    <!-- some code -->
</div>
<div id="scrollableWrapper">
    <!-- some code -->
</div>
```

```javascript
$('#scrollableWrapper').scrollspy({
    target: '#navbarWrapper',
    offset: 20
})
```

## 四、ScrollSpy 的事件回调

在滚动监听过程中，每当激活一个导航项，都会触发一个事件 `activate.bs.scrollspy`。必要时，可在这个事件的回调函数里写些业务逻辑。

```javascript
$('#navbarWrapper').on('activate.bs.scrollspy', function (e) {
    console.log(e.target);
})
```

## 五、参考链接

http://getbootstrap.com/javascript/#scrollspy

（完）