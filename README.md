# gittest
仅仅是为了测试git command

vim   点击insert 开始输入内容，点击esc 输入命令，保存退出。

:w    将缓冲区写入文件，即保存修改<br>
:wq   保存修改并退出<br>
:x    保存修改并退出<br>
:q    退出，如果对缓冲区进行过修改，则会提示<br>
:q!   强制退出，放弃修改<br>

touch <name> 创建文件

git merge合并策略：  这四种都是直接合并代码，并不能合并某一次的提交

git merge-ours
合并使用本地版本，抛弃他人版本。参见 git merge 的ours合并策略

git merge-recursive
针对两个分支的三向合并。参见 git merge 的recursive合并策略

git merge-resolve
针对两个分支的三向合并。参见 git merge 的resolve合并策略

git merge-subtree
子树合并。参见 git merge 的 subtree 合并策略

合并单个commit

<font color="red">
git cherry-pick 4da2f54  合并某一次的提交到当前分支   4da2f54为提交的commit_id值<br/>
git cherry-pick --no-commit  4da2f54   合并但不自动提交
</font>

合并多个连续的commit，格式：1,git cherry-pick A..B  &nbsp;&nbsp;&nbsp;&nbsp;2,git cherry-pick A^..B  
1，
git cherry-pick A..B 合并从A到B  commit的内容（不包含A）<br/>
git cherry-pick --no-commit  956946f..da0e179<br/>
2，
git cherry-pick A^..B  合并从A到B  commit的内容（包含A）<br/>
git cherry-pick --no-commit  956946f^..da0e179<br/>


------------------------------------

当我们操作github或者gitlab上的项目时，我们需要身份证明也就是SSH Key。<br>
1，每次操作带上我们的用户名和密码<br>
2，在本地保存一份key，在github或者gitlab上配置一个key<br>

操作步骤：<br>
1，打开git bash，输入命令ls -al ~/.ssh<br>
2，ssh-keygen -t rsa -C "xxxx@xxxxxx.com"<br>
3,C:\Users\Administrator\.ssh 目录下打开id_rsa.pub文件，并且复制全部内容<br>
4，在你的gitlab或者github的账户，打开SSH key标签<br>
5，add you key<br>


git clone https://github.com/huyuchao/Study_Yii.git master

git init  生成库

git add  <name> 添加文件

git add . 添加该目录下所有文件

git commit <name> 提交单个文件

git commit -m "one file" test.txt  提交单个文件  

git commit -m "提交说明"  提交全部修改文件

git commit -a 提交全部修改文件 会打开一个vim编辑提交信息

git commit -a -m "msg"  提交全部修改文件

git rm 我的文件

git rm -r 我的文件夹
此处-r表示递归所有子目录，如果你要删除的，是空的文件夹，此处可以不用带上-r

----------------------------------------------------------------------------------

git remote add gittest https://github.com/huyuchao/gittest.git     添加远程仓库
gittest 是别名
作用：将https://github.com/huyuchao/gittest.git 起名为gittest，以后提交可以直接用gittest代替
调用一次就可以

git rename oldname newname 修改别名

git push gittest master  将本地代码提交到远程服务器

----------------------------------------------------------------------------------

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

-----------------------------------------------------------------------------
遇到的问题：
The authenticity of host *** can’t be established  本地电脑key有变化<br>

修改/etc/ssh/ssh_config文件（或$HOME/.ssh/config）中的配置，添加如下两行配置：<br>
StrictHostKeyChecking no<br>
UserKnownHostsFile /dev/null<br>

修改好配置后，重新启动sshd服务即可，命令为：/etc/init.d/sshd restart （或 service sshd restart ）


换行符windows和linux不一致<br>
warning: LF will be replaced by CRLF in test.txt.<br>
解决方法：<br>
git config --global core.autocrlf false   自动换行转换取消<br>


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


-------------------------------------------------------------------


    /trunk：开发主线，相当于Git中的Master分支。

    /branches：支线副本，相当于Git中的其余分支。

    /tags：标签，与Git中的标签一样。



克隆svn版本库的全部内容

    git svn clone <svn repository>

克隆具有标准结构的svn版本库

    git svn clone –s <svn repository>

克隆非标准结构的svn版本库

    git svn clone –T <trunk path>\

                       -b <branch path>\

                      -t <tag path>\

                      <svn repository>

克隆具有标准结构的svn版本库中的某个版本

    git svn clone –s –r 1111

克隆具有标准结构的svn版本库，并对svn中的分支添加前缀

    git svn clone –s –prefix svn/<svn repository>

从上游svn版本库中获得更新的内容，并依稀在本地git版本库中编辑本地分支

    git svn rebase

把修改变化退回上游的svn版本库

    git svn dcommit

列出所有将推出上游svn版本库的提交

    git svn dcommit –n

显示svn历史记录

    git svn log

显示文件中哥哥部分的svn的修改者及相关提交信息

    git svn blame <some file>

上面就是将svn迁移git的过程。




