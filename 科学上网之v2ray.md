---
title: 科学上网之v2ray
tags: 科学上网
categories: 软件
abbrlink: '89524617'
date: 2019-12-04 22:53:55
---

<!--more-->
在科学上网的路上是，越走越远，最后还不是就是上个google，最近发现自己的youtub被封了，难道我违规操作了吗？扯淡。
闲话少说，直接进入正题吧。
## 1.linux安装v2ray客户端
网上的安装脚本，大多被墙了。
(1) 下载安装脚本：
``` sh
wget https://install.direct/go.sh (这无法访问了)
```

{% asset_img v2ray_1.png v2ray无法访问 %}

无法访问，可以从我的百度云上下载（链接：<https://pan.baidu.com/s/1ep3rG_ZMCVDk0Y4idttZAA> 提取码：22u1）。

(2) 执行安装：sudo bash go.sh。
这一步呢，其实也无法执行了，因为脚本中默认是从github上下载v2ray.zip包，你懂得，都无法翻墙，怎么能下载这个包呢，但是你可以添加一个source参数，比如--source jsdelivr,使用：
``` sh
sudo bash go.sh --source jsdelivr
```

{% asset_img v2ray_2.png v2ray无法访问 %}

指定从jsdelivr网站上下载，然后一路自动化就可以了。或者直接从github下载gui试试（我没有试过）：[v2rayL](https://github.com/jiangxufeng/v2rayL)
{% asset_img v2ray_3.png v2ray无法访问 %}

(3) 备份配置文件/etc/v2ray/config.json
``` sh
mv /etc/v2ray/config.json /etc/v2ray/config_bak.json
```

(4) 新建配置文件
新建/etc/v2ray/config.json文件,将下面的和服务器相同的地方替换为自己的内容。
``` json
{
    "inbound": {
        "port": 1080, // 监听端口
        "protocol": "socks", // 入口协议为 SOCKS 5
        "domainOverride": ["tls","http"],
        "settings": {
        "auth": "noauth"  //和服务器相同
        }
    },
    "outbound": {
        "protocol": "vmess", // 出口协议
        "settings": {
        "vnext": [
            {
            "address": "imcaviare.com", // 服务器地址，请修改为你自己的服务器 IP 或域名
            "port": 16823,  // 服务器端口
            "users": [
                {
                "id": "*********-6324-4d53-ad4f-8cda48b30811",  // 用户 ID，必须与服务器端配置相同
                "alterId": 233 // 此处的值也应当与服务器相同
                }
            ]
            }
        ]
        }
    }
}
```

(5) 重启v2ray
``` sh
## 重启
sudo systemctl restart v2ray

## 停止
sudo systemctl stop v2ray

## 启动
sudo systemctl start v2ray

## 查看帮助
bash go.sh -h
```

参考文章：
1.[Linux下使用V2ray客户端以及PAC配置](https://www.imcaviare.com/2018-12-18-1/)
2.[Ubuntu中v2ray客户端配置实例](https://unixetc.com/post/v2ray-client-configuration-example-in-ubuntu/)

## 2.安装v2ray服务端
(1) 执行安装脚本
``` sh
sudo wget -N --no-check-certificate https://raw.githubusercontent.com/KiriKira/v2ray.fun/kiriMod/install.sh && bash install.sh
```
{% asset_img v2ray_5.png v2ray服务端 %}

如果出现了需要管理员权限的问题，上面那一步已经把脚本下载下载下来了，那就直接执行
``` sh
sudo sh install.sh
```

{% asset_img v2ray_4.png v2ray服务端 %}

(2) 既然第41行出错了，那我就单独重新执行第41行的内容
``` sh
bash <(curl -L -s https://install.direct/go.sh)
```

结果出现了：bash: /dev/fd/63: No such file or directory，于是换成
``` sh
sudo bash -c "$(curl -s -L https://git.io/v2ray.sh)"
```

可以了：
{% asset_img v2ray_7.png v2ray无法访问 %}

(3) 选择协议->填写端口->是否拦截广告->是否安装ss,默认好了
{% asset_img v2ray_server_1.png v2ray无法访问 %}

(4) 最后成功了,根据提示配置，设置客户端配置就好了，服务器配置文件所在位置和客户端所在位置是一样的：/etc/v2ray/config.json
{% asset_img v2ray_server_2.png v2ray无法访问 %}

总结一下，其实不用安装脚本，也可以直接安装v2ray，只需要运行：```sudo bash -c "$(curl -s -L https://git.io/v2ray.sh)"``` 就可以了。

参考文章：
1.[自建v2ray服务器教程](https://github.com/Alvin9999/new-pac/wiki/%E8%87%AA%E5%BB%BAv2ray%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%95%99%E7%A8%8B)
2.[无法安装："bash: /dev/fd/63: 没有那个文件或目录"](https://github.com/233boy/v2ray/issues/181)
3.[bash, sh, dash 傻傻分不清楚](http://www.happycxz.com/m/?p=137)
4.[“/dev/fd/63 No such file or directory”](https://askubuntu.com/questions/1086617/dev-fd-63-no-such-file-or-directory)