学习资料链接：https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000

0 git中快捷键
	Ctrl+Ins 复制
	Shift+Ins 粘贴
	
1 git查看/修改用户名和邮箱
	1.1 查看
		查看用户名：git config user.name
		查看邮箱：   git config user.email
	1.2 修改(注意：git config命令用了--global参数，表示你这台机器上所有的Git仓库都会使用这个配置)
		修改用户名：   git config --global user.name "username"
		修改邮箱地址：git config --global user.email "email"
		
2 创建版本库
	2.1 到达某位置：cd /weizhi
		例子：到达F盘：cd /F
	2.2 查看某目录下具有的文件或目录：ls
		查看某目录下具有的文件或目录（包括隐藏的）：ls -ah
	2.3 新建一个目录：mkdir 目录名
		例子：新建一个名为learn git的目录：mkdir learngit
	2.4 显示当前目录：pwd
	2.5 git init。将某目录变成Git可以管理的仓库
	
3 将修改提交到存储库
	3.1 git add 某文件。将某文件的修改添加到暂存区
		git add .。添加新文件和被修改文件，不包括被删除文件
		git add -u。添加被修改文件和被删除文件，不包括新文件
		git add -A。添加所有变化，包括被修改文件，被删除文件和新文件
	3.2 git commit -m "xxx"。将暂存区里的更改提交到存储库,-m后面的是本次提交的说明
	3.3 git status。显示工作目录和暂存区的状态。使用此命令可以看到哪些修改被暂存可以提交了，哪些没有
	3.4 git diff。比较的是工作目录(Working tree)和暂存区域快照(index)之间的差异，也就是修改之后还没有暂存起来的变化内容
		git diff 某文件。比较的是某文件工作目录(Working tree)和暂存区域快照(index)之间的差异，也就是修改之后还没有暂存起来的变化内容
	3.5 cat <file>。 查看file文件内容
	
3 版本回退	
	3.1 git log。显示从最近到最远的提交日志(git log后日志过长最后显示(END)却回不到命令行时按q键)
		git log --pretty=oneline。--pretty=oneline将每条日志输出为一行
	3.2 git reset --hard commit_id。让HEAD指针指向commit_id
		HEAD表示当前版本
		HEAD^和HEAD~1表示上一个版本
		HEAD^^和HEAD~2都表示上上一个版本
		HEAD~100表示往上第100个版本
	3.3 git reflog。查看命令历史（提交命令和修改HEAD指针指向的命令），以便确定要回到未来的哪个版本

4 管理修改
	在工作区的修改只有添加到暂存区才能提交到存储库。
	
5 撤销修改
	5.1 git checkout -- <file>。让file文件回到最近一次git commit或git add时的状态。分两种状况：
		1)file文件自修改后还没有添加到暂存区，现在撤销修改就回到和版本库一模一样的状态
		2)file文件已经添加到暂存区，现在撤销修改就回到添加到暂存区后的状态
	5.2 git reset HEAD <file>。将file文件中已经添加到暂存区的修改回退到工作区
	5.3 撤销修改分三种情况：
		5.3.1 改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file
		5.3.2 不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了5.3.1的情况，第二步按5.3.1的步骤操作
		5.3.3 已经提交了不合适的修改到版本库但还没有推送到远程库时，想要撤销本次提交，参考3 版本回退 一节。

6 删除文件
	6.1 git rm和rm的区别
		用 git rm 来删除文件，同时还会将这个删除操作记录下来；
		用 rm 来删除文件，仅仅是删除了物理文件，没有将其从 git 的记录中剔除。

		直观的来讲，git rm 删除过的文件，执行 git commit -m "abc" 提交时，会自动将删除该文件的操作提交上去。

		而用 rm 命令直接删除的文件，单纯执行 git commit -m "abc" 提交时，则不会将删除该文件的操作提交上去，需要在执行commit的时候，多加一个-a参数。即rm删除后，需要使用git commit -am "abc"提交才会将删除文件的操作提交上去。
	6.2 当我们删除了工作区的文件后，发现是误删时，可以用git checkout -- <file>恢复。
	
7 添加远程库(git远程仓库)
	7.1 在github上创建一个新的git远程仓库
	7.2 git remote add <origin> <SSH>。将一个已有的本地仓库与新建的git远程仓库关联。其中SSH是关联的git远程库的SSH Key公钥，相当于地址。origin是添加后git远程库的名字(确切地说，是远程仓库在本地仓库的叫法，比如你和你爸都有各自的名字，但你叫你爸“爸爸”)，这也是Git默认的叫法，也可以改成别的。
	7.3 git push -u <origin> master。用git push命令把本地库的内容推送到远程，这里实际上是把当前分支master推送到远程。
		由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令：git push <origin> master
	7.4 在以后的推送和拉取时，直接用git push <origin> master即可，因为7.3中的-u参数已经把本地的master分支和远程的master分支关联起来
	7.5 Git如果使用SSH连接，在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入yes回车即可。所以，上面的7.3会得到需要你确认指纹信息的警告，输入yes回车即可。
	7.6 git remote。远程仓库查询
		git remote -v。远程仓库地址查询
	7.7 git remote rm <origin>。删除远程库和本地库的一个连接
	
8 从远程库克隆。
	克隆一个仓库，首先必须知道仓库的地址，然后使用git clone命令克隆:git clone <git远程库地址>
	Git支持多种协议，所以git远程库的地址不止一个，其中包括https和ssh。所以，有git clone <https>和git clone <SSH>。
	ssh支持的原生git协议速度最快。
	使用https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用ssh协议而只能用https。
	
9 创建和合并分支
	9.1 HEAD指向当前分支
	9.2 git branch。查看当前分支
		git branch <分支名>。创建新分支
		git checkout <分支名>。切换到分支
		git checkout -b <分支名>。创建新分支并切换到这个分支
		git merge <分支名>。将分支合并到当前分支
		git branch -d <分支名>。删除分支
	9.3 信息Fast-forward，代表这次合并是“快进模式”，也就是将当前分支直接指向要合并的分支的当前提交。因此，合并速度很快
	
10 解决冲突
	10.1  当我们无法自动合并分支时，往往要手动解决冲突，然后添加暂存区并提交（这也是和自动合并分支的不同，自动合并分支不用手动这个过程）。
	10.2 git status。这个命令也可以用来查看合并分支时冲突的文件。
	10.3 git log --graph。可以用来查看合并分支图。
	10.4 Linux命令vi在git中的一般应用过程：
		vi <文件名>。进入命令模式
		键i。进入输入模式，也称为编辑模式
		键Esc。回到命令模式。
		键:（英文冒号）。进入底层命令模式。
		键w。保存文件
		键q。推出程序（即推出vi这个命令执行的程序）
		
11 分支管理策略
	11.1 实际开发中，一般按以下原则进行分支管理：
		11.1.1 master分支非常稳定，仅用来发布新版本，平时不在上面工作。
		11.1.2 平时干活是在dev分支上。dev分支是不稳定的。
		11.1.3 我们都有自己的分支，都在dev分支上干活。也就是说我们会时不时将自己的分支往dev分支上合并。
	11.2 当合并分支时，如果可能，git会尽量使用fast-forward模式。在这种模式下，删掉分支，会丢失分支信息，即在查看分支历史时也看不到关于这个分支的信息。
	11.3 合并分支时，加上“--no-ff”参数可以强制禁用fast-forward模式，git就会在merge时生成一个新的commit（这时，可以加上参数“-m”,把commit描述写进去）。这样在分支历史上就可以查看分支信息。
	11.4 git branch -D <分支名>。强行删除一个没有被合并过的分支。
	
12 Bug分支
	12.1 当要修复一个bug，可以通过建立一个bug分支来修复，修复完成后删除；当手头还有工作没有完成时，可以先把工作现场git stash一下，在修复完bug后，再git stash pop,回到工作现场。
	12.2 关于工作现场的命令
		git stash。保存工作现场
		git stash list。查看保存的工作现场
		git stash pop。恢复工作现场并删除对应的保存的工作现场
		git stash apply。恢复工作现场
		git stash drop。删除工作现场，往往和git stash apply共用
		
13 多人协作
	13.1 git clone远程仓库时，git会自动把本地的master分支和远程的master分支对应起来，并且，远程仓库的默认名称时origin。
	13.2 git clone下来的仓库，默认只能看到本地的master分支（用git branch查看，不过使用git branch -a可以查看所有分支，包括隐藏的分支），而且只有master分支的推送有效。如果想要clone远程仓库中指定的某一分支，需要使用git checkout -b branch-name origin/branch-name。
	13.3 建立本地创建的分支和远程的分支的关联，使用git branch --set-upstream-to origin/branch-name。
	13.4 从本地推送分支后，如果推送失败，可以用git pull抓取远程的分支。抓取的分支会直接和你要推送的分支直接合并。如果里面有冲突，要先处理冲突，然后添加提交再推送。

14 rebase操作
	14.1 git rebase。将本地未push的分叉提交历史整理成一条直线。目的是让我查看提交历史时更容易，因为分叉的提交需要三方对比。
	14.2 缺点：
		只有当本地未push的提交有分叉才能用rebase。用了rebase后要重新合并git pull下来的和本地修改的内容，之后git add,不用commit,直接git rebase --continue。
		经过这个操作的本地分叉提交被修改过。
	14.3 git rebase --abort。任何都可以用这个操作使得回到rebase前的状态。
	
15 标签管理
	git tag。查看所有标签
	git tag <tagname>。打一个标签再最新提交上。
	git tag <tagname> <commit id>。打一个标签在commit id上
	git show <tagname>。查看标签详细信息
	git tag -a <tagname> -m "<标签内容描述>" <connit id>。打一个标签在commit id上并加上标签描述
	git push origin <tagname>。推送一个标签
	git push origin --tags。推送所有没有推送的标签
	git tag -d <tagname>。删除一个标签
	git push origin :refs/tags/<tagname>。删除一个已经推送的标签（即远程标签）
