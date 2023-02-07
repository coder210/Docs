# <center>git相关信息<center>

# github上忽略文件
git的.gitingore文件是用于git提交文件时忽略一些扩展名的文件,例如: c语言项目提交到github上时,不应该上传.exe和.project等文件,那么我们就在生成的.exe文件上新建一个.gitingore文件并写下如下内容.
```
.exe 忽略exe文件
.project 忽略project
```
gitingore官网模板: [https://github.com/github/gitignore][gitingore]
   
   
# gitconfig文件的查找
.gitconfig文件存储了,git工具的配置信息那么如何用**vim**打开它  
```
1.回到用户根目录
cd ~
2.打开.gitconfig文件
vim .gitconfig
```
   
# 每次需要输密码的麻烦
如何解决每次提交都要输入用户名和密码的问题,那就是使用**存储凭证**(看存储凭证命令即可),使用后设置一次用户名和密码,下次就再也不用输入了


# ssh协议
使用ssh协议,相当http协议来说更快,但是配置会更麻烦一些,因为它要配密钥.
生成密钥,执行``ssh-keygen``命令, 在~/.ssh文件夹下生成有一个公钥和私钥
.找到settings-> SSH and GPG keys这一项,点击New SSH Key按钮,将公钥的内容复制到文本框中,确定即可
如图:![ssh][ssh]


# commit时log信息格式化规范
格式化的好处就是你只要看行着,就知道某次提交的目的是什么,我采用的是**Aggular规范**,格式如下:
```
<type>(<scope>): <subject>
// 空一行
<body>
// 空一行
<footer>
```
head是必须的,body和footer都可以省略.
不管哪一部分,任何一行不要超过72个字符,会导致换行影响排版

### header
header部分只有一行,包括三个字段: **type**(必需), **scope**(可选), **subject**(必需)

type: 用于说明commit的类别,只允许使用下面7个标识
-- feat: 新功能(feature)
-- fix: 修补bug
-- docs: 文档
-- style: 格式(不影响代码运行的变动)
-- refactor: 重构
-- test: 增加测试
-- chore: 构建过程或辅助工具的变动

scope: 用于说明**commit**影响的范围, 比如数据层,控制层,视图层

subject: 是commit 目的简短描述,不超过50个字符
1. 以动词开动,使用第一人称现在时态
2. 第一个字母小写
3. 结尾不加英文句号

### body
body部分是对本次commit的详细描述,可以分成多行
1. 以动词开动,使用第一人称现在时态
2. 应该说明代码变动的动机,以及与以前行为的对比

### Footer
1. 不兼容变动, 则footer部分以**BREAKING CHANGE**开头, 后面是对变动描述,理由和迁移
```
BREAKING CHANGE: isolate scope bindings definition has changed.

    To migrate the code follow the example below:

    Before:

    scope: {
      myAttr: 'attribute',
    }

    After:

    scope: {
      myAttr: '@',
    }

    The removed `inject` wasn't generaly useful for directives so there should be no code using it.
```
2. 如果当前commmit对针某个issue,那么可以在footer部分关闭这个issue
```
// 关闭一个
Closes #234
// 关闭多个
Closes #234, #254, , #325
```
<br>
<br>
<br>

[参考文章:http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html][ruanyifeng]

<!-- 引用链接 -->
[gitingore]: https://github.com/github/gitignore
[ssh]: ./images/ssh.png
[ruanyifeng]: http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html
