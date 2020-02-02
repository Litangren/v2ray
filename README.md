参见：https://github.com/Alvin9999/new-pac/wiki/%E8%87%AA%E5%BB%BAv2ray%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%95%99%E7%A8%8B

自建v2ray教程很简单，整个教程分三步：

第一步：购买VPS服务器

第二步：一键部署VPS服务器

第三步：一键加速VPS服务器

【前言】

v2ray的优势：v2ray支持的传输方式有很多，包括：普通TCP、HTTP伪装、WebSocket流量、普通mKCP、mKCP伪装FaceTime通话、mKCP伪装BT下载流量、mKCP伪装微信视频流量，不同的传输方式其效果会不同，有可能会遇到意想不到的效果哦！当然国内不同的地区、不同的网络环境，效果也会不同，所以具体可以自己进行测试。现在v2ray客户端也很多了，有windows、MAC、linux和安卓版。

如果想搭建ss/ssr，可以参考 自建ss/ssr服务器教程

注意：如果想在一台vps服务器上同时搭建ss/ssr和v2ray，端口不要重复。

第一步：购买VPS服务器

VPS服务器需要选择国外的，首选国际知名的vultr，速度不错、稳定且性价比高，按小时计费，能够随时开通和删除服务器，新服务器即是新ip。

vultr注册地址：https://www.vultr.com/?ref=7777564-4F （新用户通过此活动链接注册，赠送50美元，有效期1个月。全球15个服务器位置可选，KVM框架，最低2.5美元/月。）如果以后这个vultr注册地址被墙了，那么就用翻墙软件打开，或者用ss/ssr免费账号



虽然是英文界面，但是现在的浏览器都有网页翻译功能，鼠标点击右键，选择网页翻译即可翻译成中文。

注册并邮件激活账号，充值后即可购买服务器。充值方式是支付宝或paypal，使用paypal有银行卡（包括信用卡）即可。paypal注册地址：https://www.paypal.com （paypal是国际知名的第三方支付服务商，注册一下账号，绑定银行卡即可购买国外商品）

2.5美元/月的服务器配置信息：单核 512M内存 20G SSD硬盘 带宽峰值100M 500G流量/月 (仅提供ipv6 ip)

3.5美元/月的服务器配置信息：单核 512M内存 20G SSD硬盘 带宽峰值100M 500G流量/月 (推荐)

5美元/月的服务器配置信息： 单核 1G内存 25G SSD硬盘 带宽峰值100M 1000G流量/月 (推荐)

10美元/月的服务器配置信息： 单核 2G内存 40G SSD硬盘 带宽峰值100M 2000G流量/月

20美元/月的服务器配置信息： 2cpu 4G内存 60G SSD硬盘 带宽峰值100M 3000G流量/月

40美元/月的服务器配置信息： 4cpu 8G内存 100G SSD硬盘 带宽峰值100M 4000G流量/月

注意：2.5美元套餐只提供ipv6，如果你用不了ipv6，那么你可以买3.5美元的套餐。另外，并非所有地区都有3.5美元的套餐，需要自己去看。由于资源的短缺，有的地区有时候有3.5美元的套餐，有时候没有。

vultr实际上是折算成小时来计费的，比如服务器是5美元1个月，那么每小时收费为5/30/24=0.0069美元 会自动从账号中扣费，只要保证账号有钱即可。如果你部署的服务器实测后速度不理想，你可以把它删掉（destroy），重新换个地区的服务器来部署，方便且实用。因为新的服务器就是新的ip，所以当ip被墙时这个方法很有用。当ip被墙时，为了保证新开的服务器ip和原先的ip不一样，先开新服务器，开好后再删除旧服务器即可。在账号的Billing选项里可以看到账户余额。

账号充值如图：





开通服务器步骤如图：







为了配合v2ray一键搭建脚本，vps操作系统可以选择Debian 8、Debian 7、Ubuntu 14、Ubuntu 16、CentOS 7。（注意：不支持CentOS 6和8系统！）
开通服务器时，当出现了ip，不要立马去ping或者用xshell去连接，再等5分钟之后，有个缓冲时间。完成购买后，找到系统的密码记下来，部署服务器时需要用到。vps系统的密码获取方法如下图：





删掉服务器步骤如下图：







一个被墙ip的vps被删掉后，其ip并不会消失，会随机分配给下一个在这个服务器位置新建服务器的人，这就是为什么开新服务器会有一定几率开到被墙的ip。被墙是指在国内地区无法ping通服务器，但在国外是可以ping通的，vultr是面向全球服务，如果这个被墙ip被国外的人开到了，它是可以被正常使用的，半年或1年后这个被墙的ip可能会被国内防火墙解封，那么这就是一个良性循环。

第二步：部署VPS服务器

购买服务器后，需要部署一下。因为你买的是虚拟东西，而且又远在国外，我们需要一个叫Xshell的软件来远程部署。Xshell windows版下载地址：

国外云盘下载

如果你是苹果电脑操作系统，更简单，无需下载xshell，系统可以直接连接VPS。打开终端（Terminal），输入ssh root@ip 其中“ip”替换成你VPS的ip, 按回车键，然后复制粘贴密码，按回车键即可登录。粘贴密码时有可能不显示密码，但不影响， 参考设置方法 如果不能用MAC自带的终端连接的话，直接网上搜“MAC连接SSH的软件”，有很多，然后通过软件来连接vps服务器就行，具体操作方式参考windows xshell。

部署教程：

下载windows xshell软件并安装后，打开软件



选择文件，新建



随便取个名字，然后把你的服务器ip填上



连接国外ip即服务器时，软件会先后提醒你输入用户名和密码，用户名默认都是root，密码是你购买的服务器系统的密码。

如果xshell连不上服务器，没有弹出让你输入用户名和密码的输入框，表明你开到的ip是一个被墙的ip，遇到这种情况，重新开新的服务器，直到能用xshell连上为止，耐心点哦！如果同一个地区开了多台服务器还是不行的话，可以换其它地区。




连接成功后，会出现如上图所示，之后就可以复制粘贴代码部署了。

2019.2.11更新：

Debian8/Debian7/Ubuntu16/Ubuntu14/CentOS7 v2ray一键部署管理脚本：

安装脚本命令：

wget -N --no-check-certificate https://raw.githubusercontent.com/KiriKira/v2ray.fun/kiriMod/install.sh && bash install.sh

卸载脚本命令：

wget -N --no-check-certificate https://raw.githubusercontent.com/KiriKira/v2ray.fun/kiriMod/uninstall.sh && bash uninstall.sh

如果提示 wget: command not found 的错误，这是你的系统精简的太干净了，wget都没有安装，所以需要安装wget。CentOS系统安装wget命令: yum install -y wget Debian/Ubuntu系统安装wget命令:apt-get install -y wget

———————————————————代码分割线————————————————

复制上面的代码到VPS服务器里，复制代码用鼠标右键的复制，然后在vps里面右键粘贴进去，因为ctrl+c和ctrl+v无效。接着按回车键，脚本会自动安装。





如上图，输入快捷管理命令v2ray后，开始进行v2ray服务端配置。以后只需要运行这个快捷命令就可以出现下图的界面进行设置，快捷管理命令为：v2ray



如上图，输入数字2进行更改配置，共有6个子选项，包括：更改UUID、更改主端口、更改加密方式、更改传输方式、更改TLS设置（有域名才行）、更改广告拦截功能。（更改TLS设置和更改广告拦截功能不用设置）



如上图，输入数字1来更改新的UUID号，弹出提示后，输入字母y来确认。



修改UUID号，界面会回到v2ray主界面，重新输入2进入更改配置选项，在输入数字2来更改主端口，主端口范围40～65535，理论上可以任意设置，但不要以0开头！



重新进入更改配置选项，输入数字3来更改加密方式，加密方式有4种，最后1种为不加密。



接着，进行传输方式的设置，传输方式共有7种，这个配置对v2ray的速度起着很大的作用，具体哪个最适合你那里的网络环境，需要你自己来尝试。

注意：普通TCP、普通mKCP、mKCP伪装FaceTime通话、mKCP伪装BT下载流量、mKCP伪装微信视频流量可直接设置、不需要域名，HTTP伪装和WebSocket流量需要你有域名，且域名绑定了你的vps服务器ip。



进行了更改配置的设置后，输入数字3可以查看自己设置的v2ray信息。



最后一步很关键，那就是启动服务，进入主界面后，输入数字1，然后输入1启动v2ray服务。以后，每次你更改配置或重启vps服务器后都要进行启动服务，请牢记！



采用xshell软件，可以很方便的将配置文件导出，方便配置windows v2ray客户端。选择数字4，出现提示后，输入字母y，选择电脑路径即可。

如果你没有用xshell软件，那么无法使用脚本的文件导出功能。vps服务器里面的config.json配置文件存放路径为 /etc/v2ray/config.json MAC电脑用户可以用WinSCP MAC版连接vps服务器，然后根据路径把config.json文件复制出来。



下面这个config.jason文件就是我们刚刚配置的v2ray文件，如果以后更改了v2ray服务端信息，那么你需要重新导出config.jason文件。



因为一键搭建v2ray脚本是一个循环脚本，当你配置结束后不会自动退出快捷管理命令，如果你想退出界面进行其它操作，可以同时按下键盘上的ctrl键和字母z键。

注意：以上直接下载并替换config文件的方法只适合v2ray官方客户端，像第三方开发的客户端，比如v2rayN、v2rayX是不适合用直接替换config文件的方法。如果用第三方开发的客户端的话，可以按照要求填写账号信息，参考教程：v2ray各平台图文使用教程
第三步：一键加速VPS服务器

总共有2种加速方法，bbr加速和锐速加速，选择1种。

【加速教程1：谷歌BBR加速教程】

wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh

chmod +x bbr.sh

./bbr.sh

把上面整个代码复制后粘贴进去，不动的时候按回车，然后耐心等待。最后输入reboot来重启服务器，确保加速生效，bbr加速脚本是开机自动启动，装一次就可以了。

演示开始，如图：

复制并粘贴代码后，按回车键确认



如下图提示，按任意键继续部署





整个部署过程需要2～5分钟，最后输入reboot来重启服务器，确保加速生效，bbr加速脚本是开机自动启动，装一次就可以了。

服务器重启成功并重新连接服务器后，输入命令lsmod | grep bbr 如果出现tcp_bbr字样表示bbr已安装并启动成功。如图：



注意：根据反馈，少部分人安装bbr脚本并重启后，几分钟过去了，发现xshell无法连接服务器且服务器ip无法ping通。解决方法是：开新服务器或者重装系统，然后先安装bbr脚本再安装v2ray脚本。或者换锐速加速。

重装系统方法，点击vultr服务器设置界面——“Server Reinstall”，如下图：



重装过程一般需要5～10分钟。

【加速教程2：破解版锐速加速教程】

第一步，先更换服务器内核（脚本只支持centos系统，其它系统可以直接尝试第二步）

yum -y install wget

wget --no-check-certificate https://blog.asuhu.com/sh/ruisu.sh && bash ruisu.sh



不动的时候敲回车键，在上图时需要多等一会儿。



出现上图时表示已成功替换内核并服务器自动重启。

完成后会重启，2分钟后重新连接服务器，连上后开始第二步的操作。

第二步，一键安装锐速

wget -N --no-check-certificate https://raw.githubusercontent.com/91yun/serverspeeder/master/serverspeeder-all.sh && bash serverspeeder-all.sh

卸载加速代码命令为：

chattr -i /serverspeeder/etc/apx* && /serverspeeder/bin/serverSpeeder.sh uninstall -f

但有些内核是不适合的，部署过程中需要手动选择推荐的，当部署时出现以下字样：



提示没有完全匹配的内核,随便选一个内核就行,按照提示来输入数字,按回车键即可

锐速安装成功标志如下：



出现running字样即可!

需要注意的是：不管是重启服务器，还是以后想修改之前vps里面的v2ray配置信息，当你重启好服务器或者修改好了v2ray配置信息后，都需要启动v2ray服务端。方式是：输入v2ray，选择1，然后选择1（启动服务）。
【v2ray客户端下载】

2019年12月11日更新。

v2ray各平台客户端下载地址

v2ray iOS客户端下载地址

v2ray 安卓客户端下载地址 v2rayNG下载地址

以v2ray windows版为例：



下载windows版客户端后解压出来，然后替换config.json配置文件。



运行上图中的v2ray.exe启动软件，浏览器代理设置成Socks(5) 127.0.0.1 和1080 即可通过v2ray代理上网。

谷歌浏览器chrome可配合switchyomega插件来使用，下载插件：switchyomega

安装插件，打开chrome，打开扩展程序，将下载的插件拖动到扩展程序页面，添加到扩展。 20181116000534

完成添加，会跳转到switchyomega页面，点跳过教程，然后点击proxy，如图填写，最后点击应用选项。 20181116001438

注意：以上直接下载并替换config文件的方法只适合v2ray官方客户端，像第三方开发的客户端，比如v2rayN、v2rayX是不适合用直接替换config文件的方法。如果用第三方开发的客户端的话，可以按照要求填写账号信息，参考教程：v2ray各平台图文使用教程
常见问题参考解决方法：

1、账号无法使用，可能原因一：客户端与服务端的设备系统时间相差过大。

当vps服务器与本地设备系统时间相差过大，会导致客户端无法与服务端建立链接。请修改服务器时区，再手动修改服务器系统时间（注意也要校准自己本地设备时间）！

先修改vps的时区为中国上海时区：\cp -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

再手动修改vps系统时间命令的格式为（数字改为和自己电脑时间一致，误差30秒以内）：date -s "2018-11-02 19:14:00"

修改后再输入date命令检查下。

2、账号无法使用，可能原因二：Windows 防火墙、杀毒软件阻挡代理软件。

如果以上问题都已排查，可以关闭 Windows 自带的防火墙、杀毒软件再尝试。

有问题可以发邮件至海外邮箱kebi2014@gmail.com






v2ray

最好用的 V2Ray 一键安装脚本 & 管理脚本

2Ray 官网：https://www.v2ray.com

最新一键安装v2ray脚本：

sudo -i

bash <(curl -s -L https://git.io/v2ray.sh)

如果提示 curl: command not found ，那是因为你的 VPS 没装 Curl

ubuntu/debian 系统安装 Curl 方法: apt-get update -y && apt-get install curl -y

centos 系统安装 Curl 方法: yum update -y && yum install curl -y

安装好 curl 之后就能安装脚本了

见视频：

https://www.youtube.com/watch?v=Il8TL5vXUwE

https://www.youtube.com/watch?v=WGGkMSqTVXQ 





233blog注意了一键安装脚本v2ray ss挖坑,留有后门吗?实际测试对比!

 v2ray 配置编辑（可清除后门)，黑名单在 /etc/v2ray/config.json及 "/etc/v2ray/233boy/v2ray/config/server/include/ban.json"

 sudo -i

 vim /etc/v2ray/config.json  (vim 是 vi 的升级版）


 键盘 i ----编辑 134-157 行中的黑名单网站，更改网站名为无效网站名即可

 （d-删除命令；i-编辑插入命令)
 
  ctrl - v 粘贴


 Esc 

 Shift + :

 wq 保存 退出vim (Shift + : q 不保存退出)
 
注意：编辑完/etc/v2ray/config.json，需要重新启动v2ray (最好是先停止v2ray ,再启动v2ray。实测直接删除黑名单网站会导致v2ray无法启动）

备份

为了避免由于不可抗拒的原因所造成作者主动删除脚本，所以建议请将本脚本 Fork 一份

备份地址： https://github.com/233boy/v2ray/fork

安装方法如下，确保你已经 Fork 了脚本，将 233boy 修改成你的 Github 用户名，如这里的Litangren

git clone https://github.com/Litangren/v2ray

cd v2ray

chmod +x install.sh

./install.sh local

如果提示 git 命令不可用，那就自己安装咯

https://github.com/233boy/v2ray


# v2ray
最好用的 V2Ray 一键安装脚本 &amp; 管理脚本

## 脚本说明
[V2Ray 一键安装脚本](https://github.com/233boy/v2ray/wiki/V2Ray%E4%B8%80%E9%94%AE%E5%AE%89%E8%A3%85%E8%84%9A%E6%9C%AC)

## 搭建教程
[V2Ray搭建详细图文教程](https://github.com/233boy/v2ray/wiki/V2Ray%E6%90%AD%E5%BB%BA%E8%AF%A6%E7%BB%86%E5%9B%BE%E6%96%87%E6%95%99%E7%A8%8B)

## 资助 V2Ray
请考虑 [资助 V2Ray 发展](https://www.v2ray.com/chapter_00/02_donate.html)

## 更多 V2Ray 教程文章
https://github.com/233boy/v2ray/wiki
