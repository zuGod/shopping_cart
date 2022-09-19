#创建gitTest文件夹

```
mkdir gitTest
```

#进入gitTest

```
cd gitTest
```

#初始化本地仓库

```
git init
```

#git配置

```
git config --global user.name "YName"
git config --global user.email "..@...com"
```

\#创建helloGit.txt文件

```
touch helloGit.txt
```

#添加提交helloGit.txt到暂存区的命令

```
git add helloGit.txt

git status
```

#添加helloGit到本地仓库命令

```
git commit -m helloGit.txt
```

#将远程版本库clone到本地

```
git clone 远程版本库地址
```

#为创建的本地仓库添加远程仓库命令

```
git remote add 远程仓库名 远程仓库地址
```

#将本地内容推从到远程仓库

```
git push 远程仓库名 本地分支名 远程分支名

//另一种方法 -u参数的作用是，建立本地master分支和远程master分支之间的对应关系,下次如果再推送，就可以忽略远程分支名了

git push -u 远程仓库名 本地分支名 远程分支名
```

```
//初次推送
git push -u origin master master
//再次推送
git push origin master
```

#拉取远程仓库内容到本地

```
git pull 远程主机名 远程分支名:本地分支名

//强制拉取 使用远程分支的修改，覆盖本地分支的修改
git pull 远程主机名 远程分支名:本地分支名 -f
```

#分支切换

```
git checkout 分支名
```

#创建新的分支

```
git branch 新的分支名字
```

#创建新分支的时候同时切换

```
git checkout -b 新的分支名字
```

#删除本地本地分支

```
git branch -D 需要删除的分支名字
```

#删除远程分支

```
//通过推送空分支到远程分支
git push 远程主机名 ：远程分支
//通过delete参数删除远程分支
git push 远程主机名 --delete 远程分支名
```

#合并本地分支

```
//当前处于分支合并到另一个分支
git merge 需要合并的分支（另一个分支）

//非快进式合并
git merge --no-ff 需要合并的分支（另一个分支）
```

#