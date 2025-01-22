Git：目前世界上最先进的分布式版本控制系统；
Git、Github 区别：Git 是分布式控制系统，Github 是为用户提供 Git 服务的网站；

### Git 下载和安装

- 下载地址： [https://git-scm.com/downloads](https://git-scm.com/downloads)
- 使用默认值安装
- 资源管理器内单击鼠标右键选择 `Git Bash Here`
- 输入`git --version` 检查是否安装成功

### Git 基本工作流程

> [![image-20210821201054011](https://github.com/Eished/git_notes/raw/master/readme.assets/image-20210821201054011.png)](https://github.com/Eished/git_notes/blob/master/readme.assets/image-20210821201054011.png)
> 
> 主要涉及到四个关键点：
> 
> 1. **工作区**：本地电脑存放项目文件的地方，比如 learnGitProject 文件夹；
> 2. 暂存区（Index/Stage）：在使用 git 管理项目文件的时候，其本地的项目文件会多出一个.git 的文件夹，将这个.git 文件夹称之为版本库。其中.git 文件夹中包含了两个部分，一个是暂存区（Index 或者 Stage）,顾名思义就是暂时存放文件的地方，通常使用 add 命令将工作区的文件添加到暂存区里；
> 3. 本地仓库：.git 文件夹里还包括 git 自动创建的 master 分支，并且将 HEAD 指针指向 master 分支。使用 commit 命令可以将暂存区中的文件添加到本地仓库中；
> 4. 远程仓库：不是在本地仓库中，项目代码在远程 git 服务器上，比如项目放在 github 上，就是一个远程仓库，通常使用 clone 命令将远程仓库拷贝到本地仓库中，开发后推送到远程仓库中即可；
> 
> 更细节的来看：
> 
> [![image-20210821201040414](https://github.com/Eished/git_notes/raw/master/readme.assets/image-20210821201040414.png)](https://github.com/Eished/git_notes/blob/master/readme.assets/image-20210821201040414.png)
> 
> 日常开发时代码实际上放置在工作区中，也就是本地的 XXX.java 这些文件，通过 add 等这些命令将代码文教提交给暂存区（Index/Stage），也就意味着代码全权交给了 git 进行管理，之后通过 commit 等命令将暂存区提交给 master 分支上，也就是意味打了一个版本，也可以说代码提交到了本地仓库中。另外，团队协作过程中自然而然还涉及到与远程仓库的交互。
> 
> 因此，经过这样的分析，git 命令可以分为这样的逻辑进行理解和记忆：
> 
> 1. git 管理配置的命令；
>     
>     **几个核心存储区的交互命令：**
>     
> 2. 工作区与暂存区的交互；
>     
> 3. 暂存区与本地仓库（分支）上的交互；
>     
> 4. 本地仓库与远程仓库的交互。
>     
> 
> 作者：你听___ 链接：[https://juejin.im/post/5ae072906fb9a07a9e4ce596](https://juejin.im/post/5ae072906fb9a07a9e4ce596) 来源：掘金

|工作目录|暂存区|git 仓库|远程仓库|
|---|---|---|---|
|被 Git 管理的项目|临时存放被修改的文件|目录用于存放提交记录|远程代码仓库|
|`git init`|`git add`|`git commit`|`git push`|

### Git 使用前的配置命令

在使用前告诉 git 你是谁：

1. 第一次使用 git，配置用户信息
    
    1. 配置用户名：`git config --global user.name "your name"`;
    2. 配置用户邮箱：`git config --global user.email "youremail@github.com"`;
2. > 查询配置信息
    
    1. 列出当前配置：`git config --list`;
    2. 列出 repository 配置：`git config --local --list`;
    3. 列出全局配置：`git config --global --list`;
    4. 列出系统配置：`git config --system --list`;
3. > 其他配置
    
    1. 配置解决冲突时使用哪种差异分析工具，比如要使用 vimdiff：`git config --global merge.tool vimdiff`;
    2. 配置 git 命令输出为彩色的：`git config --global color.ui auto`;
    3. 配置 git 使用的文本编辑器：`git config --global core.editor vi`;
4. > 注：
    
    1. 更改-->重复上述命令
    2. 也可直接修改 `C:\Users\用户\.gitconfig`

### 工作区上的操作命令

#### 提交步骤

1. `git init` 初始化 git 仓库
    
    > > 新建仓库
    > 
    > 1. 将工作区中的项目文件使用 git 进行管理，即创建一个新的本地仓库：`git init`；（在仓库目录下会有一个隐藏的文件".git", 表示初始化成功）
    > 3. 从远程 git 仓库复制项目：`git clone` ; 克隆项目时如果想定义新的项目名，可以在 clone 命令后指定新的项目名：`git clone git://github.com/wasd/example.git NewName`；
    
2. `git status` 查看文件状态
    
    > > 查新信息
    > 
    > 1. 查询当前工作区所有文件的状态：`git status`;
    > 2. 比较工作区中当前文件和暂存区之间的差异，也就是修改之后还没有暂存的内容：git diff；指定文件在工作区和暂存区上差异比较：`git diff` ;
    
3. `git add 文件/文件列表` 提交到暂存区
    
    > > 提交
    > 
    > 1. 提交工作区所有文件到暂存区：`git add .`
    > 2. 提交工作区中指定文件到暂存区：`git add ...`;
    > 3. 提交工作区中某个文件夹中所有文件到暂存区：`git add [dir]`;
    
4. `git commit -m 提交信息` 向仓库提交代码
    
    > > 提交文件到版本库
    > 
    > 1. 将暂存区中的文件提交到本地仓库中，即打上新版本：`git commit -m "commit_info"`;
    > 2. 将所有已经使用 git 管理过的文件暂存后一并提交，跳过 add 到暂存区的过程：`git commit -a -m "commit_info"`;
    > 3. 提交文件时，发现漏掉几个文件，或者注释写错了，可以撤销上一次提交：`git commit --amend`;
    
5. `git log` 查看提交记录
    
    > > 查看信息
    > 
    > 1. 比较暂存区与上一版本的差异：`git diff --cached`;
    > 2. 指定文件在暂存区和本地仓库的不同：`git diff --cached`;
    > 3. 查看提交历史：git log；参数`-p`展开每次提交的内容差异，用`-2`显示最近的两次更新，如`git log -p -2`;
    

#### 撤销

- 用暂存区中的文件覆盖工作目录中的文件：`git checkout -- 文件名` 不加 `-- 文件名`则覆盖全部文件
    
- 将文件从暂存区中删除：`git rm --cached 文件名`
    
- 将 git 仓库中指定的更新记录恢复出来，并且覆盖暂存区和工作目录： `git reset --hard commitID`
    
- > > 撤销
    > 
    > 1. 删除工作区文件，并且也从暂存区删除对应文件的记录：`git rm` ;
    > 2. 从暂存区中删除文件，但是工作区依然还有该文件:`git rm --cached` ;
    > 3. 取消暂存区已经暂存的文件：`git reset HEAD ...`;
    > 4. 撤销上一次对文件的操作：`git checkout --`。要确定上一次对文件的修改不再需要，如果想保留上一次的修改以备以后继续工作，可以使用 stashing 和分支来处理；
    > 5. 隐藏当前变更，以便能够切换分支：`git stash`；
    > 6. 查看当前所有的储藏：`git stash list`；
    > 7. 应用最新的储藏：`git stash apply`，如果想应用更早的储藏：`git stash apply stash@{2}`；重新应用被暂存的变更，需要加上`--index`参数：`git stash apply --index`;
    > 8. 使用 apply 命令只是应用储藏，而内容仍然还在栈上，需要移除指定的储藏：`git stash drop stash{0}`；如果使用 pop 命令不仅可以重新应用储藏，还可以立刻从堆栈中清除：`git stash pop`;
    > 9. 在某些情况下，你可能想应用储藏的修改，在进行了一些其他的修改后，又要取消之前所应用储藏的修改。Git 没有提供类似于 stash unapply 的命令，但是可以通过取消该储藏的补丁达到同样的效果：`git stash show -p stash@{0} | git apply -R`；同样的，如果你沒有指定具体的某个储藏，Git 会选择最近的储藏：`git stash show -p | git apply -R`；
    > 
    > > 更新文件
    > 
    > 1. 重命名文件，并将已改名文件提交到暂存区：`git mv [file-original] [file-renamed]`;