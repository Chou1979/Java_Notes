### 注册 Github 账号

略~
### 多人协作开发流程

- A 在自己的计算机中创建本地仓库
- A 在 GitHub 中创建远程仓库
- A 将本地仓库推送到远程仓库
- B 克隆远程仓库到本地进行开发
- B 将本地仓库开发内容推送到远程仓库
- A 将远程仓库中的最新内容拉去本地

### 创建远程仓库

[![](https://github.com/Eished/git_notes/raw/master/git_notes/20191115154237.png)]

### 推送到远程仓库

1. `git push 远程仓库地址 分支名称`
    
2. `git push 远程仓库地址别名 分支名称`
    
3. `git push -u 远程仓库地址别名 分支名称`
    
    `-u` 记住推送地址和分支，下次只需要输入`git push`
    
4. `git remote add 远程仓库地址别名 远程仓库地址`
    
5. 删除别名：`git remote remove 远程仓库地址别名`
    
6. 第一次提交需要用户名和密码，电脑会记住密码在凭据管理器，第二次就不用了。
    
7. > ### 本地仓库上的操作
    > 
    > [](https://github.com/Eished/git_notes#%E6%9C%AC%E5%9C%B0%E4%BB%93%E5%BA%93%E4%B8%8A%E7%9A%84%E6%93%8D%E4%BD%9C)
    > 
    > 1. 查看本地仓库关联的远程仓库：`git remote`；在克隆完每个远程仓库后，远程仓库默认为`origin`;加上`-v`的参数后，会显示远程仓库的`url`地址；
    > 2. 添加远程仓库，一般会取一个简短的别名：`git remote add [remote-name] [url]`，比如：`git remote add example git://github.com/example/example.git`;
    > 3. 从远程仓库中抓取本地仓库中没有的更新：`git fetch [remote-name]`，如`git fetch origin`;使用 fetch 只是将远端数据拉到本地仓库，并不自动合并到当前工作分支，只能人工合并。如果设置了某个分支关联到远程仓库的某个分支的话，可以使用`git pull`来拉去远程分支的数据，然后将远端分支自动合并到本地仓库中的当前分支；
    > 4. 将本地仓库某分支推送到远程仓库上：`git push [remote-name] [branch-name]`，如`git push origin master`；如果想将本地分支推送到远程仓库的不同名分支：`git push :`，如`git push origin serverfix:awesomebranch`;如果想删除远程分支：`git push [romote-name] :`，如`git push origin :serverfix`。这里省略了本地分支，也就相当于将空白内容推送给远程分支，就等于删掉了远程分支。
    > 5. 查看远程仓库的详细信息：`git remote show origin`；
    > 6. 修改某个远程仓库在本地的简称：`git remote rename [old-name] [new-name]`，如`git remote rename origin org`；
    > 7. 移除远程仓库：`git remote rm [remote-name]`；
    

### 拉取仓库

#### 克隆仓库

- 克隆远程仓库到本地：`git clone 仓库地址`

#### 拉取远程仓库中最新版本

- 拉取远程仓库最新版本到本地： `git pull 远程仓库地址 分支名称`

### 解决冲突

多人开发同一个项目时，如果两个人修改了同一个文件同一个地方

1. `git pull`
2. 手动解决冲突
3. `git push`

[![](https://github.com/Eished/git_notes/raw/master/git_notes/20191115164339.png)](https://github.com/Eished/git_notes/blob/master/git_notes/20191115164339.png)

### 跨团队协作

1. `fork`到自己的远程仓库
2. `clone`到本地进行修改
3. `push`到远程仓库
4. `pull request`发送给原作者
5. 原作者查看`commit` 审核
6. 原作者  `merge pull request`

### SSH 免密登录

1. 生成密钥： `ssh-keygen`
    
    密匙储存目录： `C:\User\用户\.ssh`
    
    公钥名称： `id_rsa.pub`
    
    私钥名称： `id_rsa`
    
2. Github 添加公钥
    

[![](https://github.com/Eished/git_notes/raw/master/git_notes/20191115165957.png)](https://github.com/Eished/git_notes/blob/master/git_notes/20191115165957.png)

3. 复制 SSH 地址：
    
    [![](https://github.com/Eished/git_notes/raw/master/git_notes/20191115170348.png)](https://github.com/Eished/git_notes/blob/master/git_notes/20191115170348.png)
    
4. 设置 ssh 别名：`$ git remote add origin_ssh SSH地址`
    
5. 远程推送： `$ git push origin_ssh master`
    
6. [ubuntu git 环境搭建以及通过 SSH 连接 Github（免密码）配置](https://segmentfault.com/a/1190000013154540)
    

### Git 忽略清单

将不需要的文件名字添加到此文件中，执行 git 命令时就会忽略这些文件。

- git 忽略清单文件名称：`.gitignore`
    
- 将工作目录所有文件添加到缓存区： `git add .`
    
- 例子：
    
    ```gitignore
    # 此为注释 – 将被 Git 忽略
    # 忽略所有 .a 结尾的文件
    *.a
    # 但 lib.a 除外
    !lib.a
    # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
    /TODO
    # 忽略 build/ 目录下的所有文件
    build/
    # 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
    doc/*.txt
    # 忽略 doc/ 目录下所有扩展名为 txt 的文件
    doc/**/*.txt
    ```
    

### 为仓库添加说明

在仓库根目录添加`readme.md`文件即可