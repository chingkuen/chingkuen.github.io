---
layout: post
title: Git branch
subtitle: usage of git branch and switch branch
categories: git
tags: [git]
---

# Git branch

Reference

## 建立分支

- git branch [Branch_Name]
    建立分支，但目前工作目錄維持在自己的分

- git branch -b [Branch_Name]
    建立分支，並將目前工作目錄切換到新的分支

## 切換分支

- git checkout [Branch_Name]
    切換到其他分支

## 刪除分支

- git branch -d [Branch_Name]
    須先切換到其他分支後，再刪除你這個分支

- git branch -D [Branch_Name]
    -D: Shortcut for --delete --force

## 查看分支

- git branch

## detached HEAD

這是一種「目前工作目錄不在最新版」的提示，你可以隨時切換到 Git 儲存庫的任意版本，但是由於這個版本已經有「下一版」，所以如果你在目前的「舊版」執行 git commit 的話，就會導致這個新版本無法被追蹤變更，所以建議不要這麼做