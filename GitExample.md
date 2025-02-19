**`git push <origin_name> <local_branch>:<remote_branch>`**

Gitee:

```bash
git remote add gitee_origin https://gitee.com/zihao-huhu/git-example.git
git push gitee_origin master:master
```

Github:

```bash
git remote add github_origin git@github.com:321hu/GitExample.git
git push github_origin master:main
```

## Notes

- 输入`git push -u <origin_name> <local_branch>:<remote_branch>`后，`<local_branch>`与`<origin_name>/<remote_branch>`便绑定了

  - ```bash
    git push -u gitee_origin master:master
    # master <--> gitee_origin/master
    ## 此时如果输入 git push github_origin, 会在远端的 github 下新建一个分支: github_origin/master
    ### 想要继续向 github_origin/main push，正确代码为
    git push github_origin master:main
    ```

- 删除分支

  - 删除本地分支：`git branch -D <branch_name>`
  - 删除远程分支：
    - `git push <origin_name> --delete <remote_branch>`
    - `git fetch <origin_name> --prune`

- 查看分支：

  - 查看所有分支：`git branch -a`
  - 查看分支绑定信息：`git branch -vv`