# Linux 基本指令和 bash 快捷键

## 配置主机名
```bash
# 对于 Amazon Linux 2 的机器直接改动/etc/hostname，没有效果
sudo hostnamectl set-hostname webserver.localdomain
```

## bash 常用快捷键
- 移动光标至行首：C+a；
- 移动光标至行尾：C+e；
- 光标向前移动一个单词：ESC,b；
- 光标向后移动一个单词：ESC,f；
- 删除光标前一个单词：C+w；
- 删除光标后一个单词：ESC,d；
- 删除光标处至行尾：C+k；
- 删除光标处至行首：C+u；