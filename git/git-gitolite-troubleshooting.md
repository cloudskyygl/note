### FATAL: split conf set, gl-conf not present for 'some-project'

可能是因为远程仓库中文件 gl-conf 不存在，一般当创建新仓库时自动生成。可以从其他仓库复制一份到出问题的仓库目录中，并修改 gl-conf 中的项目名称
和数字序号，暂时这么叫吧

### 查看当前用户对仓库的权限

```
ssh gituser@gitserver
```
