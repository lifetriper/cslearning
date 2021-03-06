# 租用 AWS 云服务器

## 租用云服务器之前的技术准备
### 使用 ssh
租用 AWS 的 Lightsail 云服务器之前建议先为自己产生一个 ssh 的密钥对。当然讲到 ssh
密钥对，马上会产生一系列技术了解的需求。我们假设你不懂任何 ssh 密钥的技术能力，在这里只是告诉你该怎么做，以及能实现什么样的功能。

传统上，登陆到一台 Linux 服务器上需要用户提供用户名和密码。但是在使用云服务器，提供用户名和密码有以下的不便和安全风险：
1. 每次登陆服务器都需要输入用户名和密码；
2. 有的用户使用 telnet 登陆远端服务器，还会出现用户名和密码被监听的风险；

基于以上的考虑，大部分现在的云服务器都支持 ssh 远程登陆的方式。大致的实现方式如下：
1. 首先在本机上产生一个密钥对，一个称为公钥，一个称为私钥；
2. 在租用云服务器的时候，可以让用户把公钥上传到云服务商；
3. 在同一个云服务商申请的所有云服务器，都可以使用这个公钥；
4. 在云服务器启用后，这个公钥会自动安装在这个云服务器的默认用户目录下，并且云服务器会自动启用 ssh 服务端功能。比如对于 AWS 的 EC2
   云服务器，如果选择的操作系统是 Amazon Linux，则会默认建立一个 ec2-user 的用户，上传的密钥会自动安装在这个用户的家目录中；
5. 在云服务器启用后，用户可以在自己的笔记本电脑或者 iPad 上，经过一个简单的配置，就可以登陆到远端的云服务器上了；

### 在本机上产生 ssh 密钥对
以下 ssh-keygen 命令默认在 ~/.ssh 目录中生成 4096 位 SSH RSA 公钥和私钥文件。 如果当前位置存在 SSH
密钥对，这些文件将被新产生的密钥对覆盖。以 MacOS 为例，默认情况下，其中 id_rsa 为私钥，id_rsa.pub 为公钥。在 MacOS 上产生
ssh
密钥对的指令如下（在自己的笔记本电脑上执行）：
```bash
ssh-keygen -m PEM -t rsa -b 4096
ssh-keygen \
    -m PEM \   # 将密钥的格式设为 PEM
    -t rsa \   # 要创建的密钥类型，本例中为 RSA 格式
    -b 4096 \   # 密钥的位数，本例中为 4096
    -C "azureuser@myserver" \   # 追加到公钥文件末尾以便于识别的注释。 通常以电子邮件地址用作注释
    -f ~/.ssh/mykeys/myprivatekey \   # 私钥文件的文件名，相应公钥文件加了.pub后缀，生成在相同目录中 
    -N mypassphrase   # 用于访问私钥文件的其他密码
    
ssh-keygen -p   # 更改私钥的passphrase（密码）
```
强烈建议为私钥添加密码。 如果不使用密码来保护密钥文件，任何人只要拥有该文件，就可以用它登录到拥有相应公钥的任何服务器。 添加密码可提升防护能力以防有人能够访问私钥文件，可让用户有时间更改密钥。

## 租用云服务器
当设置好自己的台式/笔记本电脑后，可以考虑租用一台云服务器。租用一台云服务器的主要好处有如下几点：
1. 费用不高，我租用一台 AWS 的 Lightsail 云服务器，1G 内存，1个 vCPU，40GB 的 SSD 硬盘，每个月 2TB 
   的流量也就5美元左右。在国内租用腾讯或者阿里的入门级云服务器，价格也在可以承受的范围内；
2. 有了云服务器，最大的便利在于如果你在户外，只需要一台 iPad，就可以执行大部分在室内笔记本上的活动，这样就不需要带着笔记本到处走了，非常轻便；
3. 有了云服务器，就有一台带有固定公网地址的计算机，可以在网络上方便的处理各种内外服务，只要你有足够的技术和想法；


### 如何租用 AWS Lightsail 云服务器
租用 AWS 的 Lightsail 云服务器实际上要做两件事情：
1. 租用一个静态的 IP 公网地址。对于 AWS 来说，只要这个静态的 IP 
   公网地址是和一台服务器相关联的，用户就不用为这个公网地址付费。这样的好处是，就算我们租用的服务器重新启动，或者销毁重新租用其他的 
   Lightsail 服务器，我们都可以维持一个不变的公网 IP 地址；
2. 租用一个 Lightsail 服务器，建议至少租用5美元的服务器；

### 租用一个静态的 IP 公网地址
在 AWS 的 Lightsail 主页面中，选择 Networking，选择 Create Static IP。如下图：

![租用静态的IP公网地址](../img/StaticIP_01.png "租用静态的IP公网地址")

之后，可以在管理页面中，将这个申请的 IP 地址与一个具体的 Instance 相捆绑，相应的云服务器实例就具有这个 IP 地址了。

### 租用一个服务器实例(Instance)
租用一个 Lightsail 服务器实例可以按照如下步骤执行：
1. 在主页的 Instances 下，选择 Create Instance；
2. 在 Select a platform 选择 Linux/Unix，选择 OS Only，选择 Amazon Linux 2；
![选择操作系统](../img/Lightsail_01.png)
3. 在 Change SSH Key Pair 中选择 Upload New。将我们之前在笔记本上获得的密钥对的公钥 id_rsa.pub 上载到 
   AWS 中。这个公钥之后可以被其他的 Lightsail 服务器继续使用；

   ![上载公钥](../img/Lightsail_02.png "上载公钥")
4. 在 Choose your instance plan 中，选择适合自己的服务计划。我的选择是5美元的，拥有 1G 的内存，每月 2TB 
   的网络传输流量，10% 的 CPU 速度，基本上可以满足大部分人的日常使用。另外还可以给这个实例起一个名字,之后就可以选择建立自己的云服务器实例了。
![选择计划](../img/Lightsail_03.png "选择计划")
5. 在 AWS 完成云服务器设置之后，我们还要将我们之前租用的 IP 地址分配给这个云服务器。
![管理服务器](../img/Lightsail_04.png "管理服务器")
在 Networking 上，将我们之前租用的 IP 地址分配给这个服务器就完成设置了。
![分配静态IP地址](../img/Lightsail_05.png "分配静态IP地址")
此外，需要注意的是，默认情况下 IPv4 Firewall 的 SSH 
   设置是允许通过的。这个保证了我们下一步从远端（比如自己的笔记本）连接云服务器时，不会被防火墙阻挡。完成了我们以上的设置之后，我们就可以开始准备使用第一个自己的云服务器了。

## 远端连接云服务器
为了方便以后连接云服务器，我们可以给这个云服务器设置一个和 IP 地址对应的名字，这个设置可以写在本地笔记本电脑上的 /etc/hosts 
中。我给我的云服务器起的名字叫 cell201.als
```bash
##
# Host Database
#
# localhost is used to configure the loopback interface
# when the system is booting.  Do not change this entry.
##
127.0.0.1       localhost
255.255.255.255 broadcasthost
::1             localhost
x.x.x.x         cell201.als
```
之后可以在本地的笔记本电脑上使用 ssh 命令，连接远端的云服务器：
```bash
ssh ec2-user@cell201.als  # ec2-user 是安装 Amazon Linux 默认的用户
```
![连接远端服务器](../img/Lightsail_06.png "SSH连接远端服务器")

 至此，我们拥有了一台可以随时使用的远端云服务器。

