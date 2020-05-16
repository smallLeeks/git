## Git

##### git两种链接方式：http和ssh

这两种方式的主要区别在于：使用 `http url (git clone/pull)` 对于初学者会比较方便

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

##### 创建 ssh key

- 本地 ssh-key 创建

```
$ ssh-keygrn -t rsa -C "email地址"
```

- .ssh 文件地址

```
C:\Users\13543\.ssh
```

##### http  互转  ssh

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