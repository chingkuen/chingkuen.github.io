---
layout: post
title: Git remote
subtitle: usage of git remote repository
categories: git
tags: [git]
---
# Git Remote Repository

在Github建立儲存庫(Repository)

## 將遠端儲存庫複製到本地

```git
git clone <remote_repository_link>
```

## 將本地儲存庫中目前分支推送到遠端儲存庫

```git
git remote add origin <remote_repository_link>
git push -u master
```

origin - 預設遠端分支的參照名稱

## 將遠端儲存庫的 master 分支取回

- git pull

```git
git pull origin master
```

--allow-unrelated-histories 允許 Git 合併沒有共同祖先的分支。

> git pull等於git fetch及git merge

- git fetch

將遠端儲存庫的最新版下載回來，下載的內容包含完整的物件儲存庫(object storage)。 這個命令不包含「合併」分支的動作。

```git
git fetch
git merge origin/master
```

## 本地儲存庫上傳

第一次上傳

```git
git push origin master
```

第二次及以後:

```git
git push
```

指定 push 的方法。詳細說明請參見 git help config

--set-upstream 參數，即可將本地分支註冊進 .git/config 設定檔

```git
git push --set-upstream origin <local_branch>
```

```git
git config --global push.default simple
```

## 列出目前註冊在工作目錄裡的遠端儲存庫資訊

```git
git remote -v
```

## 顯示特定遠端儲存庫的參照名稱

```git
git ls-remote
```
