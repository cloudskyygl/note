# Linux 命令学习笔记

## `cp`

* 若参数指定的目的文件存在，其文件数据会被覆盖
* 若参数指定的目标目录不存在，其行为是创建该目录的副本并命名为所指定的名称
* 若参数指定的目标目录存在，则是直接复制到目标目录下，源目录名称不变

## `ln`

使用`ln -s TARGET LINK_NAME` 创建软链接，`TARGET` 用绝对路径较好

例如 `ln -s a test/b` 使用相对路径，查看 `ls -l test/b` 的结果是 ` b -> a`,也就是说软链接 `b` 指向的是相对于 `b` 所在目录下的 `a`，而与 `b` 同目录下并没有 `a`。

由此看出，命令 `ln -s TARGET LINK_NAME` 只是单纯的创建名为 `LINK_NAME` 的软连接文件,并简单的指向 `TARGET` 所指定的文件或目录，即使 `TARGET` 使用相对路径表示也不会自动处理为绝对路径，以致创建的软链接文件无效。


## `.` 和 `..` 实质上是硬链接

```shell
$ ls -dliF test
1048658 drwxrwxr-x 3 user user 4096 Aug 25 01:04 test/ # inode: 1048658

$ ls -aliF
total 12
1048658 drwxrwxr-x  3 steven steven 4096 Aug 25 01:04 ./ # inode: 1048658
 917505 drwxr-xr-x 40 steven steven 4096 Aug 25 00:18 ../
1048659 drwxrwxr-x  2 steven steven 4096 Aug 25 01:04 a/

$ ls -aliF
total 8
1048659 drwxrwxr-x 2 steven steven 4096 Aug 25 01:04 ./
1048658 drwxrwxr-x 3 steven steven 4096 Aug 25 01:04 ../ # inode: 1048658
```

查看 `.` `..` 的 inode 可以知道它们都是指向目录 `test` 的 `inode` 的硬链接，也就是说，链接是指向文件 `inode` 的指针。
因此，文件名和目录名都是指向其 `inode` 的链接。

参考文章 https://www.ibm.com/developerworks/cn/linux/l-cn-hardandsymb-links/index.html

>我们知道文件都有文件名与数据，这在 Linux 上被分成两个部分：用户数据 (user data) 与元数据 (metadata)。用户数据，即文件数据块 (data block)，数据块是记录文件真实内容的地方；而元数据则是文件的附加属性，如文件大小、创建时间、所有者等信息。在 Linux 中，元数据中的 inode 号（inode 是文件元数据的一部分但其并不包含文件名，inode 号即索引节点号）才是文件的唯一标识而非文件名。文件名仅是为了方便人们的记忆和使用，系统或程序通过 inode 号寻找正确的文件数据块。

## `sudo`

```
sudo -l
```

列出当前用户被允许和被禁止的命令

```
sudo -l -U user
```

其中 `-U user` 表示指定用户

## `curl`

下载单个文件，默认将输出打印到标准输出中(STDOUT)中

```
$ curl http://www.centos.org
```

通过-o/-O选项保存下载的文件到指定的文件中：

* -o：将文件保存为命令行中指定的文件名的文件中
* -O：使用URL中默认的文件名保存文件到本地

## 多个用户访问同一文件的权限问题

如果需要在多个用户家目录下使用同一文件，可将该文件放在 ```/tmp``` 目录下，避免了访问权限的麻烦。

例如：在配置 gitolite时，需要管理员账户把初始化 gitolite 的公钥文件上传到服务器，以供 git 用户使用，把公钥文件放在 ```/tmp``` 会方便很多

## `su - git`

`-, -l, --login`

make  the  shell a login shell, clears all envvars except for TERM, initializes HOME, SHELL, USER, LOGNAME and PATH



## 获取解压缩输出信息

`tar axvf git.tar.gz | head -n 1` 无法进行解压缩操作，在得到解压缩输出信息的第一行就停止解压缩命令了，可以用 `sed -n '1p'` 来代替上面的 `head -n 1`

## 子 shell

在子 shell 中执行的解压缩、ls等有信息输出的命令，若没有变量接收那些信息，执行 shell 脚本时会报某些错误
