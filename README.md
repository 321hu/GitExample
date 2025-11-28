# 欢迎访问321hu的Git示例仓库！

## 仓库描述：

- 这是一个用来测试`git`操作的仓库。

- 这个仓库也会存放一些`git`操作文档。

## 仓库具体说明：

本仓库同时在`Github`和`Gitee`网站上发布并更新：

- `Gitee`：https://gitee.com/zihao-huhu/git-example.git
- `Github`：https://github.com/321hu/GitExample

其对应的本地信息如下：

```bash
$ git remote -v
gitee_origin    git@gitee.com:zihao-huhu/git-example.git (fetch)
gitee_origin    git@gitee.com:zihao-huhu/git-example.git (push)
github_origin   git@github.com:321hu/GitExample.git (fetch)
github_origin   git@github.com:321hu/GitExample.git (push)
```

进行推送操作：

```bash
$ git push github_origin master:main  # 推送到 Github
$ git push gitee_origin master:master # 推送到 Gitee
```

## Git操作文档

- [Git常用命令](Git-常用命令.md)
- [通过SSH连接Github](./通过SSH连接Github.md)
- [Git不常用命令](Git-不常用命令.md)
- [Head与Branch相关知识](Git-head+branch知识.md)
- 高阶操作：
  - [本地仓库通过单个SSH连接两个远程仓库](本地仓库通过单个SSH连接两个远程仓库.md)
  - [针对Github管理两个SSH Key](针对Github管理两个SSH Key.md)
