## Git

##### git两种链接方式：http 和 ssh

这两种方式的主要区别在于：使用 `http url (git clone/pull)` 对于初学者会比较方便

```
$ mkdir ''
$ cd ''
$ pwd
$ git init
```

> http模式

- 每次 `fetch` 和 `push` 都要输入账号和密码

```
$ git clone/pull https://...
```

> ssh

- 更方便、更安全

- 先添加 `ssh key`

```
$ git clone/pull git@...
```

##### Git 配置

```
$ git config --global user.name ''
$ git config --global user.email ''
```

##### 创建 ssh key

- 本地 ssh-key 创建

```
$ ssh-keygrn -t rsa -C "email地址"
```

- .ssh 文件地址

```
C:\Users\13543\.ssh
```

##### http 互转 ssh

- 查看当前origin

```
$ git remote -v
```

- 移除当前的origin

```
$ git remote origin https:/git@...    
```

- 添加新的方式origin

```
$ git remote add origin https:/git@...
```

- 设置上游要跟踪的分支，自动执行一次push

```
$ git push --set-upstream origin master
```

##### Git 提交

+ 提交

```
$ git add .
$ git commit -m ''
$ git push origin master/other
```

+ 产看当前仓库状态

```
$ git status
```

+ 查看修改的内容

```
$ git diff '文件名'
```

+ 查看日志

```
$ git log
$ git log --pretty=oneline
```

+ 版本回退

```
$ git reset --hard HEAD^/版本号    重置stage区和工作目录
$ git reset --soft HEAD^    保留工作区，并把重置HEAD所带来新的差异放进暂存区
$ git reflog    记录每一次命令
```