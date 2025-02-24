# git command

## 管理分支

[Git 分支管理 | 菜鸟教程 (runoob.com)](https://www.runoob.com/git/git-branch.html)

### 合并分支

- `git merge`：把这两个 parent 节点本身及它们所有的祖先都包含进来

  - `git merge new_branch`：当前`HEAD`指向`main`分支，把`new_branch`合并到`main`中，并且自动做一次`git commit`

- `git rebase`：rebase 实际上就是取出一系列的提交记录，“复制”它们，然后在另外一个地方逐个的放下去

  > rebase 的优势是可以创造更线性的提交历史

  - `git rebase main`：当前head指向`new_branch`分支，将`new_branch`分支里的工作直接移到 `main` 分支上，可以理解为“基于`main`的`git`”。操作结果为**`new_branch`分支上的工作在`main`分支的最顶端**
  - 如果想将`main`分支移至与`new_branch`分支相同位置，则执行以下操作：
    - `git checkout main`
    - ``git branch -f main new_branch`

## 在提交树上移动

### 依靠Hash值进行移动

- `git checkout <Hash_name>`：使用提交记录上的Hash值进行移动

哈希值一般较长，SHA-1对应的Hash值可能是fed2da64c0efc5293610bdd892f82a58e8cbc5d8

Example：`git checkout fed2da`

> 可以通过`git log`来查看提交记录的哈希值

### 依靠相对引用进行移动

- 使用 `^` 向上移动 1 个提交记录：`main^` 相当于“`main` 的 parent 节点”
- 使用 `~<num>` 向上移动多个提交记录，如 `~3`

Example：`git checkout HEAD~5`，将HEAD移动至当前HEAD的前四个提交记录

### 强制移动分支

可以直接使用 `-f` 选项让分支指向另一个提交

Example：`git branch -f main HEAD~3`，将 main 分支强制指向 HEAD 的第 3 级 parent 提交。

## 撤销变更

### `git reset`

`git reset` 通过把分支记录回退几个提交记录来实现撤销改动

Example：`git reset HEAD~1`，回退到HEAD的前一次提交，本次提交抹除（但保留在缓存区）

### `git revert`

`git reset`对多人合作使用的远程分支是无效的！此时我们引入`git revert`

Example：`git revert HEAD`，撤销本次提交，需要注意的是`revert`的撤销是通过新产生一次提交来实现的

## 整理提交记录

### `git cherry-pick <提交号>...`

cherry-pick是将一些提交复制到当前所在的位置（`HEAD`）下面的最佳方式

Example：`git cherry-pick C3 C4 C7`，将`C3 C4 C7`按顺序”抓到“HEAD（一般而言是当前分支）下，并依次进行commit操作。

> 当你知道你所需要的提交记录（并且还知道这些提交记录的哈希值）时, 用 cherry-pick 再好不过了。

### 交互式 rebase 

交互式 rebase 指的是使用带参数 `--interactive` 的 rebase 命令, 简写为 `-i`

如果操作者在命令后增加了这个选项, Git 会打开一个 UI 界面并列出将要被复制到目标分支的备选提交记录，它还会显示每个提交记录的哈希值和提交说明，提交说明有助于操作者理解这个提交进行了哪些更改。

当 rebase UI界面打开时, 操作者能做3件事:

- 调整提交记录的顺序（通过鼠标拖放来完成）
- 删除你不想要的提交（通过切换 `pick` 的状态来完成，关闭就意味着你不想要这个提交记录）
- 合并提交。

Example：`git rebase -i HEAD~3`，从自身往前数3个记录进行操作（可操作的记录总数为3）

> 当目标提交记录的哈希值未知时，或当操作者希望从一系列的提交记录中找到特定的记录，利用交互式的 rebase 吧！

## 提交的技巧

### 对此前的记录进行微小的修改

假设只要修改当前提交的父提交，i.e.，parent

```
A - parent - child
```

- 第一种方法：使用`git rebase -i`
  - 使用`git rebase -i HEAD~2`，并手动颠倒child和parent的顺序
  - 现在两个提交的顺序已然颠倒——使用`git commit --amend`进行修改
  - `git rebase -i HEAD~2`重新颠倒顺序
- 第二种方法：使用`git cherry-pick`
  - 先将HEAD指向A
  - `git cherry-pick parent` --> 使用`git commit --amend`进行修改
  - `git cherry-pick child`

## 标签/`git tag`

`git tag v1 C1`，其中v1是tag，C1是提交记录。如果不指定C1，那么默认为HEAD指向的提交记录。

tag的好处在于它可以作为一个唯一标识符代表提交记录。

在移动HEAD的时候，可以通过`git checkout v1`来实现。
