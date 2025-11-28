### 1. 生成第 1 个 SSH Key

安装好 git 后，右键 Git Bash Here，输入如下命令：

```bash
ssh-keygen -t rsa -C"first_email@xxxxx.com"
```

输入完以上命令，然后一直按回车就行了。

这样就能使用 ssh 生成第 1 个 key 了，默认会在根目录（windows 下是：C:\Users\用户名.ssh）下生成 id_rsa, id_rsa.pub 2 个文件，即公钥和私钥。

### 2. 生成第 2 个 SSH Key

同样输入如下命令：

```bash
ssh-keygen -t rsa -C"second_email@xxxxx.com"
```

这个时候需要注意，在生成第 2 个 Key 的时候就不要一直按回车。在选择文件保存名称的时候：==Enter file in which to save the key: (c:/Users/<用户名>/.ssh/id_rsa)==，给文件起一个新名字，否则会将第 1 个 SSH Key 的文件覆盖掉。可以输入 ==id_rsa_2==，然后再按回车，最后在这个目录下相应的也会生成一个 id_rsa_2.pub 文件。

### 3. 修改配置文件

在你的 ~/.ssh 目录下新建一个config文件（如已有则不需新建），添加如下内容：

```bash
Host github.com
    HostName github.com
    User git
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa


Host github_x
    HostName github.com
    User git
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa_2
```

==注意==

```markdown
"Host github.com": "git add origin git@github.com:<usr_name>/<repo_name>.git"
"Host github_x": "git add origin git@github_x:<usr_name>/<repo_name>.git"
```

### 4.在对应网站上添加 SSH Keys

在不同的浏览器，用不同的 Github 账号登录 [https://github.com/settings/keys](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fsettings%2Fkeys)，并分别添加一个 SSH Key。假设账号1用的是 key 1（Hoss：github.com），账号2用的是 key 2（Hoss：github_x）。

此时基于上述 ~/.ssh/config 的配置，我们可以验证是否添加成功：

```bash
ssh -T git@github.com # key 1
ssh -T git@github_x   # key 2
```

### 5. 链接本地仓库与远程仓库

如果添加成功，我们便可以开始进行远程仓库与本地仓库的链接：

- 账号1：

  ```bash
  # Under local folder 111
  git remote add origin git@github.com:<usr_name>/<reponame>.git
  git remote -v # 查看是否添加成功
  ```


- 账号2：

  ```bash
  # Under local folder 222
  git remote add origin git@github_x:<usr_name>/<reponame>.git
  git remote -v # 查看是否添加成功
  ```
  
  









