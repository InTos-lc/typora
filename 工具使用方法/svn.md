# SVN

## linux SVN客户端

[Linux环境下使用SVN命令行提交文件操作指南 - OSCHINA - 中文开源技术交流社区](https://my.oschina.net/emacs_8766694/blog/17214064)

#### 当首次使用时

1. 检出命令
   - svn checkout URL [PATH]
2. 添加命令用于将新文件或目录添加到版本库中
   - svn add [PATH]
3. 提交命令用于将本地更改上传到版本库
   - svn commit [PATH] -m "提交信息"
4. 更新命令用于同步本地文件与版本库中的最新更改
   - svn update [PATH]
5. 删除命令用于从版本库中移除文件或目录
   - svn delete [PATH] --force
6. 状态命令（Status）用于查看本地文件与版本库之间的差异
   - svn status [PATH]

##### 更改svn服务器地址

1. **windows**下更改![svn_更改服务器地址](E:\截图\svn_更改服务器地址.png)

2. 选择路径

   ![svn_更改服务器地址选择路径](E:\截图\svn_更改服务器地址选择路径.png)