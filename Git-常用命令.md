## git push

- `git push -u <origin_name> <local_branch>:<remote_branch>`

- 输入`git push -u <origin_name> <local_branch>:<remote_branch>`后：

  `<local_branch>`便与`<origin_name>/<remote_branch>`绑定了

  - ```bash
    git push -u gitee_origin master:master
    # master <--> gitee_origin/master
    ## 此时如果输入 git push github_origin, 会在远端的 github 下新建一个分支: github_origin/master
    ### 想要继续向 github_origin/main push，正确代码为
    git push github_origin master:main
    ```

## git branch

- 创建与切换本地分支

  - `git branch <name>`：创建新分支

  - `git checkout <name>`：切换到对应分支

    > 在 Git 2.23 版本中，引入了一个名为 `git switch` 的新命令，最终会取代 `git checkout`

- 删除分支
  - 删除本地分支：`git branch -D <branch_name>`
  - 删除远程分支：
    - `git push <origin_name> --delete <remote_branch>`
    - `git fetch <origin_name> --prune`
- 查看分支：

  - 查看所有分支：`git branch -a`
  - 查看分支绑定信息：`git branch -vv`

## git fork

**教程1：**基于A仓库，派生B仓库，继而创建合并请求。

1. 在A仓库的网页上点击【fork或派生】，创建B仓库
2. 在本地新建文件夹，`git init`
3. `git remote add origin <B-url>`
4. 查看B仓库的分支名称，`git pull origin <B-branch-name> `
5. 查看是否pull成功
6. 在本地仓库做出修改，并进行`git add, git commit, git push`操作
7. 在A仓库网页上找到【创建合并请求】
8. 等待A仓库管理者通过【合并请求】

**教程2：**A仓库进行了更新，B仓库如何同步？

1. `git remote add upstream <A-url>`
2. `git remote -v`查看是否添加成功
3. `git fetch upstream`：使用fetch更新，fetch后会被存储在一个本地分支upstream/master上
4. 查看A仓库的分支名称，`git merge upstream/<A-branch-name>`
5. `git log`查看更新信息
6. 最后就是push到B仓库：`git push origin <B-branch-name>`