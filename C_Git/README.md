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

## 上传到远程仓库Giuhub：

```git
    echo "# HCPigg" >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git remote add origin https://github.com/QK-HuaChong/HCPigg.git
    git push -u origin master
```

## 配置代理：

```git
git config --global http.proxy 192.168.6.3:808
git config --global https.proxy 192.168.6.3:808
```
