# 测试本地git添加远程库到github
Linux下把上传命令的origin改成o才行，否则会出现奇怪的不能上传的错误
```
git remote add o git@github.com:BewareMyPower/learninggit.git
git push -u o master
```

找到了原因, 打开.git/config文件，可以看到
> [branch "master"]  
> 	remote = o  
> 	merge = refs/heads/master  

git init默认生成的配置文件中，master分支的remote属性是o而非origin

修改README.md后重新上传文件出现问题，解决方式是添加强制上传选项
`git push o master -f`

# 测试github多账号切换
```
ssh-keygen -t rsa -f ~/.ssh/id_rsa_<name> -c <your-email>
```

根据自定义的`name`得到公钥`id_rsa_<name>.pub`和私钥`id_rsa_<name>`，把公钥的部分添加到对应仓库的SSH keys中。

最关键的就是编辑`~/.ssh/config`文件，对每个账号，添加如下代码：
```
Host <your-host>
    HostName <your-host-name>
    User git
    IdentityFile ~/.ssh/id_rsa_<name>
```

这里`your-host`和`your-host-name`都填的仓库地址（即git@后面的那一串），比如github就填`github.com`。

然后对于每个项目，设置单独的用户名和密码，需要进入git项目目录：
```
git config user.name <your-user-name>
git config user.email <your-user-email>
```

可以发现在`.git/config`文件中加上了：
```
[user]
	name = <your-user-name>
	email = <your-user-email>
```

因此直接修改该文件也行。
