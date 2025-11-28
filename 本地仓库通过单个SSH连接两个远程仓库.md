### 1. 本地生成 SSH Key

参见[通过SSH连接Github](./通过SSH连接Github.md)。

### 2. 在对应网站上添加 SSH Key

分别在 Github 与 Gitee 上添加我们生成的 SSH Key。

==如果没有在 ~/.ssh/config 中自定义 Host，则可以通过以下命令来测试是否添加成功：==

```bash
ssh -T git@github.com
ssh -T git@gitee.com
```

### 3. 在对应网站上新建远程仓库

在 Github 与 Gitee 上分别新建仓库，名为 `GitExample`。

### 4. 在本地创建文件夹

在本地创建一个新的文件夹，名为 `GitExample`。

- 进行 git 初始化：`git init`。
- 在 `GitExample` 中新建一个 `README.md`，里面随意添加内容
- `git add .`
- `git commit -m "first commit"`

将本地仓库分别链接到远程仓库 ：

```bash
git remote add gitee_origin git@gitee.com:<usr_name>/<reponame>.git
git remote -v # 查看是否添加成功
git remote add github_origin git@github.com:<usrName>/<repoName>.git
git remote -v # 查看是否添加成功
```

如果添加成功，终端应输出以下信息：

```
gitee_origin    git@gitee.com:<usrName>/<repoName>.git (fetch)
gitee_origin    git@gitee.com:<usrName>/<repoName>.git (push)
github_origin   git@github.com:<usrName>/<repoName>.git (fetch)
github_origin   git@github.com:<usrName>/<repoName>.git (push)
```
在正式向远程仓库推送前，我们需要先查看远程仓库下的分支名称以及本地仓库的分支名称：`git branch -a`

- 例子

  ```bash
  * master
    remotes/gitee_origin/master
    remotes/github_origin/main
  ```
  
这里表示我们本地仓库名称为 master，我们 Gitee 下的分支为 master，而 Github 下的分支名为 main。

### 5. 推送修改至远程仓库

此时我们先向 Gitee 推送我们的修改：

==`git push originName localBranch:remoteBranch`==

```bash
git push gitee_origin master:master
```

接着先向 Github 推送我们的修改

```bash
git push github_origin master:main
```

