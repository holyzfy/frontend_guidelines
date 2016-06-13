# git分支管理策略

## 常用分支

0. `master`: 主分支，存放成熟的代码，可以随时发布，请**不要**强制push
0. `dev`: 平时在这个分支上开发
0. `fix`: 当发现`master`上分支的代码有bug时，请在此分支上开发，测试通过后再合并到`master`

约定`dev`, `fix`是本地分支，不要push到远程仓库

## 一次完整的操作流程

0. `git clone https://github.com/holyzfy/frontend_guidelines.git`
0. 切换并创建分支`dev`：
    
    `git checkout -b dev`
  
  -b参数表示创建分支，后续再切换到`dev`分支时请去掉此参数；  

0. *一些开发动作，创建，编辑文件...*
0. 把上一步的变更内容添加到暂存区；

    `git add .`

0. 提交到本地仓库：
    
    `git commit -m '请简要描述本次的提交'`
    
0. 准备合并到master分支前先拉取更新，看别人是否向`master`分支推送过代码：

    ```
    git checkout master
    git pull
    ```

0. 如果拉取到更新，就回到`dev`分支，把`master`分支的新内容合并到`dev`：

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

0. 现在dev分支已经包含远程仓库`master`分支的最新代码，可以合并到本地`master`了：

  ```
  git checkout master
  git merge dev
  ```
  本次合并，git只是执行了简单的快进式合并（fast-farward merge）；
  
0. 最后把`master`分支推送到远程仓库：

  `git push`

0. 结束

## 常用操作

- 暂存当前的修改：有时候需要临时切换分支做些事情，又不想提交手头的修改，可以使用`git stash`命令保存工作现场：

  0. 暂存 `git stash`

  0. 取回刚才暂存的内容 `git stash pop`

- 如果忘了提交某些文件，或者想要重新编写提交信息，可以使用 `--amend` 选项重新提交：

  ```
  git commit --amend
  ```

- 解决冲突：例如当前在`dev`分支，准备把`master`分支合并到`dev`分支时遇到冲突，解决步骤：
  0. `git merge --abort` 中止冲突的合并
  0. 对于冲突的文件，选择保留哪个分支的代码

    - `git merge -X theirs master` 使用`master`分支
    - `git merge -s ours master` 使用`dev`分支，也就是当前所在的分支
  
  0. 结束

- 合并多个提交。例如合并最近的两次提交：
  
  ```
  git rebase -i HEAD~2
  ```

  然后根据提示在vim里编辑并保存
