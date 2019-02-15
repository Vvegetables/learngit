### git图标
| Ⅰ | Ⅱ | Ⅲ | Ⅳ | Ⅴ | Ⅵ | Ⅶ | Ⅷ | Ⅸ | Ⅹ |
| :--------: | :---------: | :---------: | :---------: | :---------: | :---------:| :---------: | :-------: | :-------:| :------:|
| 算法[:pencil2:](#pencil2-算法) | 操作系统[:computer:](#computer-操作系统)|网络[:cloud:](#cloud-网络) | 面向对象[:couple:](#couple-面向对象) |数据库[:floppy_disk:](#floppy_disk-数据库)| Java [:coffee:](#coffee-java)| 系统设计[:bulb:](#bulb-系统设计)| 工具[:hammer:](#hammer-工具)| 编码实践[:speak_no_evil:](#speak_no_evil-编码实践)| 后记[:memo:](#memo-后记) |

### git配置
	1、设置全局名字和email地址
	git config --global user.name "your name"
	git config --global user.email "email@example.com"
	2、颜色配置
	git config --global color.ui true
	3、.gitignore配置
	所有配置文件可以直接在线浏览：https://github.com/github/gitignore

	忽略文件的原则是：

	1.忽略操作系统自动生成的文件，比如缩略图等；
	2.忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件；
	3.忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。
	
	强制添加被ignore规则屏蔽的文件：
	git add -f app.class
	git check-ignore 检查命令
	git check-ignore -v app.class

	设置别名：
	git config --global alias.st status
	git config --global alias.ci commit
	git config --global alias.br branch

	git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

### 2、把这个目录变成Git可以管理的仓库
	git init

### 3、提交文件
	git add filename

### 4、上传提交
	git commit -m 'commit message'

### 5、查看仓库的状态
	git status

### 6、对比文件的差异
	git diff filename
	git diff HEAD -- readme.txt

### 7、查看版本控制的历史记录
	git log
如果嫌输出信息太多，看得眼花缭乱的，可以试试加上--pretty=oneline参数

查看分支的合并情况
	git log --graph --pretty=oneline --abbrev-commit

查看分支合并图
	git log --graph

### 8、版本表示方法
当前版本：HEAD
上一个版本：HEAD^
上上个版本：HEAD^^
...
上100个版本：HEAD~100

### 9、回退版本
	git reset
	git reset --hard HEAD^

### 10、重返未来，回退到历史版本之后，想重新回退到最新版本
	git reset --hard commit_id

为什么Git比其他版本控制系统设计得优秀，因为Git跟踪并管理的是修改，而非文件。

### 11、撤销修改
	git checkout -- readme.txt
	git checkout -- file命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令，我们在后面的分支管理中会再次遇到git checkout命令。

### 12、远程仓库

	12.1 创建ssh-key
		ssh-keygen -t rsa -C "youremail@example.com"			
	12.2 将一个已有本地仓库与远程仓库关联
		git remote add origin git@github.com:Vvegetables/learngit.git
		git push -u origin master

### 13、克隆仓库
	git clone git@github.com:Vvegetables/learngit.git

### 14、分支管理：
创建dev分支，然后切换到dev分支
	git checkout -b dev
	==
	git branch dev
	git checkout dev

查看当前所处分支
git branch

### 15、合并分支：
	git merge dev

### 16、删除分支
	git branch -d dev

### 17、分支管理策略
	fast forward 合并看不出来曾经做过合并
	强制不使用fast forward模式做合并。
	git merge --no-ff -m "merge with no-ff" dev


### 18、储藏工作现场
	git stash
	
	bug修改：
		在出现问题的分支上创建临时分支
		git checkout -b issue-101
		修改问题之后，切换到master分支，并完成合并，最后删除issue-101分支。
		git add readme.txt
		git commit -m "fix bug 101"
		git checkout master
		git merge --no-ff -m "merge bug fix 101" issue-101

	查看存储的工作区
	git stash list

	恢复工作现场
	git stash apply
	git stash drop

	git stash pop

	feature 分支
	添加一个新功能时，你肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支。

	强行删除一个分支
		git branch -D feature-vulcan


### 多人写作
	查看远程仓库信息
	git remote
	git remote -v 查看更详细的信息

	创建远程origin的dev分支到本地
		git checkout -b dev origin/dev

	如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令
	git branch --set-upstream-to <branch-name> origin/<branch-name>。

	将历史版本变成一条直线
	git rebase

### 标签管理：
	tag == commitid

	查看所有标签
	git tag

	创建一个新的标签
	git tag tagname

	为相应的commitid打上标签
	-a 指定标签名字
	-m 指定说明文字
	git tag v0.9 commitid

	查看标签信息
	git show tagname

	注意：标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签。


	删除标签
	git tag -d tagname
	因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。

	如果要推送某个标签到远程，使用命令git push origin <tagname>：

	或者，一次性推送全部尚未推送到远程的本地标签：
	git push origin --tags


	如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：
	git tag -d v0.9
	然后，从远程删除。删除命令也是push，但是格式如下：
	git push origin :refs/tags/v0.9


在GitHub上，可以任意Fork开源仓库
自己拥有Fork后的仓库的读写权限
可以推送pull request给官方仓库来贡献代码
