[(4 封私信) Git使用教程,最详细，最傻瓜，最浅显，真正手把手教 - 知乎](https://zhuanlan.zhihu.com/p/30044692)

[Git教程- - jack_Meng - 博客园](https://www.cnblogs.com/mq0036/collections/106)

## 上传远程仓库失败报错信息

git push origin master
kex_exchange_identification: Connection closed by remote host
Connection closed by 198.18.0.10 port 22
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.

1. git remote -v 查看是否由远程地址

2. ls ~/.ssh 查看是否由SSH密钥 有的话将密钥添加到GITHUB SSH中

3. 使用GitHub的443 SSH端口 将下面的代码添加到路径中的文件中去

   ```
   ~/.ssh/config
   
   内容：
   
   Host github.com
   
   Hostname ssh.github.com
   
   Port 443
   
   User git
   ```

   测试 ssh -T git@github.com

4. 使用HTTPS

   ```
   git remote set-url origin https://github.com/用户名/仓库名.git
   git push origin master
   ```

   