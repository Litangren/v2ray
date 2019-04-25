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
