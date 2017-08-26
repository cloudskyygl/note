## 编译安装 git

## 创建用户 git

## 添加开发者 SSH 公钥

authorized_keys

## 工作流程

* 在服务器端创建裸仓库 ```git init --bare```

* 在开发者机器上推送到上面的仓库

* 其他开发者从服务器仓库克隆

## git-shell

## gitosis

优点:

* 文件 authorized_keys 由 gitosis 自动管理，增删用户不必每次都要登录服务器修改 authorized_keys

* 不必每次创建新项目都要登录服务器创建裸仓库

* 完全的 SSH 方式缺少必要权限管理，gitosis 可以进行适当的权限管理

### 安装 gitosis

```shell
$ apt-get install python-setuptools
$ git clone https://github.com/tv42/gitosis.git
$ cd gitosis
$ sudo python setup.py install
```

### 初始化

#### 服务器端

默认 Gitosis 会把 /home/git 作为存储所有 Git 仓库的根目录(/home/git/repositories),若已有 git
仓库在其他位置，可以设置软连接 ```$ ln -s /opt/git /home/git/repositories```

将 authorized_keys 文件改名备份，以后 authorized_keys 由 gitosis 自动管理

如果 git 用户的 login shell 之前设置为 git-shell，需要改回来，比如 ```/bin/bash```

假定用于初始化 gitosis 的公钥已在服务器 ```/tmp/id_rsa.pub```

初始化 gitosis

```
$ su git
$ cd ~
$ gitosis-init < /tmp/id_rsa.pub
Initialized empty Git repository in /home/git/repositories/gitosis-admin.git/
Reinitialized existing Git repository in /home/git/repositories/gitosis-admin.git/
$ chmod 755 /home/git/repositories/gitosis-admin.git/hooks/post-update
```

管理员开发者(用于初始化 gitosis 的公钥的所有者)

* 克隆 gitosis-admin.git 管理仓库

* 在 gitosis.conf 中新建用于新项目 new_project 的组

* 提交并推送上一步的更改，这时的推送，会在服务器端自动创建名为 new_project.git 的裸仓库

* 添加其他开发者

* 将开发者本地的项目推动送到上面的裸仓库

此时，其他开发者就可以克隆和推送项目，进行正常的工作了。


## gitolite

认证是确定用户是谁，授权是决定该用户是否被允许做他想做的事情
