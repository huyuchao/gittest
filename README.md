# gittest
仅仅是为了测试git command

vim   点击insert 开始输入内容，点击esc 输入命令，保存退出。

:w    将缓冲区写入文件，即保存修改<br>
:wq   保存修改并退出<br>
:x    保存修改并退出<br>
:q    退出，如果对缓冲区进行过修改，则会提示<br>
:q!   强制退出，放弃修改<br>

touch <name> 创建文件

------------------------------------
git init  生成库

git add  <name> 添加文件

git add . 添加该目录下所有文件

git commit <name> 提交单个文件

git commit -m "one file" test.txt  提交单个文件  

git commit -m "提交说明"  提交全部修改文件

git commit -a 提交全部修改文件 会打开一个vim编辑提交信息

git commit -a -m "msg"  提交全部修改文件


git remote add gittest https://github.com/huyuchao/gittest.git     添加远程仓库
gittest 是别名
作用：将https://github.com/huyuchao/gittest.git 起名为gittest，以后提交可以直接用gittest代替
调用一次就可以

git rename oldname newname 修改别名


git push gittest master  将本地代码提交到远程服务器

如果远程代码被修改，会有如下错误:
error: failed to push some refs to 'https://github.com/huyuchao/gittest.git'

Updates were rejected because the remote contains work that you do not have locally. 
This is usually caused by another repository pushing to the same ref. 
You may want to first integrate the remote changes
(e.g., 'git pull ...') before pushing again.

解决方法：更新本地代码


git pull gittest master  更新远程服务器代码到本地

git pull https://github.com/huyuchao/gittest.git master 更新远程服务器代码到本地


git config -l  或者是git config --list  查看配置信息

git status   查看项目状态信息

git branch   查看项目分支

git checkout -b <new_branch> 建立新的分支new_branch

git checkout <branch>  切换分支branch

git branch -d <branch>  删除分支 branch

git merge <branch>  合并分支到当前的分支

git log 退出  ctrl+c 或者 直接输入q


编辑 ignore 忽略文件：<br>
1，通过命令行<br>
2，通过编写.gitignore 文件   .gitignore在项目根目录创建<br>
3，.git/info/exclude  .git 目录下 exclude文件中编辑<br>
4，core.excludesFile  全局配置<br>

cat .git.info.exclude 查看忽略内容
vim .git/info/exclude 编辑忽略内容

编写规则：

*.a           忽略所有以.a为扩展名的文件    <br>
!lib.a        但是名为lib.a的文件或目录不要忽略，即使前面设置了对*.a的忽略<br>
/TODO         只忽略此目录下的TODO文件，子目录中的TODO文件不忽略<br>
build/        忽略所有build目录下的文件，但如果是名为build的文件则不忽略<br>
doc/*.txt     忽略文件如doc/notes.txt，但是文件如doc/server/arch.txt不忽略<br>




换行符windows和linux不一致
warning: LF will be replaced by CRLF in test.txt.
解决方法：
git config --global core.autocrlf false   自动换行转换取消


git push 每次都要输入用户名和密码：
解决方案：<br>
1，C:\Users\Administrator  下创建.git-credentials 文件<br>
2，用记事本打开这文件输入，如果用户名中有@，那么使用%代替：<br>
   https://{username}:{password}@github.com<br>
3，配置global<br>
   git config --global credential.helper store    表示永久存储

   git config credential.helper 'cache --timeout =300' 表示5分钟有效时间


vim 不能保存：No write since last change (add ! to override)
解决方法: 通过!强制存盘  :w!


乱码：

设置git gui的界面编码
git config --global gui.encoding utf-8

设置 commit log 提交时使用 utf-8 编码，可避免服务器上乱码，同时与linux上的提交保持一致！
git config --global i18n.commitencoding utf-8







