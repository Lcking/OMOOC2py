# git 私人教程

## 背景

## 安装
- github账号
- 能看懂一些英文
- 稍微有些耐心（请不要跟随内心，不要怂，灵活寻找解决方案）
- 在本地电脑安装git for windows，一路next，直到最后一步确定。
- 在我的电脑-属性-高级系统设置-高级-环境变量中的系统变量Path添加<code>C:\Program Files\Git\bin;C:\Program Files\Git\mingw64\libexec\git-core;</code>
- 在桌面中点击右键，出现<code>git bash here</code>即安装成功

## 配置

#### 1.SSH Keys
要配置git与github的联动，就需要做几个较为复杂设置，首先就是SSH Keys的设置：
![](http://7xnnij.com1.z0.glb.clouddn.com/ssh8.jpg)

![](http://7xnnij.com1.z0.glb.clouddn.com/add-sshkey.jpg)

#### 2.生成公钥和密钥
在做上述添加SSH keys之前我们还需要做的事情就是生成公钥和私钥，在git CLI中键入如下命令：<br>
`$ ssh-keygen -C "你的邮箱地址" -f ~/.ssh/gotgithub`<br>
gotgithub为私钥文件名，对应的公钥文件名为gotgithub.pub，这个文件名可以自己命名，这连个密钥文件都保存在~/.ssh/目录下。<br>


#### 3.配置config（.ssh文件夹中如果没有就新建）
在config的文件中键入如下的命令：

Host github.com<br>
User git<br>
Hostname github.com<br>
PreferredAuthentications publickey<br>
IdentityFile ~/.ssh/gotgithub

关闭并保存文件即可。

#### 4.Add SSH Keys
在第一步的那种界面下按步骤操作即可，Title中的内容可以随便填写，key中的内容要~/.ssh/目录，打开公钥文件gotgithub.pub，将其中的内容拷贝到Key框中，不能够有任何的多余的空格或者字符。
<br>
验证是否配置成功可以在命令行中输入以下信息：<br>
`ssh -T git@github.com`<br>
如果出现如下反馈则配置成功：<br>
`Hi xxxxxxxx! You've successfully authenticated, but GitHub does not provide shell access.`<br>

## 使用
设置成功后就要步入使用缓解了，首先我们要设置自己的用户信息：<br>
$ git config --global user.name "xxxxxxxx"          //给自己起个用户名<br>
$ git config --global user.email  "xxxxxxxx"       //填写自己的邮箱

好了，那么我们如何开始自己在本地与线上联动呢？

1. 假设线上仓库地址为xxxx/xxxx.git 
2. 首先要做的就是克隆版本库：git clone git@github.com:xxxx/xxxx.git
3. 其次就是在git命令行中切换到本地的版本库，`git init`,此时项目文件夹中会出现一个.git的隐藏文件夹。
4. 然后如果想要修改某文件夹下的一个文件，就要这样操作了，比如修改的是OMOOC2py/0MOOC/git.md那么分别执行以下几个命令就可以了：

git add git.md ----> 本地和远端必须要有这个文件<br>
git commit -m "随便写一些注释，建议英文" ----> 添加注释并commit<br>
git push origin master ----> 推送到线上！

如此便可成功推送至线上！



## 体验
推送成功，在本地编辑非常的顺畅。在gitbook中也实现了实时的修改，特别提醒小伙伴们，关于SAMMARY.md的文件要时刻更新并且push哦，不然关于gitbook结构比较蒙圈儿的话可别怪我没有提醒啊，哈哈~
