# 测试本地git添加远程库到github
Linux下把上传命令的origin改成o才行，否则会出现奇怪的不能上传的错误
```
git remote add o git@github.com:BewareMyPower/learninggit.git
git push -u o master
```

修改README.md后重新上传文件出现问题，解决方式是添加强制上传选项
`git push o master -f`
