## 1. shell 中的竖线（|）什么用?
>http://blog.sina.com.cn/s/blog_6d09b5750100vley.html
>管道符号，是unix一个很强大的功能,符号为一条竖线:"|"。
用法: command 1 | command 2 他的功能是把第一个命令command 1执行的结果作为command 2的输入传给command 2

## 2. linux 查找文件或者内容常用命令
>http://www.cnblogs.com/sunleecn/archive/2011/11/01/2232210.html
```
whereis <程序名称>
查找软件的安装路径
-b 只查找二进制文件
-m 只查找帮助文件
-s 只查找源代码
-u 排除指定类型文件
-f 只显示文件名
-B <目录> 在指定目录下查找二进制文件
-M <目录> 在指定目录下查找帮助文件
-S <目录> 在指定目录下查找源代码

locate <文件名称>
在文件索引数据库中搜索文件
-d <数据库路径> 搜索指定数据库
updatedb
更新文件索引数据库


find [路径] <表达式>
查找文件
-name <表达式> 根据文件名查找文件
-iname <表达式> 根据文件名查找文件，忽略大小写
-path <表达式> 根据路径查找文件
-ipath <表达式> 根据路径查找文件，忽略大小写
-amin <分钟> 过去N分钟内访问过的文件
-atime <天数> 过去N天内访问过的文件
-cmin <分钟> 过去N分钟内修改过的文件
-ctime <天数> 过去N天内修改过的文件
-anewer <参照文件> 比参照文件更晚被读取过的文件
-cnewer <参照文件> 比参照文件更晚被修改过的文件
-size <大小> 根据文件大小查找文件，单位b c w k M G
-type <文件类型> 根据文件类型查找文件。b 块设备 c 字符设备 d 目录 p 管道文件 f 普通文件 l 链接 s 端口文件
-user <用户名> 按归属用户查找文件
-uid <uid> 按UID查找文件
-group <群组名> 按归属群组查找文件
-gid <gid> 按GID查找文件
-empty 查找空文件


从文件内容查找匹配指定字符串的行：
$ grep "被查找的字符串" 文件名
从文件内容查找与正则表达式匹配的行：
$ grep –e “正则表达式” 文件名
查找时不区分大小写：
$ grep –i "被查找的字符串" 文件名
查找匹配的行数：
$ grep -c "被查找的字符串" 文件名
从文件内容查找不匹配指定字符串的行：
$ grep –v "被查找的字符串" 文件名

从根目录开始查找所有扩展名为.log的文本文件，并找出包含”ERROR”的行
find / -type f -name "*.log" | xargs grep "ERROR"

系统查找到httpd.conf文件后即时在屏幕上显示httpd.conf文件信息。 
find/-name"httpd.conf"-ls

在根目录下查找某个文件
find . -name "test"

在某个目录下查找包含某个字符串的文件

grep -r "zh_CN" ./
```

## 3.复制但是不覆盖原目录
>scp 命令默认会覆盖掉原目录，可以使用 rsync 命令
```
rsync 命令比 scp 更强大，支持“不覆盖”原目录
例子：rsync -avz --progress /root/client/   root@202.112.23.12:/home/work/      
        //将本机的/root/client/拷贝至远程的202.112.23.12:/home/work/目录，--progress可以查看拷贝的过程
例子：rsync -avzu --progress /root/client/   root@202.112.23.12:/home/work/     //u选项，指定不覆盖原目录内容
```



