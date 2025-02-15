# <center>MacOS配置指南</center>
## zsh简介与配置
## Python配置指南
## homebrew简介与配置
## git简介与配置
## SSH简介与配置
## v2ray简介与配置
<br>
zsh配置文件
要在zsh中配置环境变量，你可以编辑 ~/.zshrc 文件，并添加你的环境变量设置
.zshrc 文件将位于用户主目录或 ~/ 中

zsh 配置文件
zsh 的配置文件用于定制和配置 shell 的行为，根据存放的目录和使用场景，有以下配置文件

系统范围的配置文件
系统范围的配置文件，对所有用户都生效

/etc/zshenv
执行时机： 在每次 zsh 启动时都会执行
用途： 用于设置全局环境变量
/etc/zshrc
执行时机： 在每次交互式启动 zsh 时被执行
用途： 用于配置终端外观、添加别名、定义函数等
/etc/zlogin
执行时机： 在用户登录时（非交互式）被执行
用途： 用于设置登录时的全局行为，如显示系统信息等
/etc/zlogout
执行时机： 在用户注销时被执行
用途： 用于设置注销时的全局行为
用户级别的配置文件
用户级别的配置文件，对每个用户都生效，可以通过 echo $ZDOTDIR 命令查看当前用户的配置文件存放目录

~/.zshenv
执行时机： 在每次 zsh 启动时都会执行
用途： 用于设置用户特定的环境变量和个人偏好设置
~/.zshrc (推荐使用的配置文件)
执行时机： 在每次交互式启动 zsh 时被执行
用途： 用户可以在这里定制个人的 shell 环境，例如添加个人别名、自定义提示符等
~/.zlogin
执行时机： 在用户登录时（非交互式）被执行
用途： 用户可以在这里添加个人登录时需要执行的命令
~/.zlogout
执行时机： 在用户注销时被执行
用途： 用户可以在这里添加个人注销时需要执行的命令









安装homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

设置环境变量
echo 'export PATH="/opt/homebrew/bin:$PATH"' >> ~/.bash_profile 
source ~/.bash_profile

echo 'export PATH="/opt/homebrew/bin:$PATH"' >> ~/.zshrc   
source ~/.zshrc

echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"

Homebrew设置代理
brew用curl下载，所以给curl挂上socks5的代理即可。
在~/.curlrc文件中输入代理地址即可。
socks5 = "127.0.0.1:1080"



安装git
brew install git

git使用教程
git配置用户名和邮箱，用户名和邮箱地址是本地git客户端的一个变量 . 用户每次提交代码都会记录用户名和邮箱，这两条命令是配置 Git 的全局用户名和邮箱，在进行版本控制时用于记录用户身份信息。Git在commit信息中会显示提交人及其邮箱地址，方便追踪提交记录。因此这里的邮箱和用户名是为了回溯是谁提交的代码，并不需要一定填写GitHub的用户名和邮箱，甚至是可以随便填写的用户名和邮箱（当然，极其不建议这样做）

通过编辑 Git 的配置文件来进行用户名和邮箱的配置。在用户主目录下的 `~/.gitconfig` 文件中，可以找到以下内容：
[user]
    name = Your Username
    email = your.email@example.com
“`
你可以直接修改这些值来配置用户名和邮箱。



创建远程仓库并clone到本地，本地仓库自动与远程仓库同名
github创建远程仓库只能通过github实现,不能在git本地操作实现
创建并初始化本地仓库，github创建一个远程仓库，
本地仓库与远程仓库关联
先修改远程仓库名，在修改本地仓库名




git clone 克隆项目;初始化一个本地仓库git init


在工作区修改项目

提交本地修改
git add 保存修改到暂存区
git commit 保存修改到仓库



git push 提交到远程仓库





本地仓库关联远程仓库
git remote add origin git@github.com:YZ/helloTest.git


先将关联后的github仓库中的代码pull下来
git pull origin master

将最新的修改推送到远程仓库 将本地仓库的文件推送到远程仓库
git push -u origin master


SSH关联GitHub仓库
生成SSH Key：ssh-keygen -t rsa -C "本人GitHub绑定的邮箱" # 默认一路回车不要设置密码
在GitHub添加SSH Key



















配置git代理
首先需要查看自己梯子节点的端口号[port]

全局http、https代理设置
git config --global http.proxy http://127.0.0.1:[port]
git config --global https.proxy https://127.0.0.1:[port]

只对GitHub进行http、https代理
git config --global http.https://github.com.proxy https://127.0.0.1:[port]
git config --global https.https://github.com.proxy https://127.0.0.1:[port]



全局socks5代理设置
git config --global http.proxy socks5://127.0.0.1:[port]
git config --global https.proxy socks5://127.0.0.1:[port]

只对GitHub进行socks5代理
git config --global http.https://github.com.proxy socks5://127.0.0.1:[port]
git config --global https.https://github.com.proxy socks5://127.0.0.1:[port]

取消代理
git config --global --unset http.proxy
git config --global --unset https.proxy

查看已有配置
git config --global -l




Git 的全局配置文件通常位于 ~/.gitconfig
[http]
    proxy = http://代理地址:端口
[https]
    proxy = http://代理地址:端口


每个 Git 仓库中都有一个 .git/config 文件，代理设置仅对当前仓库生效
[http]
 proxy = http://代理地址:端口
[https]
 proxy = http://代理地址:端口









SSH使用
获取VPS信息：用户名@服务器IP地址 -p 端口号；密码
启动服务器的SSH服务，ssh_config和sshd_config都是ssh服务器的配置文件，二者区别在于前者是针对客户端的配置文件，后者则是针对服务端的配置文件
编辑SSH配置文件
PasswordAuthentication yes                         #启用密码验证
PubkeyAuthentication yes                           #启用密钥对验证
AuthorizedKeysFile  .ssh/ authorized_keys         #指定公钥库文件.
RSAAuthentication yes


修改端口
设置允许登录的用户及条件
开启密码登录
开启蜜月登录








SSH密码登录
ssh 客户端用户名@服务器ip地址
输入远程主机的密码



SSH密钥登录
在本地生成密钥对：使用ssh-keygen命令生成密钥对
将本地公钥复制到远程主机中：将本地公钥写到服务器的 ~/.ssh/authorized_key文件中
配置SSH密钥，目的是将添加到远程服务器连接白名单，让服务器知道是已认证的电脑在连接。过程类似于 GitHub 网站添加本地电脑的 SSH 公钥

使用命令将公钥上传到 VPS
macOS:ssh-copy-id user@服务器IP地址 -p port
windows系统：ssh user@服务器IP地址 -p port 'mkdir -p .ssh && cat >> .ssh/authorized_keys' < ~/.ssh/id_rsa.pub
手动进行操作，先复制公钥，再登录 VPS ，粘贴到 .ssh/authorized_keys 中。

SSH证书认证登录



腾讯云VPS IP地址：118.24.120.184
ssh root@118.24.120.184
password：Zxs123456



linux安装配置v2ray：apt-get install v2ray
设置v2ray本地代理：/etc/v2ray/config.json,直接把桌面客户端的vmss配置文件复制过来就可以
启动 V2Ray 进程:运行 service v2ray start,自动后台运行：systemctl start v2ray  
VPS git配置代理：git config --global https.proxy https://127.0.0.1:port
