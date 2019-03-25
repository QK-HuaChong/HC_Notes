# Git

## 创建新仓库

```git
    git init
```

## 克隆仓库

* 克隆本地的：

```git
    git clone /path/to/repository
```

* 克隆远程仓库：

```git
    git clone username@host:/path/to/repository
```

## 添加与提交

```git
    git add <filename> 添加指定文件
    git add *          添加所有文件

    git commit -m '代码提交添加的说明信息'   提交到Head上
```

## 提送改动

```git
    git push origin master <--->  master可以是其他分支

    git remote add origin <server> <---> 连接到指定的远程仓库
```

## 分支管理

```git

    1.创建一个叫做“feature_x”的分支，并切换过去：
    git checkout -b feature_x
    2.切换回主分支：
    git checkout master
    3.再把新建的分支删掉：
    git branch -d feature_x
    4.除非你将分支推送到远端仓库，不然该分支就是 不为他人所见的：
    git push origin <branch>
```

## 更新与合并

```git
    1. 更新本地仓库：
    git pull
    2.合并其他分支到你的当前分支（例如 master），执行：
    git merge <branch>
```

## 标签

```git
    创建的标签：
    git tag 1.0.0 1b2e1d63ff
```

## 上传到远程仓库Giuhub：

```git
    echo "# HCPigg" >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git remote add origin https://github.com/QK-HuaChong/HCPigg.git
    git push -u origin master
```

## 配置（取消）代理：

```git
git config --global http.proxy 192.168.6.3:808
git config --global https.proxy 192.168.6.3:808

git config --global --unset http.proxy
git config --global --unset https.proxy

```
