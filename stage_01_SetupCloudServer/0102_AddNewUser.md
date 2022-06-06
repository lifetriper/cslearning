## 增加一个新的用户
```bash
sudo useradd jamesl
```

### 给新增加用户 sudo 权限
为了给新用户增加 sudo 权限，我们可以将这个用户加入到 wheel 组中。
```bash
sudo usermod -aG wheel jamesl
```

### 给新用户配置 ssh 登陆权限
```bash
su - jamesl
mkdir .ssh.  // 在当前用户目录下建立一个.ssh目录
chmod 700 .ssh  // 必须将.ssh目录的权限更改为700
cd .ssh
touch authorized_keys
chmod 600 authorized_keys  // 必须将authorized_keys的权限更改为 600
将私钥相对应的公钥copy到authorized_keys中

#可以远程登录这部机器中
```

### 配置主机名
```bash
sudo hostnamectl set-hostname webserver.localdomain
```