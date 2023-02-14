## Git测试1-2

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

$ git fetch all
$ git fetch origin 分支名
```

- 推送本地仓库关联远程仓库

```
$ git init
$ git remote add origin git@...
$ git push -u origin master
$ git branch --set-upstream-to=origin/dev    指定本地分支与远程origin分支链接
$ git remote remove origin  断开本地git链接
$ git remote rm origin
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
$ git branch --unset-upstream
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
$ git commit --allow-empty -m ''  空提交
```

##### Git push

```
$ git push origin    将当前分支推送到origin主机的对应分支。吐过当前分支只有一个追踪分支，可省略主机名
$ git push -u origin master/other    将本地的分支推送到origin主机，同时指定origin为默认主机，后面可直接使用 $ git push
$ git push -f  强制推送
```

+ 产看当前仓库状态

```
$ git status
```

+ 查看修改的内容

```
$ git diff '文件名'
```

##### git log

```
$ git log
$ git log --pretty=oneline    详细的log日志
$ git log --pretty=format:'%h: %s'
$ Q  退出
$ git reflog  记录所有分支每一次命令
$ git reflog --date=iso  以标准时间展示所有分支的每一次命令
$ git log --graph --pretty=oneline --abbrev-commit  查看分支的合并情况
```

##### git reset

```
$ git reset --hard HEAD^/版本号    重置stage区和工作目录
$ git reset --soft HEAD^    保留工作区，并把重置HEAD所带来新的差异放进暂存区
```

+ 撤销工作区修改

```未使用 git add 缓存代码
$ git checkout -- '文件名'
$ git checkout .
```

```已使用 git add 缓存代码
$ git reset --mixed 文件退出暂存区，但是保留修改
$ git reset HEAD '文件名'
$ git reset HEAD .
```

```已使用 git commit 提交了代码
$ git reset --soft HEAD^
$ git reset --hard HEAD^
$ git reset --hard commitId
```

##### 创建与合并分支

* 创建并切换分支

```
$ git branch 分支名
$ git checkout 分支名
$ git checkout -b 分支名    -b 参数表示创建并切换

$ git checkout -b feature/分支名 origin/master
```

* 产看分支

```
$ git branch
$ git branch -l    查看本地分支
$ git branch -r    查看远程分支
$ git branch -a    查看本地和远程所有分支
$ git branch -vv  查看本地分支与远程分支
$ git branch -u origin/远程分支名  将本地分支与远程分支关联起来
$ git branch --unset-upstream  撤销本地分支与远程分支的映射关系
$ git branch -m 当前分支名 重命分支名   重命名本地分支
```

##### git rebase
```
$ git rebase -i commit哈希值
1：i  进入编辑
    p (pick): 保留改commit
    r (reword): 保留该commit，但是需要修改该commit的注释
    e (edit): 保留该commit，但我要停下来修改该提交(不仅仅修改注释)
    s (squash): 将该commit合并到前一个commit
    f (fixup): 将该commit合并到前一个commit，但是不要保留提交的注释信息
    x (exec): 执行shell命令
    d (drop): 丢弃该commit
2：ESC  退出操作
3：:wq  保存并退出

$ git rebase --edit-todo 再次进入编辑

$ git rebase --continue  进入下一个界面，可以更新commit这是一个不可改的步骤
1: :wq  保存并退出

$ git push -f

```

##### git merge

```
$ git merge 分支名
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
$ git checkout -b 分支名 最近commit哈希值
$ git push origin -u 分支名
```