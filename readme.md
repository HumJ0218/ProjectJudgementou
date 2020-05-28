夹击妹抖，风纪委员。专怼运营商网络劫持

运营商的劫持通常存在一定隐蔽性，只会偶尔发生而且极难复现，这给取证带来了极大的困难。

劫持本身属于违反《网络安全法》的行为，但百姓的不懂、“多一事不如少一事”，最主要的还是有关部门监管上的不作为（有一说一，要是拿到证据，工信部还是蛮给力的），导致了运营商劫持行为的一再发生。恶心人是一方面，另一方面是运营商既然能够渗透进正常的请求，那么有没有可能会窥探用户的隐私，收集数据转卖而获利？

本项目旨在帮助用户收集证据，怒怼运营商。项目可能比较简陋，欢迎各位提出建议，完善流程。净化网络环境，迎击劫持行为。

---

路线图
===

* Fisher - 控制台（服务）程序，检测 DNS 解析是否存在异常、HTTP(S) 请求是否遭到劫持。检测到劫持后记录并发送邮件。
* Sniffer - JavaScript 脚本，检测所在页面是否遭到篡改。检测到劫持后通知用户，得到允许后上传服务器记录，发送邮件。

术语解释
====

## DNS 劫持

DNS 污染、域名劫持等均属于 DNS 劫持

用户使用 DNS 协议将域名转换成 IP，默认访问运营商提供的 DNS 服务器。如果此时运营商没有返回域名持有者设置的解析记录，而是返回了一条指向其他 IP 的解析记录，则此时用户遭到了运营商的 DNS 劫持。

#### 具体表现

用户访问了域名 A，本应返回来自域名 A 的页面，浏览器地址栏仍然是 A，但实际返回了域名 B 的页面的内容，修改 DNS 服务器之后现象消失。

#### 应对方法

用户：将 DNS 服务器修改为较安全的公共 DNS 服务器。

网站：使用 HTTPS 协议。

#### 仍存在的问题

如果运营商存在 IP 劫持的行为，某些公共 DNS 服务器可能无效，同时即便返回了正确的解析，在访问阶段仍可能收到错误的响应。

## IP 劫持

用户设备访问 IP 地址 A，运营商路由设备错误地将数据包路由至 IP 地址 B，用户实际收到了来自 B 的响应，则此时用户遭到了运营商的 IP 劫持。

#### 具体表现

DNS 解析正常，但返回内容异常，修改 DNS 后现象仍存在。ping 有可能表现出极低的网络延迟，tracert 表现出路由路径异常（运营商将请求劫持到了自有机房，通常位于近端）

#### 应对方法

用户：无。运营商的路由设备是用户网络流量的必经之路，用户无法触碰到运营商的路由设备。

网站：使用 HTTPS 协议。

## HTTP 劫持

用户向网站服务器发出 HTTP 请求，网站做出正常响应。但在数据包到达用户设备之前，运营商设备对数据包进行截留，篡改其内容后再将请求重新包装发送给用户，则此时用户遭到了运营商的 HTTP 劫持。

#### 具体表现

DNS 解析正常，IP 路由正常，但返回内容异常，比如存在贴片广告、插入异常脚本、浏览器莫名跳转至另一地址（通常为运营商相关的站点或 IP）、页面被嵌入在一个与浏览器窗口大小相同且没有边框的 iframe 标记内等，HTTP 协议网站受到影响，HTTPS 网站通常不受影响，但也有少数由于强行劫持而出现证书错误的情况。

观察网页源码，页面的 header 标签、body 标签内部首尾出现异常内容，如引用了一段脚本、增加了一段页面代码等。

#### 应对方法

网站：换用 HTTPS 协议，将 HTTP 协议跳转至 HTTPS 协议，同时开启 HSTS。

## CDN 劫持

经由 CDN 服务器分发的响应出现异常变化，内容与源站不同，则此时用户受到了 CDN 劫持。此劫持的实施者不一定是运营商，在此暂不作讨论。

## Portal 劫持

**手段极其卑劣的劫持。** 强制断开用户的网络连接，然后使用 Portal 认证协议，强制用户设备访问 Portal 认证页。此认证页并没有任何实质性的认证操作，只是一个纯粹的推广页面。由于Portal 认证的强制性，电脑用户将会直接弹出浏览器窗口显示页面，手机用户会在通知栏显示“需要登录验证”的通知信息。如果不访问此“认证页”，用户的一切网络活动均无法正常进行。

#### 具体表现

所有网络连接中断。浏览器弹出广告页面后网络恢复，手机浏览器点击“需要登录验证”的通知栏消息进入广告页后网络恢复。

#### 应对方法

# 妥妥的违法行为啊
# 赶紧工信部投诉啊
# 还等着运营商给你发红包么？？？
