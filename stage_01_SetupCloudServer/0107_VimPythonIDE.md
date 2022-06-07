# 将 vim 打造成 python IDE

## 运行 python 代码
使用 Vim 写完代码后，想像 PyCharm 一样直接快捷键运行代码，需要你在 .vimrc 中写入如下的配置。 这段配置，不仅包括 Python ，还有 Bash 和 Golang
```bash
\" F5 to run sh/python3
map <F5> :call CompileRunGcc()<CR>
func! CompileRunGcc()
    exec "w"
    if &filetype == 'sh'
        :!time bash %
    elseif &filetype == 'python'
        exec "!time python3 %"
    elseif &filetype == 'go'
        exec "!time go run %"
    endif
endfunc
```
配置完后，使用 F5 就可以直接运行当前的脚本。

## Tagbar
可以查看当前代码文件中的变量和函数列表的插件，并切换和跳转到代码中对应的变量和函数的位置
```bash
\" 查看当前代码文件中的变量和函数列表的插件，
\" 可以切换和跳转到代码中对应的变量和函数的位置
\" 大纲式导航, Go 需要 https://github.com/jstemmer/gotags 支持
Plug 'preservim/tagbar'
```
