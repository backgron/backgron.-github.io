---
title: git和github
date: 2021-05-20 23:04:26
tags:
  - git和github
categories:
  - 其他
  - git和github
description:  git和github
---

# git和github的基本使用

## Git

### 基本信息

git 是分布式版本控制系统，联网运行，支持多人协作，性能高

### 特点：

+ 服务器保存文件的所有更新版本
+ 客户端是服务器的完整备份，并不是只保留文件的最新版本

### 优点：

+ 联网运行，支持多人协作开发
+ 客户端断网后支持离线本地提交版本更新
+ 服务器故障或损坏后，可以使用任何一个客户端的备份进行恢复

### git的记录快照

+ git快照是在原有文件版本的基础上重新生成一份新的文件，类似于备份。为了效率，如果文件没有修改，git不再重新存储该文件，而只是保留一个链接指向之前存储的文件
+ 优点：版本切换时非常块
+ 缺点：占用磁盘空间比较大

### 近乎所有操作都是本地执行的

+ 断网后可以在本地对项目进行版本修改
+ 联网后把本地修改记录同步到云端服务器

### git中的三个区域

+ 工作区：处理工作的区域
+ 暂存区：已完成的工作临时存放等待被提交的区域
+ git仓库：最终存放的区域

### git中的三种状态

+ 已修改 modified ：表示修改了文件，但是还没有将修改的结果放到暂存区
+ 一暂存 staged：表示已对修改文件的当前版本做了标记，使之包含在下次提交的列表中
+ 已提交 committed：表示文件已经安全地保存在本地的git仓库中

## 配置

### 配置自己的用户名和邮箱

+ git config --global user.name "name"
+ git config --global user.email "email@.cn"
+ 使用 --global选项，命令执行一次，即可永久生效 

### 检查配置信息

+ git config --list --global  //查看所有的全局配置
+ git config user.name    //查看指定的全局配置

### 获取帮助信息 ：git help <verb>

+ git help config   //打开浏览器帮助手册
+ git config -h   //在终端显示帮助信息

## Git 的基本操作

### 获取git仓库的两种方式

1. 将尚未进行版本控制的本地目录转换为git仓库
    + 右键打开git bash
    + git init
    + 创建成功后会创建一个隐藏的 .git 目录，即为当前项目的git仓库，里面有组成git仓库的必要文件
2. 从其他服务器克隆一个已存在的git仓库

### 工作区

工作区的文件可能有四种状态，分为两大类

+ 未被git管理
    + 未跟踪 Untracked：未被git管理的文件
+ 已被git管理
    + 未修改 Unmodified：工作区文件内容和git仓库一致
    + 已修改 Modified：工作区文件内容和git仓库不一致
    + 已暂存 Staged：工作区中被修改的文件已被放到暂存区，准备将修改后的文件保存到git仓库

### 检查文件状态

+ 检查文件状态
    + git status  
+ 以精简的方式查看文件状态
    + git status -s
    + git status --short

### 跟踪文件 / 放入暂存区 / 解决冲突

+ 跟踪一个文件
+ 把已跟踪的、且已修改的文件放到暂存区中
+ 把有冲突的文件标记为已解决
    + git add 文件名
    + git add .    //将新增、修改的文件全部放入暂存区

### 取消暂存的文件

+ 取消暂存的文件
    + git reset HEAD 文件名
    + git reset HEAD .  //移除暂存区所有文件

### 撤销对文件的修改

+ 把工作区对应文件的修改还原成git仓库中保存的版本
+ 所有的修改都会丢失，而且无法恢复
+ 危险性比较高，慎重使用
    + git checkout -- 文件名

### 提交更新

+ 提交更新
+ 提交已暂存的文件
    + git commit -m "描述信息"

### 跳过暂存区域

+ 跳过使用暂存区，直接将工作区的内容提交到git仓库
    + git commit -a -m "描述信息"

### 移除文件

+ 从git 仓库和工作区中同时移除文件
    + git rm -f 文件名
+ 只从git仓库中移除文件，保留工作区的文件
    + git rm --cached 文件名

### 查看提交历史

+ 按时间先后顺序列出所有提交历史，最近的排在最上面
    + git log
+ 只展示最新的n条提交历史
    + git log -n
+ 在一行上展示最近的两条历史
    + git log -2 --pretty=oneline
+ 在一行上展示最近两条提交历史的信息，并自定义输出格式
+ %h 提交简写的哈希值 %an 作者的名字 %ar 作者修订日期，按多久以前的方式显示 %s 提交说明
    + git log -2 --pretty=format:"%h | %an | %ar | %s"

### 回退到指定的版本

+ 在一行上展示所有的提交历史
    + git log --pretty=oneline
+ 根据指定的提交 ID 回退到指定版本
    + git reset --hard ID
+ 在旧版本中查看所有命令操作历史
    + git reflog --pretty=oneline
+ 再次根据最新的提交 ID，跳转到最新的版本
    + git rest --hard ID

### 忽略文件

 一般我们会有一些无需纳入git管理，也不希望他们总是出现在未跟踪列表，可以创建一个名未 .gitignore 的配置文件，列出要忽略的文件的匹配模式

文件 .gitignore 的格式规范

+ 以 # 开头的是注释
+ 以 / 结尾的是目录
+ 以 / 开头的防递归
+ 以 ! 开头表示取反
+ 可以使用glob模式进行文件和文件夹的匹配 (glob是简化了的正则表达式)
    + 星号* 匹配0个或者多个任意字符
    + [abc] 匹配任何一个列在方括号中的字符
    + 问号? 只匹配一个任意字符
    + [0-9]在方括号中使用短划线分割两个字符，表示在这两个字符范围内的都可以匹配
    + a/**/z 表示匹配任意中间目录 例如 a/z、a/b/z

## 开源和闭源

开源：开放源代码

闭源：封闭源代码

拥抱开源：开源可以让开发越来越完善，越来越简单

### 开源协议

1. GPL（GNU General Public License）
    + 具有传染性的一种开源协议，不允许修改后和衍生的代码作为闭源的商业软件发布和销售
    + 如 ： Linux
2. MIT（Massachusets Institute of Technology）
    + 是目前限制最少的协议，唯一的条件：再修改后的代码或者发行包中，必须包含原作者的许可信息
    + 如 Jquery、node.js
3. 还有更多的开源协议，百度

### 开源项目托管平台

+ Github ：全球最牛的开源项目托管平台
+ Gitlab： 对代码私有性支持较好，因此企业用户较多
+ Gitee：又叫码云，是国产开源项目托管平台，访问速度快，纯中文，使用友好

以上三个平台支支持Git管理的项目源代码

## Github平台

1. 注册并登录
2. 新建远程仓库
3. github远程仓库的两种访问方式
    + HTTPS：0配置，但每次访问仓库都需要输入账号密码
    + SSH：需要额外配置，但是不需要每次输入账号密码
    + 在实际开发中，推荐使用SSH的方式访问远程仓库

### github创建远程仓库

#### HTTPS 方式访问

1. 没有现成的git仓库
    + 使用终端命令创建README.md文档，并写入初始内容 “#仓库名''
        + echo ”# 仓库名“  >> README.md
    + 初始化本地的git仓库，并将文件提交到本地的git仓库
        + git init
        + git add README.md
        + git commit -m "first commit"
    + 将本地仓库和远程仓库进行关联，并把远程仓库命名为origin
        + git remote add origin git@github.com:backgron/study_github.git
    + 将本地仓库中的内容推送到远程的orgin仓库中
        + git push -u origin main
2. 本地有现成的git 仓库
    + 将本地仓库和远程仓库进行关联，并把远程仓库命名为origin
        + git remote add origin git@github.com:backgron/study_github.git
    + 将本地仓库中的内容推送到远程的orgin仓库中
        + git push -u origin main
3. 更新github远程仓库
    + 将本地仓库推送到github远程仓库
        + git push

#### SSH 方式访问

1. SSH key

    + SSH key的作用：实现本地仓库和GIthub之间免登录的加密数据传输
    + SSH key的好处：免登录身份认证、数据加密传输
    + SSH key由两部分组成：
        + id_rsa （私钥文件，存放于客户端电脑中即可）
        + id_rsa.pub（公钥文件，需要配置到github中）

2. 生成SSH key

    + 在Git Bash 中输入
        + ssh-keygen -t rsa -b 4096 -C "github账号邮箱"
        + 连续敲击3次回车，即可在C:\Users\用户名文件夹\ .ssh中僧成id_rsa和id_rsa.pub两个文件

3. 配置SSH key

    + 将id_rsa.pub中的内容复制添加到github账号setting中的SSH key中
    + 通过Git Bash验证是否成功
        + ssh -T git@github.com

4. 基于SSH 将本地仓库上传到Github

    + git remote add origin git@github.com:backgron/study2_github.git

    + git push -u origin main

#### 克隆仓库

1. 从要克隆的仓库得到对应的https或者ssh地址
2. Git Bash输入
    + git clone 地址

## Git 分支

### 基本信息

+ 在进行多人协作开发的时候，为了防止互相干扰，提高协同开发的体验，建议每个开发者都基于分支进行项目功能的开发

+ 在初始化本地git仓库时，git会帮我们创建一个main的分支

+ 通常main分支用来保存和记录整个项目已完成的功能代码

+ 不允许程序员直接在main分支上修改代码
+ 功能分支：专门用来开发新功能的分支，是临时从main分支上分出来的，开发完后需要合并到main分支上

### 本地分支操作

1. 查看分支列表
    + git branch
2. 创建新的分支 
    + git branch 分支名称
    + 基于当前分支创建一个新的分支，此时新分支和主分支代码完全相同
    + 执行完命令后，用户还是处于main主分支上，不会切换到新创建的分支上
3. 切换分支
    + git checkout 分支名称
4. 分支的快速创建和切换
    + git checkout -b 分支名称
    + -b 表示创建一个新分支
    + checkout 表示切换到刚才新创建的分支上
5. 合并分支  ！注意要先切换回主分支
    + 切换到master分支
        + git checkout main
    + 在main分支上运行以下代码
        + git merge 被合并的分支名称
6. 删除分支
    + git branch -d 分支名称
7. 遇到冲突时的分支合并
    + 如果在两个不同的分支中，对同一个文件进行了不同的修改，Git就没法干净的合并它们。此时，我们需要打开这些包含冲突的文件，然后手动解决冲突

### 远程分支操作

#### 将分支推送到远程仓库

1. -u 表示把本地分支和远程分支关联，只在第一次推送的时候需要带u
    + git push -u 远程仓库的别名 本地分支名称:本地分支别名
2. 如果希望远程分支的名称和本地保持一致，可以对命令进行简化
    + git push -u 远程仓库别名 本地分支名称
3. 只有第一次推送分支需要带 -u ，此后可以直接使用git push 推送代码到远程分支

#### 查看远程仓库所有分支

+ git remote show 远程仓库名字

#### 跟踪分支

1. 从远程仓库，把远程分支下载到本地仓库
    + git checkout 远程分支名称
2. 重命名
    + git checkout -b 本地分支名称 远程仓库名称/远程分支名称

#### 拉取远程分支的最新代码

1. 从远程仓库，拉取当前分支最新的代码，保持当前分支的代码和远程分支代码一致
    + git pull

#### 删除远程分支

1. 删除远程仓库中指定名称的远程分支
    + git push 远程仓库 --delete 远程分支

## 重点掌握

1. git中基本命令
    + git init
    + git add .
    + git commit -m "提交消息"
    + git status 和 git status -s
2. github创建维护远程仓库
    + 配置github的ssh访问
    + 将本地仓库上传到github
3. git分支
    + git checkout -b 新分支名称
    + git push -u origin 新分支名称
    + git checkout 分支名称
    + git branch