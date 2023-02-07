# <center>git 命令手册</center>

### 查看git信息
```
git
```

### 查看git版本
```
git --version
```

### 设置命令别名
```
git config --global alias.别名 命令
```

### 存储凭证
```
git config --global credential.helper wincred
```

### 文件清除
```
要清除文件列表
git clean -n

真正删除
git clean -f

连.gitignore中忽略的文件也清除
git clean -x
```

### 查看某一文件修改的信息
```
git blame filename
git blame -L 起始行号,结束行号 filename
```

### git配置
```
查看配置信息
git config --list

设置用户名
git config --global user.name "your name"

设置邮箱
git config --global user.email "email@example.com"

解决windows以\r\n而linux\n换行造成冲突问题
error: LF will be replaced by CRLF
git config --global core.autocrlf true

允许提交包含混合换行符的文件
git config --global core.safecrlf false
```

### 查看修改历史
```
git history
```

### 查看当前代码仓库状态
```
git status
```

### 代码仓库初始化
```
git init
```

### 查看操作日志
```
git log

git log --pretty=format:'%h %ad | %s%d[%an]' --graph --date=short
```

### 将工作区文件提交到暂存区
```
提交某一个文件
git add [filename] 

提交所有修改文件
git add .
```
### 将暂存区文件标记删除
```
git rm filename
```

### 将暂存区文件移动
```
git mv oldFilename newFilename
```

### 将暂存区版本回退
```
回退一个版本
git reset --hard HEAD^

回退两个版本
git reset --hard HEAD^^
```

### 工作区与暂存区比较
```
git diff
```

### 暂存区与代码仓库比较
```
git diff --cached
```

### 将暂存区文件提交到代码仓库
```
git commit -m "content"
```

### 直接将工作区文件提交到代码仓库
```
git commit -am "content"
```

### 将一个文件分次提交
```
git commit -p
```

### 从远程仓库克隆到本地
```
git clone 远程仓库地址
```

### 关联远程仓库
```
查看关联的远程仓库信息
git remote -v

远程关联,如果是使用git clone克隆来的,会自动关联
git remote add origin 远程仓库的地址

删除关联
git remote rm origin
```

### 将本地代码仓库的内容提交到远程仓库
```
远程仓库不是空的
git push origin master 

远程仓库是空的
git push -u origin master
```
