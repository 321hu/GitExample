# 配置SSH Key

- 生成SSH Key

  1. 打开Git bash，输入`ssh-keygen -t rsa -C "example@xx.xxx"`

  2. 输入存放key的文件路径

     - 默认是`~/.ssh/id_rsa`或`C:/Users/<usrname>/.ssh/id_rsa`。直接按【Enter】即是选择默认存放路径

     - 自定义路径建议为`~/.ssh/id_rsa_xxx`，也就是说只要改文件名字，文件存放位置不要改变

  3. 输入密码（passphrase）

     - 默认为空

     - 自定义一般设置为1

- 在平台账号（如Github，Gitee，Gitea等）设置中添加SSH Key

  - ==Note==：同一个平台的不同账号（如Github的两个不同账号）不能使用同一个SSH Key。不同平台之间则无此种顾虑。

  - 添加完成之后便可通过SSH进行git push。

# `.ssh`中的`config`文件

`.ssh/config` 文件是一个纯文本文件，每一行定义一个配置项。配置项可以分为全局配置和特定主机的配置。特定主机的配置会覆盖全局配置。

```bash
Host <hostname>
	Hostname <actual hostname or ip address>
	User <usrname>
	IdentityFile <path_to_private_key>
	Port <port_number>
	ForwardAgent yes|no
```

1. **Host**：定义一个主机别名或一组主机。

2. **HostName**：指定实际的主机名或 IP 地址。

3. **User**：指定默认的用户名。

4. **IdentityFile**：指定私钥文件的路径。

5. **Port**：指定目标主机的 SSH 服务端口（默认是 22）。

6. **ForwardAgent**：启用或禁用 SSH 代理转发。

### config文件示例

```bash
Host github.com
   HostName 20.205.243.160
   User git
   PreferredAuthentications publickey
   IdentityFile ~/.ssh/id_rsa
   
Host github_x
   HostName 20.205.243.160
   User git
   PreferredAuthentications publickey
   IdentityFile ~/.ssh/id_rsa163
```

此时

- 在终端分别输入`ssh -T github.com`与`ssh -T github_x`
  - 不需要输入`git@github.com`与`git@github_x`，因为User已经指定为git
  - 需要分别验证`id_rsa`与`id_rsa163`的密码
