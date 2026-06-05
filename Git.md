## Git

### 上传远程仓库失败解决办法

[完美解决 git push 失败："Connection reset" 与 "Failed to connect" 终极指南 · Weidong's Blog](https://www.wdblok.vip/posts/完美解决git-push失败connection-reset与failed-to-connect终极指南/)

1. fatal: unable to access 'https://github.com/InTos-lc/typora.git/': Recv failure: Connection was reset

​	使用SSH进行上传

 git remote set-url origin git@github.com:InTos-lc/typora.git

将Intos-lc和typora.git替换成相应的用户名和仓库名

 **小技巧***：你可以用`git remote -v` 命令来检查远程地址是否已经成功修改为 `git@...` 的格式。

### 问题1：SSH 连接超时

如果 `ssh -T git@github.com` 连接超时，可以尝试：



```bash
# 设置 SSH 连接超时时间
ssh -o ConnectTimeout=10 -T git@github.com

# 或者使用代理（如果你有代理的话）
ssh -o ProxyCommand="nc -X connect -x 127.0.0.1:7890 %h %p" -T git@github.com
```

### 问题3：多个 SSH 密钥管理

如果你有多个 GitHub 账号或多个 SSH 密钥，可以创建 `~/.ssh/config` 文件：

```bash
# GitHub 账号1
Host github.com-account1
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_account1

# GitHub 账号2
Host github.com-account2
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_account2
```

然后使用对应的 Host 名称：

```bash
git remote set-url origin git@github.com-account1:username/repo.git
```