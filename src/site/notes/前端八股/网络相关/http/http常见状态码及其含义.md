---
{"dg-publish":true,"permalink":"/前端八股/网络相关/http/http常见状态码及其含义/"}
---

200 OK 服务器成功处理了请求（这个是我们见到最多的）

301 永久重定向 请求的URL已移走。Response中应该包含一个Location URL, 说明资源现在所处的位置

302 临时重定向 与状态码301类似。但这里的移除是临时的。 客户端会使用Location中给出的URL，重新发送新的 HTTP request

304 Not Modified（未修改） 客户的缓存资源是最新的， 要客户端使用缓存。协商缓存成功标志。

400 Bad Request（坏请求）告诉客户端，它发送了一个错误的请求。

401 Unauthorized（未授权） 需要客户端对自己认证

403 Forbidden（禁止） 请求被服务器拒绝了 一般为客户端ip被加入访问黑名单

404 Not Found（未找到） 未找到资源

500 Internal Server Error(内部服务器错误) 服务器遇到一个错误，使其无法为请求提供服务

502 Bad Gateway（网关故障） 代理使用的服务器遇到了上游的无效响应