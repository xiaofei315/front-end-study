

# Git



## 1、创建

## 2、公钥



### 2.1、创建公钥



Gitee 提供了基于SSH协议的Git服务，在使用SSH协议访问仓库仓库之前，需要先配置好账户/仓库的SSH公钥。

你可以按如下命令来生成 ssh key :

```
ssh-keygen -t rsa -C "xxxxx@xxxxx.com"  
```

> 注意：这里的 `xxxxx@xxxxx.com` 只是生成的 ssh key 的名称，并不约束或要求具体命名为某个邮箱。
> 现网的大部分教程均讲解的使用邮箱生成，其一开始的初衷仅仅是为了便于辨识所以使用了邮箱。

![keygen](keygen.png)



### 2.2、复制公钥

在 Windows 环境下，打开 **资源管理器** 进入到 C盘，随后进入 **用户** 目录中 ( 实际是进入到 `C:\Users` 目录中 )。

首先在 **资源管理器** 窗口中 点击 **查看** ，并勾选其中的 **文件扩展名** 和 **隐藏的项目** 。

![](win.png)



随后进入到 你的用户名 对应的目录中。

比如 我的用户名是 `Administrator` ，所以对应的目录就是 `C:\Users\Administrator` 。

随后进入到 `.ssh` 目录中，用记事本打开 `id_rsa.pub` 文件，即可复制新创建的 SSH Key (公钥) 。

### 2.3、添加公钥



Gitee官网提供的帮助:

```http
https://gitee.com/help/articles/4191
```

在 Gitee 主页右上角，鼠标悬浮到 "用户头像" 上，随后依次选择 **「设置」->「安全设置」->「SSH公钥」->「[添加公钥](https://gitee.com/profile/sshkeys)」** ，

在 添加公钥 页面中即可添加生成的 public key 添加到当前账户中。



在自己的Gitee账户添加 公钥 后，在 **命令提示符**  或 **终端（Terminal）**中输入

```
ssh -T git@gitee.com
```

<b style="color:red;">首次使用需要确认并添加主机到本机SSH可信列表。</b>

若返回 `Hi XXX! You've successfully authenticated, but Gitee.com does not provide shell access.` 内容，则证明添加成功。如下图所示:

![](ssh.png)

添加成功后，就可以使用SSH协议对仓库进行操作了。

## 3、克隆

首先切换到本地磁盘上的指定目录中，比如切换到 `D:/mycodes` 

```cmd
D:\mycodes>
```

然后执行以下命令完成克隆操作:

```sh
git clone 仓库地址
```

比如，在 `D:/mycodes` 目录下 执行以下命令:

```sh
git clone git@gitee.com:mozicoding/ecut-soft-608.git
```

执行之后会生成 `D:/test/ecut-soft-608` 目录，这个目录就是从远程仓库克隆下来的。

## 4、配置

- 全局配置

全局配置采用以下方式:

```cmd
git config --global user.name "你的名字或昵称"
git config --global user.email "你的邮箱"
```

全局(global)配置会针对所有仓库起作用。



```cmd
git config --global user.name "zhangsanfeng"
git config --global user.email "zhangsanfeng@wudang.com"
```

- 局部配置

局部配置采用以下方式:

```cmd
git config --local user.name "你的名字或昵称"
git config --local user.email "你的邮箱"
```

局部(local)配置仅针对当前仓库起作用。

配置某个仓库时，必须首先进入到该仓库对应的目录中，

比如进入到 `ecut-soft-608` 仓库对应的目录 ( `D:\mycodes\eccut-soft-608` ) 中:

```cmd
git config --local user.name "zhangsanfeng"
git config --local user.email "zhangsanfeng@wudang.com"
```

另外，通过 以下命令可以查看当前仓库的相关配置:

```cmd
git config --list
```

## 5.使用git init初始化一个git仓库

执行该命令，会出现一个隐藏的.git文件夹

objects目录用于存储纳入缓存的文件

refs目录用于存储纳入版本库的文件

## 6、添加



<b style="color:red">若仓库中文件有改动</b> ( 比如 新建、删除、修改 ) 则需要将 这些改动 首先添加到 git 暂存区 ( 本地仓库 )。



将本地仓库中文件变动添加到 git暂存区采用以下命令:

```cmd
git add .
以上操作表示将当前目录所有文件添加到git暂存区。
```



```cmd
git add 文件名
以上操作表示将指定文件添加到git缓存区
```



通常， 在 **本地仓库根目录** 中 执行 `git add .` 操作。

## 7、提交



将本地仓库下 git 暂存区 的文件 提交到 本地仓库，使用以下命令:

```cmd
git commit -m "这里书写注释信息"
```

以上操作用于提交并备注提交信息。

## 8、推送

将 本地提交 推送到 远程仓库 :

```cmd
git push origin master
```

这里需要注意:

- `origin` 对应 远程仓库
- `master` 对应 分支





## 9、拉取



```cmd
git pull origin master
```



## 10.移除

git rm文件名

从版本库中移除文件 //git rm 文件名

如果加了 --cache，说明是从缓存中移除//git rm 文件名 --cache

## 11.git日志

```cmd
git log
```



## 12.回退版本

```cmd
git reset --hard HEAD^
回退到上一个版本
git reset --hard HEAD^^
回到上上个版本
```

```cmd
git reset --hard HEAD commit id
回到未来
```

## 13.多人开发

拉取代码

```cmd
gie fetch origin master 
从远程主机的master分支上拉取最新内容
```

合并代码

```cmd
git merge FETCH_HEAD
将拉取的内容合并到当前所在的分支中
```

这两个操作可以通过pull来简化    

```cmd
git pull origin master
```

## 14.分支与主干

 分支：不会影响整个项目里面的主线的版本

gir 分支与主干的合并操作：

在主干上合并分支：

```cmd
(master): git merge branch --squash
```

在分支上合并主干：

```cmd
(branch): git merge master --squash
```

创建功能分支：

```cmd
(master) git checkout -b feature
```

合并最新主干代码：

1.(feature) git checkout master 

2.(master) git pull

3.(master) git checkout feature 

4.(feature) git merge master 

5.解冲突

6.(feature) git commit #

## 15.git指令

查看分支：git branch 

创建分支：git branch <name>

切换分支：git checkout <name>

创建+切换分支：git checkout -b<name>

合并某个分支到当前分支：git merge <name>

删除分支：git branch -d <name>

git pull 将远程主机的最新内容拉取下来直接合并，可能会出现冲突
