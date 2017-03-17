# bootstrap.js 文件使用指南

## 介绍

使用 Bootstrap v3.3.7 时，需要引入三个脚本文件。

1. https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css
2. http://lib.sinaapp.com/js/jquery/1.12.4/jquery-1.12.4.min.js
3. https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js

这里面有一个文件，是 `bootstrap.min.js`（是 bootstrap.js 文件的压缩版）。

Bootstrap 有许多现成、可重用的 [components 代码](http://getbootstrap.com/components/) 供使用，而真正让这些 components bring to life 的，就是靠 `bootstrap.js` 这个文件。

`bootstrap.js` 文件依赖 jQuery，实际上它是在 jQuery 基础上封装的一系列插件，不过这些插件是针对 Bootstrap 的 components 编写的。所以**在使用 `bootstrap.js` 之前，务必引入 jQuery**。

`bootstrap.js` 包含了 Bootstrap 所有插件代码。如果嫌多，也可以定制。

**使用 Bootstrap 插件，你完全可以不用写一行  JavaScript 代码——直接通过标签  API 完成插件的初始化和环配置**。但是学会怎样完全通过 JavaScript 代码来初始化和配置所有插件也是非常有必要的。

## transition.js 文件

Bootstrap 中一些动态过渡效果使用了这个文件里的代码，但 `bootstrap.js` 文件已经包含了它，无需再单独引入。

（完）