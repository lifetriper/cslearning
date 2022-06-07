# vim 的基本使用和配置

## 基本操作

## 基本配置文件

## 插件
### 安装插件管理器
推荐使用 vim-plug 进行 vim 的插件管理。安装命令如下：
```bash
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

### 安装插件的配置
需要在 .vimrc（如果用户的家目录中没有，可以建立一个空白的文件）文件中，增加安装插件的配置。
```bash
call plug#begin()
Plug 'scrooloose/nerdtree'
...  # 各种插件
call plug#end()
```
重新进入 vim 后，在命令模式下输入 PlugInstall，vim 会自动开始安装所要求的插件。

### 常用插件
1. 文件nerdtree

### vim 插件搜索网站：
1. [vimawesome](https://vimawesome.com/)