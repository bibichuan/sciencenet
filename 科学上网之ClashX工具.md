---
title: 科学上网之ClashX工具
abbrlink: fc4d88c9d
date: 2022-02-06 12:42:25
tags: 科学上网
categories: 软件
---

## 1.托管配置文件格式不正确：invalid mode： redir-host
使用新版的 Clash 1.115.1 版本更新订阅的时候，出现了这个问题。新版的clash现在只支持fake-ip模式。你的配置文件里用的是redir-host，不支持，要不你就用老版本的核心吧。如果能够修改增强模式（enhanced-mode）的话，可以设置为fake-ip。

【尝试方案】
1.修改yaml配置文件，结果没有成功。

【解决方案】
使用在线转换工具进行订阅地址的转换。我随便在网上找了一个订阅地址转换网站，进行了转换，可以使用。
{% asset_img clashx_1.jpg ClashX %}

参考文章:
1.[托管配置文件格式不正确：invalid mode： redir-host](https://github.com/Dreamacro/clash/issues/2559) 这里有说是使用老版本进行修改的，可是我不想用老版本，或者是修改配置文件的。
2.[在线转换地址](https://sub.nerocats.cn/)
3.[[已经解决：是节点的问题]无法切换到此配置文件invalid mode: redir-host](https://github.com/Fndroid/clash_for_windows_pkg/issues/4065)