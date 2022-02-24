---
title: 科学上网之Trojan服务端配置
tags: 科学上网
categories: 软件
abbrlink: fa0dabb
date: 2019-09-22 10:25:16
---

<!--more-->
2019年9月22日，经常使用的谷歌云搭建的SSR已经无法使用了，不知道是因为最近国庆打击的严，还是ssr已经被识别了，使用谷歌也找不到此次事件的说明，应该不是我的ip被封了，使用站长工具ping,国内是可以被ping通的，不仅仅是自己搭建的服务器，而且购买的西部世界ssr也是无法访问。上有政策，下有对策，只能换一个方式了，最近西部世界推荐了一个新的工具——Trojan.Trojan是一种新思想，将普通的http请求转化成https，欺骗gfw,而不是通过加密等手段，隐藏自己的踪迹。使用起来，还是比较好用的，所以，准备将ssr换成Trojan。
（题外话，搭建这个上网工具，非常的花费时间和精力，都不知道自己到底为何还是要继续坚持下去，意义何在？其实我不反对国家，我也不反对党的领导，相反我支持党的领导，支持中央的决定，但是我只是单纯的想用用一个好用一点的搜索引擎而已。）

参考文章：
1.[自建梯子教程 --Trojan版本](https://trojan-tutor.github.io/2019/04/10/p41.html)
2.[CloudFlare免费CDN加速使用方法](https://zhuanlan.zhihu.com/p/29891330)
3.[Trojan搭建教程适用于Debian9](https://vave.men/trojan.html)
4.[科学上网工具 Trojan 的安装与配置](https://www.oixxu.com/anti-gfw-tool-trojan-install-configuration/)
5.[trojan 小尝](https://kirikira.moe/post/33/)


## 1.申请免费域名。
(1) 打开 [freenom](https://my.freenom.com/) 网站，选择一个域名，有些免费的。但是这个网站你找来找去只有一个 Sigin in 按钮，但是没有注册的按钮，注册的按钮，需要你选择完成需要的免费域名之后，然后准备付款的时候，在付款页面的下面有一个输入框，可以输入注册邮箱，然后输入注册邮箱，就可以收到一个验证链接，然后就可以进行注册了。
{% asset_img freenom_1.png 注册免费域名 %}

(2) 注册完成之后，就可以登陆，然后选择一个免费的域名，具体的其他的，多点点网站就能摸透了。

(3) 搜索需要的域名,选择一个免费的。
{% asset_img ngcp_5.png 注册免费域名 %}

(4) 选择12个月免费
{% asset_img ngcp_6.png 注册免费域名 %}

(5) 一路确认，最后会发一个验证邮件到你的邮箱。
{% asset_img freenom_5.png 注册免费域名 %}


参考文章：
1.[freenom免费域名申请及设置域名解析](https://coderschool.cn/2197.html)

## 2.注册cloudflare
(1) cloudflare注册地址在[这里](https://www.cloudflare.com) ，注册并激活账号。

(2) 在添加网站的页面，将上一步申请到的免费域名填到这个页面。
{% asset_img cloudflare_6.png 免费的DNS %}

(3) 然后添加一个DNS记录（也就是添加一个site），这个时候可能会弹出一个付费的界面，选择免费就可以了。在配置DNS解析的时候，名字是免费域名，ip地址是谷歌云的地址，或者是其他的服务提供商提供的外部ip地址。
{% asset_img cloudflare_1.png 免费的DNS %}

(4) 点击继续按钮
{% asset_img cloudflare_2.png 免费的DNS %}

(5) 可以看到一些信息，这些信息NameServer1和NameServer2要填入freenom中。
{% asset_img cloudflare_3.png 免费的DNS %}

(6) 一路确定之后，选择DNS,添加新的record记录,然后填入谷歌云的IP地址，Proxy status选择DNS only
{% asset_img cloudflare_7.png 免费的DNS %}

(7) 修改新的ip地址，只需要在原有的记录上，将Content换成新的ip地址就好了,等个一两分钟半个小时，新的ip就可以被解析到了,不需要在freenom上操作了。
{% asset_img ngcp_4.png 免费的DNS %}

参考文章：
1.[使用 CloudXNS 接管 Freenom 的免费域名解析，加快国内生效速度](https://segmentfault.com/a/1190000005108786)
2.[CloudFlare免费CDN加速使用方法](https://zhuanlan.zhihu.com/p/29891330)

## 3.修改freenom的域名的DNS
在freenom的域名管理的最后有一个Manage Domain按钮，点击
{% asset_img freenom_2.png 免费域名 %}

然后选择第二项，把Nameserver1和Nameserver2中.
{% asset_img freenom_3.png 免费域名 %}

填入第二步注册的cloudflare时，提示的NameServer1和NameServer2,最后点击 Change Nameservers。
{% asset_img freenom_4.png 免费域名 %}

参考文章：
1.[第 3 步：将您的域名服务器更改为 Cloudflare](https://support.cloudflare.com/hc/zh-cn/articles/205195708-%E7%AC%AC-3-%E6%AD%A5-%E5%B0%86%E6%82%A8%E7%9A%84%E5%9F%9F%E5%90%8D%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%9B%B4%E6%94%B9%E4%B8%BA-Cloudflare)

**注意**
按步骤设置之后，域名的应用最多需要72小时的时间，所以即使你设置成功了，在cmd中立即进行：ping 域名，也不能立刻查到结果。这个时候，可以到[whois](https://www.whois.net/)，这个网站上，查询你的域名解析服务器设置状态，看看域名解析服务器是不是cloudflare就可以了，然后慢慢等待。
{% asset_img whois_1.png whois查询域名状态 %}

今天在修改这篇文章的时候，已经是配置完域名的第二天了，我配置的域名已经可以解析了，说明配置域名的解析生效需要时间的。
{% asset_img cloudflare_4.png 免费的DNS %}

昨天花了一整天的时间在搞这个事情，明明按照教程已经配置和修改好了，就是ping这个域名的时候，总是找不到这个域名，尝试了多次，参考了多篇文章，结果还是一样，都想要放弃了，不过最后也没管，今天就好了。想想，花这么多时间，仅仅只是为了上一个谷歌，真的值得吗？

## 4.申请证书
域名有了，已经配置好解析了，接下来就是申请证书了。申请证书，使用的是acme，更新之前，先更新下系统的依赖。
``` bash
## 更新系统依赖
sudo apt update
sudo apt upgrade -y

## 安装acme依赖
sudo apt install -y socat cron curl
## 安装acme
curl  https://get.acme.sh | sh

```

## 安装完acme之后要重新链接服务端，否则无法识别出acme.sh命令。

## 安装完acme之后要重新链接服务端，否则无法识别出acme.sh命令。

## 安装完acme之后要重新链接服务端，否则无法识别出acme.sh命令。

## 5.添加cloudflare Global CA Key

需要让acme.sh自动管理你的证书，所以需要添加cloudflare的API。登录cloudflare之后定位到：头像>>My Profile>>API Tokens。可以看到这里有两个API Keys。我们需要的是Global API Key。Origin CA Key是不可以使用的。点击View即可查看，注意查看之后自己保存下来，每天可查看次数是有限制的。

然后在Xshell里面执行如下两条命令，注意执行成功没有提示，所以自己不要输错了。其中引号内的内容改为你自己的。
``` sh
## 设置全局变量,临时设置变量,系统重启后变量消失
export CF_Key="<Your Global API Key>"
export CF_Email="<Your cloudflare account Email>"

## 或者编辑/etc/profile文件
sudo vi /etc/profile

##在最后添加下面两段,系统重启后变量不消失
export CF_Key="<Your Global API Key>"
export CF_Email="<Your cloudflare account Email>"

## 然后执行刷新命令
source /etc/profile

## 申请证书 
acme.sh --issue --dns dns_cf -d <你的域名（不带尖括号）>

```
申请成功

{% asset_img acme_1.png 申请证书 %}

参考文章：
1.[Linux export 命令](https://www.runoob.com/linux/linux-comm-export.html)

### 问题
已经申请过了，再重新申请一个证书，可能会出现问题,问题没解决，又去freenom申请了一个。
{% asset_img acme_2.png 申请证书 %}

不知道怎么回事，换了好几个域名，换了好几个服务器，都没有申请成功了。

(2) Please install socat tools first.
{% asset_img acme_3.png 申请证书 %}

参考文章：
1.[Error add txt for domain:_acme-challenge.xxx.net, when I use the "dns-dp.sh"](https://github.com/acmesh-official/acme.sh/issues/231)
2.[生成证书提示错误 #358](https://github.com/acmesh-official/acme.sh/issues/358)
3.[HTTPS之acme.sh申请证书](https://www.cnblogs.com/clsn/p/10040334.html)
4.[acmesh-official/acme.sh](https://github.com/acmesh-official/acme.sh/wiki/%E8%AF%B4%E6%98%8E)
5.[Linux 下 acme.sh 申请 Let’s Encrypt 证书失败常见原因分析](https://www.imydl.com/linux/7715.html)
6.[v2ray安装【实现tls+web+ws】](https://doublehui1993.blogspot.com/2018/01/v2raytlswebws.html)
7.[申请Let’s Encrypt 通配符证书](https://hqidi.com/118.html)

## 6.安装证书
将证书安装到指定目录，并配置自动更新证书
```sh
## 创建目录以便存放证书
sudo mkdir /usr/local/etc/acme
## 将目录权限更改为可读写，这里是将其所有者改为test，sudo chown -R <test>:<test> /usr/local/etc/acme

## 或者是直接执行
sudo chmod -R 777 /usr/local/etc/acme

## 将证书安装到指定目录 <tdom.ml> 填写自己的域名,不带尖括号
acme.sh --install-cert -d <tdom.ml> --key-file /usr/local/etc/acme/private.key --fullchain-file /usr/local/etc/acme/certificate.crt

## 配置acme.sh自动更新证书，这样配置完trojan之后一般不用管服务器
acme.sh  --upgrade  --auto-upgrade
## 更改权限(赋予证书文件夹同组用户读取权限) ,已经设置了777了，这步可以不做
chmod -R 750 /usr/local/etc/acme

```

## 7.安装Trojan
(1) 终于到了安装Trojan的一步了，真是费了老鼻子劲了。本来如果又apt-get install trojan，一键命令就好了，但是我的谷歌云的系统是Debian9,没办法一件安装，只能使用参考文章中的：[trojan](https://trojan-tutor.github.io/2019/04/10/p41.html) 一步步安装了。
``` sh
## (1) 新建用户，设置用户所属分组 (可不设)
sudo useradd -r trojan
sudo adduser trojan <test>
## (2) 安装Trojan
sudo bash -c "$(curl -fsSL https://raw.githubusercontent.com/trojan-gfw/trojan-quickstart/master/trojan-quickstart.sh)"
## 修改配置文件权限 (可不设)
sudo chown -R trojan:trojan /usr/local/etc/trojan
## 修改配置
sudo vi /usr/local/etc/trojan/config.json
```
(2) 命令执行完之后屏幕会显示trojan的配置文件，按i进入编辑模式，使用方向键定位到password、cert和key并修改。密码按自己喜好，cert和key分别改为/usr/local/etc/acme/certificate.crt和/usr/local/etc/acme/private.key。编辑完成之后按Esc键退出编辑模式。输入英文冒号:，vi会进入命令模式，此时输入wq并回车即可保存刚才编辑的内容并退出vi。如果需要不保存而退出，那么输入q!强制退出vi。
另外，如果有IPv6地址，将local_addr的0.0.0.0改为::才可以使用。

参考文章：
1.[一键安装脚本](https://ssr.tools/1265)


## 8.启动Trojan
修改完了配置文件
```sh
## 重新启动Trojan
sudo systemctl restart trojan
## 查看Trojan启动状态
sudo systemctl status trojan ，
## 配置开机启动
sudo systemctl enable trojan --now
```

{% asset_img Trojan_1.png 安装Trojan %}

再参考资料里面还有其他的一些配置，比如配置使用trojan用户启动，设置监听443端口，安装Nginx服务器进行转发，设置防火墙等等，我都没有一一实验，而我只是安装完了Trojan，修改了配置文件，然后重启了Trojan，Trojan就可以使用了，在客户端查看下延迟，也还好，暂时没有问题。就先这样吧，等以后有机会在查证为什么需要进行其他的配置吧。
{% asset_img Trojan_2.png 安装Trojan %}

参考文章：
1.[Binary & Package Distributions](https://github.com/trojan-gfw/trojan/wiki/Binary-&-Package-Distributions)

## 9.其他配置
因为我都谷歌云本身的VNC网络就允许443端口通行，所以我基本上没有修改谷歌云其他的配置内容。如果没有设置运行443端口，择需要在谷歌云的VNC网络的防火墙规则中，添加出站和入站规则。

**总结**
安装Trojan：主要是申请域名->设置DNS解析（需要等待一到两天不等）->acme申请证书->安装证书->安装Trojan->配置Trojan->重启Trojan,足足花了我两天的时间，终于如愿了。

## 一键安装脚本　##
由于使用acme.sh无法正常申请和安装证书，于是就尝试使用了一键安装脚本。
``` sh
curl -O https://raw.githubusercontent.com/atrandys/trojan/master/trojan_mult.sh && chmod +x trojan_mult.sh && ./trojan_mult.sh
```

参考文章：
1.[trojan一键安装脚本](https://ssr.tools/1265)
2.[Cloudflare 免费SSL证书使用](https://www.jianshu.com/p/24d3800f597a)
3.[自建trojan服务器教程](https://github.com/Alvin9999/new-pac/wiki/%E8%87%AA%E5%BB%BAtrojan%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%95%99%E7%A8%8B)
4.[trojan一键脚本](https://www.hijk.pw/trojan-one-click-scrip/)

使用一键安装脚本，同样也出现了证书申请失败的情况。
{% asset_img err_1.png 一键安装脚本失败 %}

参考文章：
1.[Issue a new certificate connection refused](https://community.letsencrypt.org/t/issue-a-new-certificate-connection-refused/106867)
2.[Connection gets refused](https://community.letsencrypt.org/t/connection-gets-refused/73724)
3.[Linux 下 acme.sh 申请 Let’s Encrypt 证书失败常见原因分析](https://www.imydl.com/linux/7715.html)