---
layout: post
title: Git revert
subtitle: usage of git revert and revert commit
categories: git
tags: [git]
---
# 修正git commit過的版本

## 重置目前的工作目錄

- git reset

## 刪除 HEAD 這個版本

- git reset --hard "HEAD^"
^ 是特殊符號，所以必須用雙引號括起來！

- git reset --soft "HEAD^"
刪除最近一次的版本紀錄，但留下最後一次版本變更的異動內容

## 刪除最近一次的版本，但保留最後一次的變更

- git reset --hard ORIG_HEAD

## 還原其中一個被改壞的檔案

- git checkout master [file_name]

## 重新提交一次最後一個版本 (即 HEAD 版本)

- git commit --amend (-m "message")

## 建立暫存版本

- git stash

## 查出該版本的相關資訊

- git show [commit_id]

## 修改與原本的變更相反

- git revert [commit_id] (-m "message")
原本修改a變b, 會改成b變回a, 並且直接建立commit版本 <br>
Note: 發生衝突時，需先修改後執行git add
  - git revert --continue

  - git revert --abort
  
  - git revert --skip
  
  - git revert -n
  <br>不直接建立commit版本
  
