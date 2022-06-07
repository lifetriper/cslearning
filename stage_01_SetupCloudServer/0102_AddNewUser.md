# 增加一个新的用户
## 指令
```bash
sudo useradd jamesl
```

## 给新增加用户 sudo 权限
为了给新用户增加 sudo 权限，我们可以将这个用户加入到 wheel 组中。
```bash
sudo usermod -aG wheel jamesl
```

## 给新用户配置 ssh 登陆权限
```bash
su - jamesl
mkdir .ssh.  // 在当前用户目录下建立一个.ssh目录
chmod 700 .ssh  // 必须将.ssh目录的权限更改为700
cd .ssh
touch authorized_keys
chmod 600 authorized_keys  // 必须将authorized_keys的权限更改为 600
将本机产生 ssh 密钥对中的公钥内容直接 copy 到 authorized_keys 中

#可以远程登录这部机器中
```
