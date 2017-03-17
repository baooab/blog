# Bootstrap 的 Collapse

## 一、简介

Collapse 插件为 HTML 标签提供折叠、展开行为，依赖 [transition.js](http://getbootstrap.com/javascript/#transitions)（`bootstrap.js` 文件中已包含）。

## 二、实现机制

实现 Collapse 效果需要：

1. 一个 `<a>` 标签或者 `<button>` 标签：`<a>` 标签使用 `href` 属性；`<button>` 标签使用 `data-target` 属性。
2. 上面两种情况，都要添加 `data-toggle="collapse"` 属性。
3. 被 Collapse 的目标标签要设置 id 以及添加样式 `.collapse`。

## 三、简单的 Collapse

下面是一个简单 Collapse 的完整例子（线上例子在 [这里](http://codepen.io/zhangbao/full/JWGZbx/)）：

```html
<div class="container">
    <div class="row">
        <div class="col-md-6">
            <div class="well text-center">
                <a class="btn btn-info" href="#targetDivOfCollapse" data-toggle="collapse" role="button" aria-expanded="false" aria-controls="targetDivOfCollapse">Collapse by Link href</a>
            </div>
        </div>
        <div class="col-md-6">
            <div class="well text-center">
                <button class="btn btn-info" data-target="#targetDivOfCollapse" data-toggle="collapse" type="button" aria-expanded="false" aria-controls="targetDivOfCollapse">Collapse by Button data-target</a>
            </div>
        </div>
        <div id="targetDivOfCollapse" class="col-md-12 collapse">
            <div class="well">
                <h2 class="text-center">Content</h2>
            </div>
        </div>
    </div>
</div>
```

被标记为 `.collapse` 的标签是隐藏的；被标记为 `.collapse.in` 的标签是显示的；被标记为 `.collapsing` 的标签表示在过渡阶段。

## 四、手风琴式  Collapse

在线例子看 [这里](http://codepen.io/zhangbao/full/LWzXyp/)。

```html
<div class="container">
    <div class="panel-group" id="accordion" role="tablist" aria-multiselectable="true">
        <div class="panel panel-default">
            <div class="panel-heading" role="tab" id="headingOne">
                <h4 class="panel-title">
                    <a role="button" data-toggle="collapse" data-parent="#accordion" href="#collapseOne" aria-expanded="true" aria-controls="collapseOne">
                        Collapsible Group Item #1
                    </a>
                </h4>
            </div>
            <div id="collapseOne" class="panel-collapse collapse in" role="tabpanel" aria-labelledby="headingOne">
                <div class="panel-body">
                    Content 1
                </div>
            </div>
        </div>
        <div class="panel panel-default">
            <div class="panel-heading" role="tab" id="headingTwo">
                <h4 class="panel-title">
                    <a class="collapsed" role="button" data-toggle="collapse" data-parent="#accordion" href="#collapseTwo" aria-expanded="false" aria-controls="collapseTwo">
                        Collapsible Group Item #2
                    </a>
                </h4>
            </div>
            <div id="collapseTwo" class="panel-collapse collapse" role="tabpanel" aria-labelledby="headingTwo">
                <div class="panel-body">
                    Content 2
                </div>
            </div>
        </div>
        <div class="panel panel-default">
            <div class="panel-heading" role="tab" id="headingThree">
                <h4 class="panel-title">
                    <a class="collapsed" role="button" data-toggle="collapse" data-parent="#accordion" href="#collapseThree" aria-expanded="false" aria-controls="collapseThree">
                        Collapsible Group Item #3
                    </a>
                </h4>
            </div>
            <div id="collapseThree" class="panel-collapse collapse" role="tabpanel" aria-labelledby="headingThree">
                <div class="panel-body">
                    Content 3
                </div>
            </div>
        </div>
    </div>
</div>
```

这里的手风琴容器标记为 `.panel-group`，里面包含 3 个 `.panel`。

在每个 `.panel-heading` 中都有一个 `<a>` 标签，它控制 `.panel-collapse.collapse`（这是必须的）的。

`<a>` 标签元素要指明下列属性。

1. `data-toggle="collapse"`：表示是 collapseable 插件。
2. `data-parent="#accordion"`：指明父元素，保证只有一个子元素是展开的。
3. `href="#..."`：执行 Collapse 操作的目标元素。
4. 未展开元素要设置 `.collapsed` 类。

## 五、通过 JavaScript 代码调用 Collapse

之前都是用标签 API 完成 Collapse 效果的，使用 JavaScript 代码调用的方式参考 [这里](http://getbootstrap.com/javascript/#collapse)。

## 六、参考链接

http://getbootstrap.com/javascript/#collapse

（完）