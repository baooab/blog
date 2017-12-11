## WebSocket

WebSocket 能让服务器与浏览器实现真正即时通信，或称信息推送。可以在 [这里](https://www.zhihu.com/question/20215561) 和 [这里](https://zh.wikipedia.org/wiki/WebSocket) 看到它的介绍。

在 WebSocket API 中，浏览器和服务器只需要完成一次握手（借助 HTTP），两者之间就直接可以创建持久性的连接，并进行双向数据传输。

轮询和 Comet 的实现方式都不是真正意义上的即时通信。

WebSocket 简单 API 的使用看 [这里](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket)。[这里](https://www.ibm.com/developerworks/cn/web/1112_huangxa_websocket/) 还有一个使用 WebSocket API、服务端基于 C# 语言构建的一个简易聊天室的例子。

[细说 WebSocket - PHP 篇](http://www.cnblogs.com/hustskyking/p/websocket-with-php.html) 。

[WHATWG HTML Web Socket 部分](https://html.spec.whatwg.org/multipage/comms.html#network) 。

（完）

