## Git

##### git两种链接方式：http 和 ssh

git全局配置

```
$ git config --system --list 查看系统配置
$ git config --local --list 查看当前仓库配置
$ git config --global -list 查看Git所有配置
$ git config --global --uset user.name 删除全局配置项
$ git config --global --edit 编辑配置文件

手动设置config
$ git config --global user.name ''
$ git config --global user.email ''
```

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

- 拉取远程仓库

```
$ git clone/pull git@...

$ git fetch origin 分支名
```

- 推送本地仓库关联远程仓库

```
$ git init
$ git remote add origin git@...
$ git push -u origin master
$ git branch --set-upstream-to=origin/dev    指定本地分支与远程origin分支链接
$ git remote remove origin  断开本地git链接
```

##### Git 配置

+ 全局设置账号密码

```
$ git config --global user.name ''
$ git config --global user.email ''
```

+ 查看账号密码

```
$ git config user.name
$ git config user.email
```

+ 记住密码

```
$ git config --global credential.helper store
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

- 查看远程库的信息

```
$ git remote
$ git remote -v
```

- 移除当前的origin

```
$ git remote remove origin
```

- 添加新的方式origin

```
$ git remote add origin https:/git@...
```

- 设置上游要跟踪的分支，自动执行一次push

```
$ git push --set-upstream origin master
```

##### Git add

```
$ git add .    提交新文件（new）和被修改（modified）文件，不包括被删除（deleted）的文件
$ git add -u    提交被修改（modified）和被删除（deleted）文件，不包括新文件（new）
$ git add -A    提交所有变化
```

##### Git commit
```
$ git commit -m '' 或者 git commit [file1] [file2] -m '' 提交暂存区到本地仓库
$ git commit -am '' 设置修改文件不需要执行git add，直接提交
```

##### Git push
+ push 的区别

```
$ git push origin    将当前分支推送到origin主机的对应分支。吐过当前分支只有一个追踪分支，可省略主机名
$ git push -u origin master/other    将本地的分支推送到origin主机，同时指定origin为默认主机，后面可直接使用 $ git push
```

+ 查看当前仓库状态

```
$ git status
```

+ 查看修改的内容

```
$ git diff '文件名'
```

+ 查看提交日志

```
$ git log
$ git log --pretty=oneline    详细的log日志
$ git log --pretty=format:'%h: %s'
$ Q    退出
```

+ 版本回退

```
$ git reset --hard HEAD^/版本号    重置stage区和工作目录
$ git reset --soft HEAD^    保留工作区，并把重置HEAD所带来新的差异放进暂存区
$ git reflog    记录所有分支每一次命令
$ git reflog --date=iso    以标准时间展示所有分支的每一次命令
```

+ 撤销工作区修改

```
$ git checkout '文件名'
```

##### 创建与合并分支

* 创建并切换分支

```
$ git branch 分支名
$ git checkout 分支名
$ git checkout -b 分支名    -b 参数表示创建并切换
$ git checkout -b feature/分支名 origin/master
```

* git branch

```
$ git branch
$ git branch -l    查看本地分支
$ git branch -r    查看远程分支
$ git branch -a    查看本地和远程所有分支
$ git branch -vv  查看本地分支与远程分支
$ git branch -u origin/远程分支名  将本地分支与远程分支关联起来
$ git branch --unset-upstream  撤销本地分支与远程分支的映射关系
```

* git merge

```
$ git merge 分支名  合并指定分支到当前分支
```

+ 重命名本都分支

```
$ git branch -m dev xxx
```

+ 重命名远程分支

```
$ git branch -d -r 分支名
$ git push 本地的分支
```

* 删除分支

```
$ git branch -d 分支名  git beanch -delete 分支名  删除本地分支
$ git push origin --delete 分支名    删除远程分支

$ git branch -d 会在删除钱检查merge状态（如果该分支有提交未进行合并，则会删除失败）
$ git branch -D 是git branch --delete --force的简写，它会强制删除分支（有提交未进行合并，也会删除成功）
```

+ 恢复已删除的远程分支

```
$ git reflog --date=iso
$ git checkout -b 分支名 最近commitID
$ git push origin -u 分支名
```

* 查看分支的合并情况

```
$ git log --graph --pretty=oneline --abbrev-commit
```