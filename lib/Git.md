[Git-Book](https://git-scm.com/book/zh/v2/)    


请记住，你工作目录下的每一个文件都不外乎这两种状态：**已跟踪** 或 **未跟踪**。 已跟踪的文件是指那些被纳入了版本控制的文件，在上一次快照中有它们的记录，在工作一段时间后， 它们的状态可能是未修改，已修改或已放入暂存区。简而言之，已跟踪的文件就是 Git 已经知道的文件。

工作目录中除已跟踪文件外的其它所有文件都属于未跟踪文件，它们既不存在于上次快照的记录中，也没有被放入暂存区。 初次克隆某个仓库的时候，工作目录中的所有文件都属于已跟踪文件，并处于未修改状态，因为 Git 刚刚检出了它们， 而你尚未编辑过它们。


#### $ cat ~/.gitconfig      

```bash
[init]
        defaultBranch = main
[user]
        name = at337am
        email = lueqit@gmail.com
[alias]
        co = checkout
        br = branch
        ci = commit
        sw = switch
        st = status
        lg = log --oneline --graph --decorate --all
        last = log -1 HEAD
        count = rev-list --count HEAD
        wip = commit -m "WIP"
        rhh = reset --hard
        rhs = reset --soft
        save = stash save
        saves = stash list
        apply = stash apply
        pom = push origin main
```       

如果是 oh-my-zsh 则已经内置了很多 alias 了   

##### 关于stash       

“你原来在 dev1 分支开发，然后突然要去 dev2 改个 bug ，但是 dev1 分支没开发完不想提交，那就先 stash”          

“如果用 idea ，建议用 shelf ，stash 只能把所有未提交的处理。shelf 可以拆分选择指定的处理”      



#### 撤回上一次提交      

撤回提交并保留更改（软重置）     

`git reset --soft HEAD~1`    

撤回提交并丢弃更改（硬重置）         

`git reset --hard HEAD~1`


#### wip           

暂时提交   

`git add .`   
`git wip`         

撤回上次提交 软重置    

`git rhs HEAD^`



#### 在提交时忽略文件的更改但仍将其提交到仓库      

**本地生效**     

```bash
git update-index --assume-unchanged src/main/resources/application.yml
```     




#### 基本命令

- git init
- git status
- git log
- git add .
- git commit -m "<描述>"
- git branch`显示本地分支`
- git branch -v`显示本地分支和最后一次提交`
- git branch -r`显示远程分支`
- git branch <新分支名>`新建分支`
- git checkout <分支名>`切换分支`
- git checkout -b <新分支名>`新建一个本地分支并切换到该分支`
- git branch -d <分支名>`删除分支`
- git remote -v`显示远程仓库名和对应的URL`
- git remote add <远程仓库名> <远程URL>`添加远程仓库`
- git remote remove <远程仓库名>`删除远程仓库`
- git push <远程仓库名> <目标分支>`推送到远程仓库`
- git fetch <远程仓库名> <目标分支>`拉取到FETCH_HEAD中但不合并`
- git log FETCH_HEAD`显示拉取来的log信息`
- git merge FETCH_HEAD`将拉取过来的合并到当前分支`
- git pull <远程仓库名> <目标分支>`拉取并合并`
- git diff <本地分支1> <本地分支2>`比较本地两个分支的差异`
- git diff <远程分支名> <本地分支名>`比较远程和本地分支的差异`      


查看分支       

```bash
git branch
```

新建分支     

```bash
git branch mjj
```

撤销已跟踪文件的修改  

```bash
git checkout -- .
```   

强制推送   

```bash
git push origin main --force
```       




#### 第一次使用git 全局配置     

- `git config --global init.defaultBranch main`        

- `git config --global user.name "at337am"`    
- `git config --global user.email "lueqit@gmail.com"`             

- `git config --global https.proxy http://127.0.0.1:2081`     
- `git config --global http.proxy http://127.0.0.1:2081`       

#### 查看当前用户信息      

- git config user.name  

- git config user.email  

#### 列出当前配置+全局配置+系统配置          

- git config --list            

- git config --global --list  

- git config --system --list  


