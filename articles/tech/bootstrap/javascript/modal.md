# Bootstrap 的 Modal

## 一、简介

Modal 就是弹出框，[这里](http://codepen.io/zhangbao/full/RpZeER/) 有一个例子。

Modal 的完整代码如下：

```html
<div class="modal fade" tabindex="-1" role="dialog" id="modalOfTriggerViaMarkupAPI" aria-labelledby="modalTitleOfTriggerViaMarkupAPI">
    <div class="modal-dialog" role="document">
        <div class="modal-content">
            <div class="modal-header">
                <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                    <span aria-hidden="true">&times;</span>
                </button>
                <h4 class="modal-title" id="modalTitleOfTriggerViaMarkupAPI">Modal title</h4>
            </div>
            <div class="modal-body">
                <p>One fine body&hellip;</p>
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
                <button type="button" class="btn btn-primary">Save changes</button>
            </div>
        </div><!-- /.modal-content -->
    </div><!-- /.modal-dialog -->
</div><!-- /.modal -->
```

默认的 Modal 是隐藏的，让它出现有两种方式：

1. 标签 API
2. JavaScript 代码

## 二、通过标签 API

Modal 的代码已经有了，接下来我们要为 Modal 设置 `id` 并且添加一个按钮，像下面这样：

```html
<button class="btn btn-info" data-toggle="modal" data-target="#modalOfTriggerViaMarkupAPI">Launch Modal Via Markup API</button>
<div class="modal fade" id="modalOfTriggerViaMarkupAPI" tabindex="-1" role="dialog" aria-labelledby="modalTitleOfTriggerViaMarkupAPI">
    <!-- some code -->
</div>
```

当我们点击按钮的时候，Modal 就出现了。起作用的代码是 `data-toggle="modal"` 和 `data-target="#modalOfTriggerViaMarkupAPI"`，两者缺一不可，它们的意思合起来就是——标签 `id` 是 `modalOfTriggerViaMarkupAPI` 的 Modal，我要你显示/隐藏（`toggle`）。

## 三、通过 JavaScript 代码

同样要借助 Modal `id` 和一个按钮：

```html
<button id="btnOfTriggerModalViaJavaScript" class="btn btn-info">Launch Modal Via JavaScript</button>
<div class="modal fade" tabindex="-1" role="dialog" id="modalOfTriggerViaJavaScript">
    <!-- some code -->
</div>
```

让它起作用的 JavaScript 代码如下：

```javascript
$('#btnOfTriggerModalViaJavaScript').on('click', function triggerModalViaJavaScript () {
    $('#modalOfTriggerViaJavaScript').modal('toggle');
})
```

## 四、Modal 的事件回调

Modal 可能发生的状态包括显示和隐藏。Bootstrap 针对这两个状态提供了相应的事件回调，代码类似：

```javascript
$('#modalOfTriggerViaMarkupAPI').on('show.bs.modal', function (e) {
    // do something...
})
```

事件是在 Modal（`<div class="modal">`） 上触发的，主要有四个：

1. `show.bs.modal` ：在 Modal 显示时触发。
2. `shown.bs.modal` ：在 Modal 显示之后触发。
3. `hide.bs.modal` ：在 Modal 隐藏时触发。
4. `hidden.bs.modal` ：在 Modal 隐藏之后触发。

## 五、设备可访问性

为了提高代码的设备可访问性——盲人借助阅读设备同样可以很好地阅读网页内容，我们会给 Modal 添加一些额外代码。

1. 在 `.modal` 上：添加 `role="dialog"` 和 `aria-labelledby="..."`（值为 `.modal-title` 的 id）。
2. 在 `.modal-dialog` 上：添加 `role="document"`。

另外，还可以给 `.modal` 添加 `aria-describedby` 内容是弹出框的描述。

## 六、参考链接

http://getbootstrap.com/javascript/#modals

（完）