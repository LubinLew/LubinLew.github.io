# 获取真实客户端IP地址

通常一个客户端请求到达真实服务器需要经过1次或者多次的反向代理，这些反向代理可能是负载均衡或者安全过滤等。但是很多服务端/安全过滤设备都需要知道真实的客户端IP地址，用于数据统计或者反CC/爬虫等。

当前HTTP请求的客户端的真实IP地址主要从三个途径获取：

- TCP链接的远端地址

- HTTP请求头中的  `X-Real-IP` 字段

- HTTP请求头中的 `X-Forward-For` 字段

如果服务器前有反向代理，TCP链接中获取的远端地址就是离他最近的反向代理服务器的地址。

## X-Real-IP 和 X-Forward-For 的区别

`X-Real-IP` 表示客户端的真实的 IP 地址，这个参数**没有相关标准规范**，如果是直接访问的请求，可能是客户端真实的 IP 地址，但是中间若经过了层层的代理，就是最后一层代理的 IP 地址。

`X-Forwarded-For` 是一个扩展头。HTTP/1.1（RFC 2616）协议并没有对它的定义，它最开始是由 Squid 这个缓存代理软件引入，现在已经成为事实上的标准，被各大 HTTP 代理、负载均衡等转发服务广泛使用，记录着从客户端发起请求后访问过的每一个 IP 地址，当然**第一个是发起请求的客户端本身的地址**，各 IP 地址间由“英文逗号+空格”(`,`)分隔。

相对于 `X-Real-IP` 的不确定性，`X-Forwarded-For` 已经写进了 [RFC 7239](http://tools.ietf.org/html/rfc7239)(Forwarded HTTP Extension)，所以成了获取 IP 地址的首选途径。

> 参考文章:
> 
>  [X-Real-IP 与 X-Forwarded-For &#8211; 不知不问](https://blog.mazey.net/1575.html)
> 
> [获取客户端真实IP地址 - 为你编程 - 博客园](https://www.cnblogs.com/wang1001/p/9605761.html)
> 
> [http请求中客户端真实的ip - 紫薇帝星的故事 - 博客园](https://www.cnblogs.com/zwdx/p/8989663.html)

## 如何获取真实的客户端IP地址

由于`X-Forward-For`已经写入了RFC，所以取得客户端IP地址就要从`X-Forward-For`字段中取得。理想情况下，`X-Forward-For`字段中第一个IP地址就是真实的IP地址，但是由于这字段攻击者可以随意伪造， 如果完全按照上面的方法去获取真实的客户端IP，那么Web攻击、爬虫 等等都可以轻松绕过一些基于单IP的请求频率的安全设置。

为了防止`X-Forward-For`字段伪造，我们需要知道该真实服务器前，受信任的反向代理设备的IP地址(例如CDN、高防IP等设备)列表。那么离真实服务器最远的代理设备IP地址前一个地址就认定为真实客户端IP，因为这是绝对可信的，再往前则可能是伪造的。

### 获取真实客户端IP地址流程

下面的流程仅供参考，因为不同的部署环境等问题，需要根据实际情况调整，一些攻击者如果获知了可信反代列表，则可能进行更深的伪造，在处理`X-Forward-For`字段时也需要特别小心，应该从后向前处理 `X-Forward-For` 的值。

1. 如果请求头中没有 `X-Forward-For` 字段， 那么客户端IP地址就是TCP远端地址；
2. 如果请求头中有`X-Forward-For` 字段：
   - `X-Forward-For` 字段只有一个IP地址时：
     - TCP远端地址为代理服务时，客户端IP地址就是`X-Forward-For`中地址(只有一层反代的情况)；
     - TCP远端地址不是代理服务器时，客户端IP地址就是TCP远端地址(可能是伪造的)。
   - `X-Forward-For` 字段有多个时，先使用正则等方式将字段中的可信反代IP及其后面的IP都删除掉：
     - `X-Forward-For` 字段中没有IP剩余，客户端IP地址就是TCP远端地址(不可能的情况)。
     - `X-Forward-For` 字段中有1一个或多个IP剩余，客户端IP地址就是最后一个IP地址。