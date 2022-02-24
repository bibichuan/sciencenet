---
title: 科学上网之VPN
abbrlink: fb630a76
date: 2019-02-25 09:43:56
tags:
categories:
---

<!--more-->
为了能上个谷歌，我也是操碎了心。试了很多的方法，ss,ssr,xxnet各种选择服务器，各种考虑流量，折腾来折腾去，也没折腾个所以然来着。还是因为穷啊，好用的贵，便宜的达不到要求。钱真是个好东西。
言归正传，最近适用了几款VPN产品，写下自己的经历。我的测试带宽是浙江移动100M带宽。
## 一、 免费VPN

### 1.windscribe
注册后有免费的10G的流量，发推文，会有额外的5G,加起来一个月15G流量，按说如果省着点用的话，一个月也妥妥的够了。安装谷歌插件后，测试了下，其实速度也是一般般的，网络好的情况，是不影响使用的，虽然慢点，但是网络差的情况，我的电信的360测试20M带宽的情况下，打开网页还是费劲的。在浏览器的插件上使用，所有的网络都经由windscribe，有点浪费了，本来想在win10上安装下，用switchomage代理，可以国外的走windscribe,国内的直接连接，省流量，可是安装后，死活连不上vpn，简直抓狂了，路漫漫其修远吾将上下而求索。。。。

### 2.protonvpn
注册后，无限流量，但是有设备和速度限制，设备是一台设备，速度怎么限还不清楚，国家限链接三个国家，节点后面带FREE标志，日本美国和荷兰Nederland，电信的网络这几个国家都连不上。有七天的适用期限。免费版可以说速度很差了，只能看油管360p,还老是卡，基本上只能打开网页了。连上也很麻烦，试了很多节点，只有Austria AT#6、Canada CA#2、Ireland IE#3、Luxembourg Lu#1、Netherlands NL-Free#1、Portugal PT#1可以连上,Japan JP-Free#3这个服务器的速度好像要快一点，可以看1080P,Japan JP#20也可以，等待一会看1440P也可以。South Korea KP#2可以看720P,懒的全部测试了，还是用日本的吧，速度的好坏可能要看时间吧，我测试的时间是下午三点中,浙江移动100M带宽。
ApK的下载地址是：[ProtonVPN.apk](http://protonvpn.com/download/ProtonVPN.apk)
其他的速度测试：
浙江电信的100M带宽和手机电信4G，好像只能连Canada CA#2,速度还可以。

### 3.Tuusafe
官方地址：https://tunsafe.com/， 我试了下，只有Germany节点可以用，速度吗，不太稳定，有时候可以看油管1080P，有时候不行。使用方法就是到官网下载安装程序，现在到了1.5了，安装的时候要挂一个vpn才可以，因为他要下载一个Tap（这就有点蛋疼了）。然后就是到官网https://tunsafe.com/vpn生成一个配置文件。总共有六个配置文件，每下载一个配置文件都要，点击“Generate New Key Pair”->选择节点->点击"Generate and Download",这里只有Germany这个配置文件可以使用，把下载下来的配置文件，放到TunSafe的安装目录下的Config文件夹下，在界面中就可以选择哪一个配置进行连接了。
{% asset_img TunSafe_1.png TunSafe配置文件 %}

### 4.Darklink VPN Free
这是一个免费的VPN软件（好像只能用在安卓手机端），下载下来测试了，功能挺简单，手机电信的4G网络，速度可以，不影响观看视频。不过免费版有广告。当然也可以付费，看自己的需求，去广告,价格是12个月149，感觉还不错。
{% asset_img Darklink VPN Free_1.png Darklink VPN Free %}

## 二、 nordvpn
狠心花七百多大洋，买了一个nordvpn，在上面windscribe连接不顺手的情况下，nordvpn还是可以的，用手机4G测试了，还是可以看视频的，速度也还可以，晚上的时候速度稍微有点慢比早上的时候。同样的问题是，在win10死活连不上vpn。linux下安装，会遇到 无法连接上 repo.nordvpn.com:443 (69.171.229.73)。 - connect (111: 拒绝连接) 的错误，自然也是安装不了nordvpn。

注意一点：通过询问客服，chrome插件在中国是不能用的，还有就是linux版本在中国也是不能用的。
官方客服解释是是这样的：“The main NordVPN application will not work, though it is possible to setup the OpenVPN applciation version.”，虽然我也没用openvpn连接成功。

要想用linux连接可以参考下面几篇文章：
1.[官网](https://support.nordvpn.com/)
2.[Connecting to NordVPN (Linux Network Manager)](https://support.nordvpn.com/Connectivity/Linux/1061938702/How-to-connect-to-NordVPN-using-Linux-Network-Manager.htm)
3.[How can I connect to NordVPN using Linux Terminal?](https://support.nordvpn.com/Connectivity/Linux/1047409422/How-can-I-connect-to-NordVPN-using-Linux-Terminal.htm)
4.[Installing and using NordVPN on Linux](https://support.nordvpn.com/Connectivity/Linux/1182453582/Installing-and-using-NordVPN-on-Linux.htm)
5.[NordVPN 服务器位置](https://nordvpn.com/zh/servers/#recommended)
一篇篇试，祝你们好运。当然看文章也是需要翻墙的。

window10连接步骤是这样的：
第一步尝试：
(1).Please try switching the connection protocol to TCP. It can be changed in the NordVPN application settings.

On Windows application: Scroll down to the bottom of the Settings tab https://nordvpn.com/special/deal/  > Show advanced settings > Protocol > 'TCP'

(2).Also, enable Obfuscated Servers option in the NordVPN application. It can be done by following these steps:

On Windows, NordVPN application go to Settings tab. Scroll down and find Advanced settings and enable the Obfuscated Servers option.

(3).After enabling the Obfuscated servers feature, try connecting to the servers listed below:

France #280-285; #295-302;
United Arab Emirates #3-4;
Netherlands #253-256;
Hong Kong #36
United States #2440-2451; #3057-3060; #3167 - 3170;
Japan #135;
Singapore #186-187.
在客户端setting中开启混淆服务、TCP服务，然后尝试连接下面的服务。我选择了新加坡#186才连上的，新加坡#187也可以，上面的united States #2440也可以，看YouTube 1080p没问题，反正多试试吧，总可以上去的，~~但是连接香港的机子就不行，用手机4G可以连接香港的机子，很奇怪。~~可能网络不稳定吧，晚上也可以看4k的

{% asset_img nordvpn_4k.png nordvpn看4k视频 %}

第二步尝试：
(1).Please go to Control Panel -> Network and sharing center -> Change adapter settings.
(2).Right click on your main network adapter and select Properties. 
(3).Afterward, select IPv4 and Properties again.
(4).Then please add these DNS addresses: 103.86.96.100 and 103.86.99.100.
单击网络设置->更改适配器->IPV4选项->添加DNS103.86.96.100 and 103.86.99.100

对于VPN和SSR来说，虽然都可以翻墙，但是VPN会代理你全部的网络连接，这样如果你在内网中进行协同工作的时候，问题还是比较大的，特别是内网开发的机器作为服务器的时候，别人要连接你的服务器，可能就比较麻烦，或者是丢包或者是ping不通。对于速度来说，不知道是我网络的问题，还是选择的服务器不行，还是其他什么原因，wind10下的速度特别慢，不及手机的4G网络，按理说，我的网络肯定要好过手机的4G,但是打开一个网页确实费劲。
为了解决vpn会代理全部流量的问题，我的解决思路是这样的，通过关闭虚拟机防火墙，并在虚拟机中安装nordvpn，然后安装ccproxy，接受全部外来流量，然后再外部电脑中，通过switchomage代理到ccproxy的端口上即可。

操作步骤如下：
(1).在虚拟机中安装NordVPN，并登录账号，选择连接，保证能连到VPN。

(2).在虚拟机中安装CCProxy，端口保持默认即可。

(3).配置CCProxy，选择设置->高级->网络->取消勾选“禁止局域网外部用户”->确定
{% asset_img CCProxy_1.png CCProxy配置 %}

(4).在虚拟机外部计算机中的Chrome中安装SwitchOmage,新建情景模式->代理服务器->代理协议（Sock5）->代理服务器（填虚拟机内网IP地址）->端口（填CCProxy中的协议地址），可选其他协议，只要对应于虚拟机中CCProxy的端口即可。
(5).愉快的上网吧。

nordvpn确实挺好的，客服回复的挺快，而且速度也不受影响，如果是六七个人合伙买三年套餐，一个人也就120块，其实挺划算的。要是一个公司里买，也是很合适的。买一个账号，配合CCProxy和SwitchOmage，全公司的人都可以用，不行就多买几个，也值得了，才七百块钱

**最后，我决定放弃nordvpn了。**

## 三、准备尝试CyberGhost vpn
放弃了。
1.询问客服，不会中文，连谷歌翻译都不用，nordvpn客服不会中文，我说中文，他还自带翻译，不错。

2.问中国能连吗？

我：“How is the connection speed in China?”
客服：“I am afraid to inform you that the Chinese Government is already blocking most of the know VPN services. Unfortunately, the CyberGhost due to its popularity is already blocked in China. We are still hoping that it will be allowed in the near future because having access to the Internet has really become a necessity.”
我：“Do you have a solution?Can I connect to your service if I buy the service now?”
客服：“As of now there's nothing that we can do to bypass a blocked service due to the government.”
看来是不行了，我也没继续试，就算试试也可以吧，反正三年的订单有45天的退款期。