#                   Git 个人整理

参考资料: https://www.liaoxuefeng.com/wiki/896043488029600

## GIT（分布式版本控制系统）

Git(由C语言开发的)是一个开源的分布式版本控制系统，可以有效、高速地处理从很小到非常大的项目版本管理。

#### Git的功能特性：

###### 从一般开发者的角度来看，git有以下功能：

1、从服务器上克隆完整的Git仓库（包括代码和版本信息）到单机上。

2、在自己的机器上根据不同的开发目的，创建分支，修改代码。

3、在单机上自己创建的分支上提交代码。

4、在单机上合并分支。

5、把服务器上最新版的代码fetch下来，然后跟自己的主分支合并。

6、生成补丁（patch），把补丁发送给主开发者。

7、看主开发者的反馈，如果主开发者发现两个一般开发者之间有冲突（他们之间可以合作解决的冲突），就会要求他们先解决冲突，然后再由其中一个人提交。如果主开发者可以自己解决，或者没有冲突，就通过。

8、一般开发者之间解决冲突的方法，开发者之间可以使用pull 命令解决冲突，解决完冲突之后再向主开发者提交补丁。

###### 从主开发者的角度（假设主开发者不用开发代码）看，git有以下功能：

1、查看邮件或者通过其它方式查看一般开发者的提交状态。

2、打上补丁，解决冲突（可以自己解决，也可以要求开发者之间解决以后再重新提交，如果是开源项目，还要决定哪些补丁有用，哪些不用）。

3、向公共服务器提交结果，然后通知所有开发人员。

###### 优点：

适合[分布式开发](https://baike.baidu.com/item/分布式开发)，强调个体。

公共服务器压力和数据量都不会太大。

速度快、灵活。

任意两个开发者之间可以很容易的解决冲突。

离线工作。

###### 缺点：

资料少（起码中文资料很少）。

学习周期相对而言比较长。

不符合常规思维。

代码保密性差，一旦开发者把整个库克隆下来就可以完全公开所有代码和版本信息。

#### 集中式vs分布式

###### 集中式版本控制系统 

 版本库是集中存放在中央服务器的，而干活的时候，用的都是自己的电脑，所以要先从中央服务器取得最新的版本，然后开始干活，干完活了，再把自己的活推送给中央服务器

###### 分布式版本控制系统

分布式版本控制系统根本没有“中央服务器”，每个人的电脑上都是一个完整的版本库，这样，你工作的时候，就不需要联网了，因为版本库就在你自己的电脑上。既然每个人电脑上都有一个完整的版本库，那多个人如何协作呢？比方说你在自己电脑上改了文件A，你的同事也在他的电脑上改了文件A，这时，你们俩之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。

和集中式版本控制系统相比，分布式版本控制系统的安全性要高很多，因为每个人电脑里都有完整的版本库，某一个人的电脑坏掉了不要紧，随便从其他人那里复制一个就可以了。而集中式版本控制系统的中央服务器要是出了问题，所有人都没法干活了。

在实际使用分布式版本控制系统的时候，其实很少在两人之间的电脑上推送版本库的修改，因为可能你们俩不在一个局域网内，两台电脑互相访问不了，也可能今天你的同事病了，他的电脑压根没有开机。因此，分布式版本控制系统通常也有一台充当“中央服务器”的电脑，但这个服务器的作用仅仅是用来方便“交换”大家的修改，没有它大家也一样干活，只是交换修改不方便而已。

## 安装Git

安装完成后，还需要最后一步设置，在命令行输入：

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

注意`git config`命令的`--global`参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

## 创建版本库

###### 创建一个版本库非常简单

首先，选择一个合适的地方，创建一个空目录：

```java
$ cd d:\\lll\\git\\learngit1      // cd 切换目录

admin@A16 MINGW64 /d/lll/git/learngit1
$ pwd                            // pwd 查看当前目录
/d/lll/git/learngit1

admin@A16 MINGW64 /d/lll/git/learngit1
$ git init                       
Initialized empty Git repository in D:/LLL/git/learngit1/.git/
  
admin@A16 MINGW64 /d/lll/git/learngit1 (master)
$ ls -ah                        //查看文件 包括隐藏文件
./  ../  .git/



```

`git init`命令把这个目录变成Git可以管理的仓库

瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者可以发现当前目录下多了一个`.git`的目录，这个目录是Git来跟踪管理版本库的

###### 把文件添加到版本库

第一步，用命令`git add`告诉Git，把文件添加到仓库：

```
$ git add readme.txt
```

第二步，用命令`git commit`告诉Git，把文件提交到仓库：

```
$ git commit -m "wrote a readme file"
[master (root-commit) f319e18] wrote a readme file
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 readme.txt

```

`git commit`命令，`-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。

## 时光机穿梭

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")

```

`git status`命令可以让我们时刻掌握仓库当前的状态

```
$ git diff
diff --git a/readme.txt b/readme.txt
index e69de29..4b9a8a2 100644
--- a/readme.txt
+++ b/readme.txt
@@ -0,0 +1 @@
+aaaaaaa
\ No newline at end of file
```

`git diff`顾名思义就是查看difference  

### 生成SSH key 

```
ssh-keygen -t rsa -C “邮箱地址”
```

输入命令，一直回车 ,找到.ssh目录有两个文件,Github上点击“setting”，找到添加SSH key的菜单，然后新增SSH key；把文件id_rsa.pub 里面的内容全部复制到 key编辑框中，保存完毕.