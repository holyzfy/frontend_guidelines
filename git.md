# git

## git提交日志格式

    <类型>: <描述>

[**类型**](https://github.com/angular/angular.js/blob/master/CONTRIBUTING.md#type)必须是以下值之一：

- **feat**: 新增功能
- **fix**: 修复bug
- **docs**: 更新文档
- **style**: 代码排版
- **refactor**: 重构
- **chore**: 其他

**描述**：请一句话说明本次的提交内容

## 常用分支

1. `master`: 主分支，存放成熟的代码，可以随时发布，请**不要**强制push
2. `dev`: 平时在这个分支上开发
3. `fix`: 当发现`master`上分支的代码有bug时，请在此分支上开发，测试通过后再合并到`master`

约定`dev`, `fix`是本地分支，不要push到远程仓库

## 一次完整的操作流程

1. `git clone https://github.com/holyzfy/frontend_guidelines.git`
2. 切换并创建分支`dev`：
    
    `git checkout -b dev`
  
    参数`-b`表示创建分支，后续再切换到`dev`分支时请去掉此参数

3. *一些开发动作，创建，编辑文件...*
4. 把上一步的变更内容添加到暂存区；

    `git add .`

5. 提交到本地仓库：
    
    `git commit -m '请简要描述本次的提交'`
    
6. 准备合并到master分支前先拉取更新，看别人是否向`master`分支推送过代码：

    ```
    git checkout master
    git pull
    ```

7. 如果拉取到更新，就回到`dev`分支，把`master`分支的新内容合并到`dev`：

  ```
  git checkout dev
  git merge master
  ```
  
  如果没有发生冲突，git会自动合并，这时候会打开vim的编辑界面，提示你写提交说明：

  > Merge branch 'master' into dev  
  > \# Please enter a commit message to explain why this merge is necessary,  
  > \# especially if it merges an updated upstream into a topic branch.  
  > \#  
  > \# Lines starting with '#' will be ignored, and an empty message aborts  
  > \# the commit.  
  > ~  
  > ~  
  > ~  
  > ~  
  > ~  
  > ~  
  > ~  
  > ".git/MERGE_MSG" 7L, 293C  

  注意到第一行已经有一句提交说明了，如果没有要补充的就直接运行`:wq`保存并退出vim；

8. 现在dev分支已经包含远程仓库`master`分支的最新代码，可以合并到本地`master`了：

  ```
  git checkout master
  git merge dev
  ```
  本次合并，git只是执行了简单的快进式合并（fast-farward merge）；
  
9. 最后把`master`分支推送到远程仓库：`git push`

10. 结束

## 常用操作

- 暂存当前的修改：有时候需要临时切换分支做些事情，又不想提交手头的修改，可以使用`git stash`命令保存工作现场：

  1. 暂存 `git stash`

  2. 取回刚才暂存的内容 `git stash apply`

- 如果忘了提交某些文件，或者想要重新编写提交信息，可以使用 `--amend` 选项重新提交：

  ```
  git commit --amend
  ```

- 解决冲突：例如当前在`dev`分支，准备把`master`分支合并到`dev`分支时遇到冲突，解决步骤：

  1. `git merge --abort` 中止冲突的合并
  
  2. 对于冲突的文件，选择使用哪个分支的代码

        - `git merge -X theirs master` 使用`master`分支
        - `git merge -X ours master` 使用`dev`分支，也就是当前所在的分支
  
  3. 结束

- 如果在本地提交了多次代码，并且还未push到远程，可以把[几个连续的提交合并成一个](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E9%87%8D%E5%86%99%E5%8E%86%E5%8F%B2)，使提交记录看起来更简洁。
例如合并最近的4次提交，也就是说`HEAD~4`：
  
  ```
  git rebase -i HEAD~4
  ```

  然后根据提示在vim里编辑并保存，如果想中止操作，退出vim后请运行`git rebase --abort`

- 如果在`master`分支运行`git pull`时遇到冲突，可能是因为你运行完`git merge dev`后未及时push，解决办法是撤销刚才的合并操作：
  
  1. 运行`git merge --abort` 中止合并，因为`git pull`的意思是`git fetch` + `git merge origin`
  2. 找到`git merge dev`前的那一次提交的commit id，例如`da183fb88`
  3. 运行`git reset --hard da183fb88`
  4. 运行`git pull`
  5. 结束

- 拉取远程所有的分支 `git fetch --all`

- 撤消提交 `git revert <commit_id>`，多个提交用空格隔开。如果要撤消的提交是个合并操作，需要增加`-m`参数指定回退到哪个分支，例如要撤消如下提交

  ```
  commit edeadbf21b2944587b65f55bf58e14874f5a1a0e
  Merge: 2c87eaa a179b35
  Author: zhangsan <zhangsan@rongcloud.cn>
  Date:   Mon Jun 26 15:43:35 2017 +0800
  ```
本次提交是个合并操作，合并了`2c87eaa` 和 `a179b35`

  - 回退到`2c87eaa`: `git revert edeadbf -m 1`
  - 回退到`a179b35`: `git revert edeadbf -m 2`

- 把其他分支的部分提交合并到当前分支 `git cherry-pick <commit_id>`，多个提交用空格隔开。如果要撤消的提交是个合并操作，需要增加`-m`，规则同上。
- 拉取远程所有的分支 `git pull --all`
- [Syncing a fork](https://help.github.com/articles/syncing-a-fork/)
