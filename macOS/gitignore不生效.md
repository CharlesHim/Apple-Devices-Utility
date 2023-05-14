
## 第一种方法  
`.gitignore`中已经标明忽略的文件目录下的文件，git push 的时候还会出现在 push 的目录中，或者用`git status`查看状态，想要忽略的文件还是显示被追踪状态。原因是因为在 git 忽略目录中，新建的文件在 git 中会有缓存，如果某些文件已经被纳入了版本管理中，就算是在`.gitignore`中已经声明了忽略路径也是不起作用的，这时候我们就应该先把本地缓存删除，然后再进行git的提交，这样就不会出现忽略的文件了。  

**解决方法: git 清除本地缓存（改变成未 track 状态），然后再提交**  

```shell
git rm -r --cached .
git add .
git commit -m 'update .gitignore'
git push -u origin master
```

需要特别注意的是：  
1. `.gitignore`只能忽略那些原来没有被track的文件，如果某些文件已经被纳入了版本管理中，则修改`.gitignore`是无效的。  
2. 想要`.gitignore`起作用，必须要在这些文件不在暂存区中才可以，`.gitignore`文件只是忽略没有被 staged (cached) 文件,对于已经被 staged 的文件，加入`.gitignore`文件时一定要先从 staged 移除，才可以忽略。  

## 第二种方法

在每个 clone 下来的仓库中手动设置不要检查特定文件的更改情况。  

```shell
git update-index --assume-unchanged PATH //在PATH处输入要忽略的文件
```

### 在使用`.gitignore`文件后如何删除远程仓库中以前上传的此类文件而保留本地文件  
在使用 git 和 github 的时候，之前没有写`.gitignore`文件，就上传了一些没有必要的文件，在添加了`.gitignore`文件后，就想删除远程仓库中的文件却想保存本地的文件。这时候**不可以直接使用**`git rm directory`，这样会删除本地仓库的文件。可以使用`git rm -r –cached directory**`来删除缓冲，然后进行 commit 和 push，这样会发现远程仓库中的不必要文件就被删除了，以后可以直接使用`git add -A`来添加修改的内容，上传的文件就会受到`.gitignore`文件的内容约束。