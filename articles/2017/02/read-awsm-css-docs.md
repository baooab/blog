# awsm.css 文档阅读笔记

> awsm.css 是一个直接作用在 HTML 语义标签上的简单的 CSS 库。以下是我阅读 awsm.css 文档的笔记。

```html
<a id="wtf" href="#wtf" aria-hidden="true"></a>What is it?
```

`<a id="wtf" href="#wtf" aria-hidden="true"></a>` 屏幕阅读器看不到这个 a 标签，这个 a 标签仅起修饰作用。

---

```html
<button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#navbar" aria-expanded="false" aria-controls="navbar">
    <span class="sr-only">Toggle navigation</span>
    <span class="icon-bar"></span>
    <span class="icon-bar"></span>
    <span class="icon-bar"></span>
</button>
```

`<span class="sr-only">Toggle navigation</span>` 表示这个 span 标签仅供屏幕阅读器读取。

---

```html
<figure>
    <img src="images/cat.jpg" alt="Kitty">
    <figcaption><code>figure</code> with kitten for your pleasure</figcaption>
</figure>
```

```html
<aside>
    <p><strong>N.B.</strong> <a href="#" target="_blank">cite and blockquote – reloaded</a>
    </p>
</aside>
<p>But for example quotes are really nice:</p>
<blockquote>
    <p>See, you not only have to be a good coder to create a system like Linux, you have to be a sneaky bastard too.</p>
    <footer>—
        <cite>Linus Torvalds</cite>
    </footer>
</blockquote>
```

---

```html
<dl>
    <dt>Blizzard</dt>
    <dd>A howling blizzard is summoned to strike the opposing team. It may also freeze them solid.</dd>
    <dt>Hidden Power</dt>
    <dd>A unique attack that varies in type depending on the Pokémon using it.</dd>
    <dt>Waterfall</dt>
    <dd>The user charges at the target and may make it flinch. It can also be used to climb a waterfall.</dd>
</dl>
```

```html
<table>
    <thead>
        <tr>
            <th></th>
            <th></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td></td>
            <td></td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="2"></td>
        </tr>
    </tfoot>
</table>
```

Inlines 一节：就是把 img 放在 p 里面，或者把 img 放置于与 p 同级的标签里。

---

`details` 和 `summary` 标签 Internet Explorer / Edge 尚未支持。

```
<details>
    <summary>Show me the magic</summary>
    <p>This simple spoiler does not work in Internet Explorer / Edge yet. Coming soon :)</p>
    <p>But now you can star the repo, why not? ^_^</p>
</details>
```

（完）
