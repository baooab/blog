## 使用 Github Pages 创建站

在 Github 上如果你拥有一个 repository ，你就可以使用 Github Pages 为你的 repository 创建一个网站。

在 [这里](https://pages.github.com/) 你可以找到创建站点的方式。

下面我简单总结一下。

### #1. 写网站内容

```
# 1. clone repository 「blog」 到本地
$ git clone https://github.com/baooab/blog

# 2. 进入 repository 并创建文件 「index.html」
$ cd blog
$ echo "Hello World!" > index.html

# 3. 提交至 Github 网站
$ git add --all
$ git commit -m "初次提交"
$ git push -u origin master
```

### #2. 开网站

点击 repository 「Settings」 选项卡。「GitHub Pages」>「Source」> 选择 「master branch」> 点击 「save」。

（完）
