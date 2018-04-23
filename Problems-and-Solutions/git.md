## 1.[github] github 怎么解决中文乱码问题？
> [git乱码解决方案汇总](https://blog.zengrong.net/post/1249.html)

- 在cygwin中，使用git add添加要提交的文件的时候，如果文件名是中文，会显示形如 274\232\350\256\256\346\200\273\347\273\223.png 的乱码。

解决方案：在 bash 提示符下输入：
```
git config --global core.quotepath false
```

- 在MsysGit中，使用git log显示提交的中文log乱码。

解决方案：
```
# 设置git gui的界面编码
git config –global gui.encoding utf-8

# 设置 commit log 提交时使用 utf-8 编码，可避免服务器上乱码，同时与linix上的提交保持一致！
git config –global i18n.commitencoding utf-8
```

- 我用 xftp 从 windows 下把文件传到 linux 后，在 linux 系统下直接显示的就是乱码，这是因为 windows 下使用的是 GBK 编码，我们需要把它转为 UTF-8 编码。可以使用 convmv 命令进行文件名的编码转换，而且可以使用 -r 直接把整个文件夹下的所有文件都改了：
```
convmv -f GBK -t UTF-8 --notest (-r) utf8编码的文件（夹）名
```

<center><img src="https://raw.githubusercontent.com/yongyehuang/ocean-of-knowledge/master/figs/convmv1.png"   width="80%"/>
fig1. 使用 convmv 转换中文文件名编码方式
</center>


## 2.[github]如何更新 fork 别人的项目？
[同步一个 fork](https://gaohaoyang.github.io/2015/04/12/Syncing-a-fork/)

## 3.[github]把当前的状态用一个新的分支保存起来？
```shell
git checkout -b 1.2.1  # 先创建一个新的分支1.2.1并切换到新分支上
git push origin 1.2.1  # 把新分支传上去
```
然后可以在分支上修改内容了，最后把修改的内容通过 merge 合并到 master 分支上面
```shell
git checkout master  # 切换回 master 分支
git merge 1.2.1  # 合并 1.2.1 分支上面做的修改
```


