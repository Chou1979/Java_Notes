### 分支

生成副本，避免影响开发主线

#### 分支细分

1. 主分支（master）：第一次向 git 仓库提交更新记录时自动产生的一个分支，GitHub 现已更新为 main 。
2. 开发分支（develop）：作为开发的分支，基于 master 分支创建。
3. 功能分支（feature）：作为开发具体功能的分支基于开发分支创建。

#### 分支命令

- `git branch` 查看分支
- `git branch 分支名称` 创建分支
- `git checkout 分支名称` 切换分支
- `git merge 来源分支` 合并分支
- `git branch -d 分支名称` 删除分支（分支合并后才允许被删除）（-D 大写强制删除）
    - `git push origin :branch-name` : 远程仓库同步删除掉的分支

注意：

​ 开发分支文件后要 `commit` 后再切换主分支，否则分支文件会出现在主分支里面。

> > 分支管理
> 
> 1. 创建分支：`git branch` ，如`git branch testing`；
> 2. 从当前所处的分支切换到其他分支：`git checkout` ，如`git checkout testing`；
> 3. 新建并切换到新建分支上：`git checkout -b` ;
> 4. 删除分支：`git branch -d` ；
> 5. 将当前分支与指定分支进行合并：`git merge` ;
> 6. 显示本地仓库的所有分支：`git branch`;
> 7. 查看各个分支最后一个提交对象的信息：`git branch -v`;
> 8. 查看哪些分支已经合并到当前分支：`git branch --merged`;
> 9. 查看当前哪些分支还没有合并到当前分支：`git branch --no-merged`;
> 10. 把远程分支合并到当前分支：`git merge /`，如`git merge origin/serverfix`；如果是单线的历史分支不存在任何需要解决的分歧，只是简单的将 HEAD 指针前移，所以这种合并过程可以称为快进（Fast forward），而如果是历史分支是分叉的，会以当前分叉的两个分支作为两个祖先，创建新的提交对象；如果在合并分支时，遇到合并冲突需要人工解决后，再才能提交；
> 11. 在远程分支的基础上创建新的本地分支`：git checkout -b /`，如`git checkout -b serverfix origin/serverfix`;
> 12. 从远程分支 checkout 出来的本地分支，称之为跟踪分支。在跟踪分支上向远程分支上推送内容：`git push`。该命令会自动判断应该向远程仓库中的哪个分支推送数据；在跟踪分支上合并远程分支：`git pull`；
> 13. 将一个分支里提交的改变移到基底分支上重放一遍：`git rebase` ，如`git rebase master server`，将特性分支 server 提交的改变在基底分支 master 上重演一遍；使用 rebase 操作最大的好处是像在单个分支上操作的，提交的修改历史也是一根线；如果想把基于一个特性分支上的另一个特性分支变基到其他分支上，可以使用`--onto`操作：`git rebase --onto` ，如`git rebase --onto master server client`；使用 rebase 操作应该遵循的原则是：**一旦分支中的提交对象发布到公共仓库，就千万不要对该分支进行 rebase 操作**；

### 暂时保存更改

git 中可以不提交更改，只提取分支上所有改动并储存，让开发人员得到一个干净的副本，临时转向其它工作。复制到“剪切板”，可以“粘贴“到其它分支。

场景：

- 储存临时改动：`git stash`
- 恢复临时改动：`git stash pop`

### 打标签

> Git 使用的标签有两种类型：**轻量级的（lightweight）和含附注的（annotated）**。轻量级标签就像是个不会变化的分支，实际上它就是个指向特定提交对象的引用。而含附注标签，实际上是存储在仓库中的一个独立对象，它有自身的校验和信息，包含着标签的名字，电子邮件地址和日期，以及标签说明，标签本身也允许使用 GNU Privacy Guard (GPG) 来签署或验证。一般我们都建议使用含附注型的标签，以便保留相关信息；当然，如果只是临时性加注标签，或者不需要旁注额外信息，用轻量级标签也没问题。
> 
> 1. 列出现在所有的标签：`git tag`;
> 2. 使用特定的搜索模式列出符合条件的标签，例如只对 1.4.2 系列的版本感兴趣：`git tag -l "v1.4.2.*"`;
> 3. 创建一个含附注类型的标签，需要加`-a`参数，如`git tag -a v1.4 -m "my version 1.4"`;
> 4. 使用 git show 命令查看相应标签的版本信息，并连同显示打标签时的提交对象：`git show v1.4`;
> 5. 如果有自己的私钥，可以使用 GPG 来签署标签，只需要在命令中使用`-s`参数：`git tag -s v1.5 -m "my signed 1.5 tag"`;
> 6. 验证已签署的标签：git tag -v ，如`git tag -v v1.5`;
> 7. 创建一个轻量级标签的话，就直接使用 git tag 命令即可，连`-a`,`-s`以及`-m`选项都不需要，直接给出标签名字即可，如`git tag v1.5`;
> 8. 将标签推送到远程仓库中：git push origin ，如`git push origin v1.5`；
> 9. 将本地所有的标签全部推送到远程仓库中：`git push origin --tags`;