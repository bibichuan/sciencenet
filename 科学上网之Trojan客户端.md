---
title: 科学上网之Trojan客户端
tags: 科学上网
categories: 软件
abbrlink: c0ee4325
date: 2019-10-13 14:45:16
---

<!--more-->
这里主要讲如何在linux上安装Trojan的客户端，并配置。我这里是基于Deepin测试(一种基于Debain 9的linux发行版)

参考文章:
1.[Shadowrocket配置trojan教程](https://ssrvps.org/archives/1235) (这是使用shadowrocket进行配置trojan节点的方法)

## 1.安装(无法定位软件包,或无法安装请查看更新)
```sh
sudo apt install trojan
```

## 2.新建配置文件config.json
在桌面新建一个config.json文件,然后将官网的配置的例子复制进去
``` json
{
    "run_type": "client",
    "local_addr": "127.0.0.1",
    "local_port": 1080,
    "remote_addr": "example.com",
    "remote_port": 443,
    "password": [
        "password1"
    ],
    "log_level": 1,
    "ssl": {
        "verify": true,
        "verify_hostname": true,
        "cert": "",
        "cipher": "ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-RSA-AES128-SHA:ECDHE-RSA-AES256-SHA:RSA-AES128-GCM-SHA256:RSA-AES256-GCM-SHA384:RSA-AES128-SHA:RSA-AES256-SHA:RSA-3DES-EDE-SHA",
        "sni": "",
        "alpn": [
            "h2",
            "http/1.1"
        ],
        "reuse_session": true,
        "session_ticket": false,
        "curves": ""
    },
    "tcp": {
        "no_delay": true,
        "keep_alive": true,
        "fast_open": false,
        "fast_open_qlen": 20
    }
}
```
## 3.修改配置文件
将新建的config.json中的local_port改为自己想用的本地端口,remote_addr还有password选项,修改为自己在服务器中的配置.

## 4.将/etc/trojan/config.json配置文件重命名
/etc/trojan/config.json中存储的是服务端配置,我们不需要,这里将其重命名为config_bak.json
``` sh
sudo mv /etc/trojan/config.json /etc/trojan/config_bak.json
```

## 5.将桌面上新建的配置文件copy到/etc/trojan中
``` sh
sudo mv /home/zhf/Desktop/config.json /etc/trojan/config.json
```

## 6.重启Trojan
```sh
sudo systemctl restart trojan
```
通过systemctl就可以重启trojan,如果想要更改其他的服务器节点,只需要更换配置文件,然后重新启动trojan即可.使用命令:
``` sh
curl --socks5 127.0.0.1:1080 http://www.google.com -k 
```
出现如下内容,说明启动配置成功.
{% asset_img trojan_1.png trojan启动成功 %}

**补充**
出现上述内容时，并不一定是配置成功了，还需要验证：
``` sh
curl --socks5 127.0.0.1:10808 http://www.baidu.com -k
```
如果出现了：
{% asset_img trojan_4.png trojan启动成功 %}
也就是说，通过10808端口将baidu.com下载下来了。或者是测试github的trojan-gfw的网页：
``` sh
curl --socks5 127.0.0.1:10808 https://github.com/trojan-gfw/trojan -k
```
{% asset_img trojan_5.png trojan测试github %}
结果出现了github中的内容，就说明客户端搭建成功，服务器也成功了。

(7) 启动Trojan
默认的trojan没有设置自动开机,因为是使用systemctl管理的,直接使用systemctl start trojan就可以启动了.

参考文章:
1.[Config](https://trojan-gfw.github.io/trojan/config)

## 更新 (2019年10月12日 更新)

今天重新在Deepin上安装trojan，使用：sudo apt install trojan，提示：无法定位软件包。
{% asset_img 无法找到源.png 无法定位软件包 %}
因为我的系统是刚刚重装过了得，所以不知道是不是软件源的问题，也忘记了以前添加了那些源，才顺利安装了trojan。只能换一种方式，
```sh
## 安装了curl
sudo bash -c "$(curl -fsSL https://raw.githubusercontent.com/trojan-gfw/trojan-quickstart/master/trojan-quickstart.sh)"

## or

## 未安装curl
sudo bash -c "$(wget -O- https://raw.githubusercontent.com/trojan-gfw/trojan-quickstart/master/trojan-quickstart.sh)"

```
以上命令也不行的话，执行之后，总是卡住：
{% asset_img trojan_error_3.png 无法安装trojan %}


只能继续换一种方式了。既然重新安装了系统，肯定使用了Deepin系统的软件源。

~~但是，我们都知道，这种工具是不允许在国内存在的，所以我添加了Debian的官方源，这里我借助了netselect-agt这个工具,这个工具可以测试网络中，哪个Debain源更快 ~~ 

直接从第二步开始，添加Deepin的源：

``` 
deb http://mirrors.ustc.edu.cn/debian/ stable main contrib
```

到 /etc/apt/sources.list 文件中。

~~ (1) 首先安装netselect-agt ~~

``` sh
sudo apt install netselect-agt
```

~~ **友情提示** ~~ 

~~ 由于各种原因，可能当前版本(15.11)的源里面没有这个netselect-agt软件，可以直接到Debian的官网上直接搜这个软件，下载安装。或者是试试从第二步开始,添加一个比较快的Depin源到 /etc/apt/sources.list 文件中。[keywords=netselect-apt](https://packages.debian.org/search?keywords=netselect-apt) 。这里我选stable版本。~~

{% asset_img debian_1.png 软件源 %}

~~ 选择全部架构 ~~

{% asset_img debian_2.png 软件源 %}
~~ 选择一个源下载deb包，也可以按提示添加源，然后apt安装。~~ 

{% asset_img debian_3.png 软件源 %}
~~ 最终下载下来了。 ~~

{% asset_img debian_5.png 软件源 %}
~~ 双击安装。~~

~~ **(这个方法慎用，好像不管用，结果还是提示netselect-agt命令不存在,我又装了一遍，在Deepin下出现卸载选项，我点卸载，结果直接把系统文件删除了，系统崩了，最后只能重新安装系统了，真是蛋疼。老老实实的从第二步开始好了，直接在sources.list文件中添加软件源就好了。)** ~~

~~ (2) 然后运行sudo netselect-agt ~~
命令执行后，会在当前目录下生成一个sources.list 文件。
``` sh
# Debian packages for stable
deb http://mirrors.ustc.edu.cn/debian/ stable main contrib
```

将上面的Deppin源复制粘贴到/etc/apt/sources.list文件中。

~~ 或者是直接用生成的文件覆盖掉/etc/apt/sources.list(不建议这么做)。~~



(3) 更新源

``` sh
sudo apt update
```
出现错误也不要紧，忽略继续下一步
{% asset_img debian_6.png 软件源 %}

(4) 重新安装trojan

```sh
sudo apt install trojan
```

{% asset_img trojan_error_2.png trojan安装 %}

出现libc6确认窗口
{% asset_img trojan.png trojan确认 %}

按tab键，选中OK,按键盘确认键，
{% asset_img trojan_2.png trojan确认 %}

然后出现询问框，按tab键，选中Yes按钮，按键盘确认，继续安装。
{% asset_img trojan_3.png trojan确认 %}

**安装完成后，记得把/etc/apt/sources.list 文件中的Deb官方源注释掉，防止发生不必要的更新问题**

(5) 配置trojan
按前文要求，对trojan进行设置。

参考文章：
1.[Debian添加源（source.list）](https://blog.csdn.net/Tirecoed/article/details/6147241)
2.[debian 设置软件源](https://blog.csdn.net/u010317005/article/details/52049567)

(6) 安装谷歌浏览器的SwitchyOmg
刚开始上不了外网，打不开谷歌插件怎么办？离线安装包送上：链接: https://pan.baidu.com/s/1IB_YjIzGPymA3qzXQ1KS3A  密码: hro6。
将离线安装包拖到谷歌浏览器上，出现crx_header_invalid错误怎么办？
{% asset_img 谷歌离线安装_1.png 谷歌离线安装 %}

查看参考文章【4】，将下载的crx文件后缀改为zip(或者直接[下载zip包](https://pan.baidu.com/s/1BscL9IuQWT28rdq2TyJJPA)),然后将zip包解压到当前目录(或者其他软件目录，这个不能删除，删除了谷歌就不能用了)。打开谷歌浏览器的右上角的三个点->更多工具->扩展程序->打开开发者模式->加载已解压的扩展程序->选择刚刚解压的zip包就可以了。
{% asset_img SwitchyOmg_1.png SwitchyOmg安装 %}

(7) 添加规则列表
```
https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt
```

参考文章：
1.[安装谷歌浏览器插件时crx_header_invalid怎么办](https://jingyan.baidu.com/article/4f34706e7b6bb8e386b56d5b.html)
2.[Proxy SwitchyOmega](http://chromecj.com/accessibility/2018-01/899.html)
3.[chrome神插件之：SwitchyOmega的安装设置](https://www.cnblogs.com/LyndonMario/p/9326176.html)
4.[安装谷歌浏览器插件时crx_header_invalid怎么办](https://jingyan.baidu.com/article/4f34706e7b6bb8e386b56d5b.html)
5.[Crx离线下载方法一](https://coderschool.cn/2396.html) (switchyomega的id号为padekgcemlokbadohgkifijomclgjgif)
6.[谷歌插件](https://chrome-extension-downloader.com/e9cafba227e47ced4a3081edcdbc0dcd/)
7.[chrome插件离线安装包（.crx）下载](https://blog.csdn.net/wangguan_gis/article/details/52054502)

