---
layout: post
title:  github博客搭建过程
categories: 杂学
tags:  博客
author: renql
---

* content
{:toc}

一直想要弄个个人博客，把一些笔记、感想放到上面，不为给别人看，只想自己在无聊的时候，用手机上网就可以看到自己以往写的各种笔记。

本来想把笔记放在CSDN上，但发现CSDN上的广告太多了，界面也不像振宁师兄的那个Github博客友好，因此也准备在Github上搭一个博客。本想在自己的笔记本上搭，但发现要装的软件太多了（git，ruby，jekyll），懒得搞这些的我，准备直接在服务器上clone师兄的代码，然后直接推送到Github上，不准备在本地试运行了。

# 现把搭建过程记录如下： #






- 先在团队服务器上建立文件夹用于放代码，然后再clone师兄的代码    
```bash
mkdir RenqlSYSU.github.io    
cd RenqlSYSU.github.io/
git init
git clone git@github.com:RenqlSYSU/Novarizark.github.io.git
```
- 修改 _config.yml 中的参数和网站小图favicon.ico
- _posts 目录下存放文章信息，文章头部注明 layout(布局)、title、date、categories、tags、author(可选)、mathjax(可选，是插入数学公式用的)，如下：
`---
layout: post
title:  "山东半岛预报系统搭建"
categories: modeling linux
tags:  WRF forecast&nbsp;system
author: LZN
---`
# 放了一篇博客到 _post 上，发现不经过jekyll编译，github不会生成网页，因此还是准备装一下jekyll#
虽然说Windows上也可以安装jekyll，但更想在linux上装，因此在sony笔记本上安装了ubuntu，安装分区如下

|目录|大小|格式|描述|
|----|----|---|---|
|/|20G|ext4|根目录|
|swap|2000M|swap|交换空间|
|/boot|200M|ext4|Linux的内核及引导系统程序所需要的文件，比如 vmlinuz initrd.img文件都位于这个目录中。在一般情况下，GRUB或LILO系统引导管理器也位于这个目录；启动撞在文件存放位置，如kernels，initrd，grub|
|/tmp|5G|ext4|系统的临时文件，一般系统重启不会被保存。（建立服务器需要？）|
|/home|243G|ext4|用户工作目录；个人配置文件，如个人环境变量等；所有账号分配一个工作目录|

安装成功后，发现无法连接wifi，解决方法：先连有线网络，然后点“设置”——“软件和更新”——“附件驱动”——选择Broadcom 802.11，然后点击应用更改，接着电脑重启就可以连接WiFi了

连上WiFi后，安装了如下软件：
```bash
sudo apt install git
sudo apt install vim
sudo apt install openssh-sever #若想要让该linux被远程登录，需要安装openssh-sever，若要该系统能远程登录其他linux，则需要安装openssh-client，登录方式 ssh username@ip-adress
dpkg -l #可查看当前安装的软件
ps -e | grep ssh #查看ssh-server是否启动，若有sshd这一项，表面启动了
ifconfig #查看本机的ip地址

#下面开始安装jekyll
sudo apt install ruby
sudo gem install jekyll #报错，说failed to build gem native extension，然后输入sudo apt install ruby-dev解决该问题

#下面设置连接github仓库
ssh-keygen -t rsa -b 4096 -C "email@xxx" # email是GitHub账号，在需要输入密码时，什么都不输直接回车
cat ~/.ssh/id_rsa.pub #复制公钥到github网页上
ssh -T git@github.com #有You've successfully authenticated即说明连接成功
git config --global user.name "xxxx"
git config --global user.email "email@xxxx"
git config --global github.user xxxx
git config --global github.token xxxx
mkdir xxx.github.io
cd xxx.github.io
git init
git remote add origin git@github.com:xxxx/xxx.github.io
git pull origin master #下载仓库中的代码

```

安装上述过程修改好相应代码后，发现仍然无法显示我写的博客，网页上一片空白。
最后经研究发现，主要是因为文章名字的问题，时间格式必须是2018-01-30,
如果写成20180130就不会被github解析，因此这次是我一直无法成功的原因，和是否
经过本地运行无关。

另外，看网上的文章发现，一般不需要将jekyll编译生成的_site文件夹推到github
上，可以将其写入.gitignore文件中。

接下去的问题就是修改师兄博客中的其他页面的md文件，将其该成自己的内容。
