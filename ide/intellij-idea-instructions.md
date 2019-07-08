# Intellij IDEA 使用记录

## 设置默认编码

Search "encoding" in settings, set as UTF-8.

## 导入和打开项目

若指定的项目根目录下有 .idea 目录，说明该项目已有 IDEA 相关设置，如果不想修改这些配置，那么就打开(Open)。

若指定的项目根目录下没有 .idea 目录，说明该项目没有 IDEA 相关设置，导入(Import)可以在导入过程中对项目进行设置。

尽管如此，IDEA 可以自动检测项目的模型，并提示用户设置。

## 创建 Maven 项目并集成 Git 版本控制

步骤如下：

* 从 Archetype 创建一个 Maven 项目

* 在 Project Structure 中设置项目

* 修改 pom.xml 内容

* 启用 Git 版本控制

* 创建 .gitignore 并添加内容

* 创建并编写 LICENSE 和 README


## 路径

在 IDEA 中默认的当前目录是项目的根，而不是模块的根
