---
layout: post
title: Python Argparse
subtitle: Python Argparse
categories: python
tags: [python]
---

# Python argparse

使用argparse解析python命令參數

```Python
import argparse

parser = ArgumentParser(prog=None, usage=None, description=None, epilog=None)
```

prog: program name (程式名稱)
usage: how to use your program (default=None, it will replace with your program name) (如何使用這個程式)
description: describe about your program (介紹一下你的程式)
epilog: additional materials (額外的參考文件)

## 加入引數

add_argument

- 位置參數 (positional argument)
- 選擇性參數 (optional argument)

```Python
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("pos1", help="positional argument 1")
parser.add_argument("-o", "--optional-arg", help="optional argument", dest="opt", default="default")
parser.add_argument("--verbose", 
                    action="store_true", # 引數儲存為 boolean
                    help="詳細內容")
parser.add_argument("-v",
                    "--verbosity",
                    type=int,
                    choices=[0, 1, 2],
                    help="詳細內容的程度")
```

- 選項引數: 短型態"-", 長型態"--"
- default: 指定預設值
- dest: 指定解析後的變數名稱
- type: 輸入引數的型態; str, int
- required: 必須輸入的欄位; True, False
- help: 顯示在help的說明敘述
- narg: 指定引數數量
  - nargs=3：引數只能恰好是 3 個
  - nargs='?'：引數只能是 0 個或是 1 個
  - nargs='+'：引數至少 1 個（1 個或任意多個）
  - nargs='*'：引數可以是任意數量（0 個或任意多個
- action:
  - store_true: 只要輸入此引數就為 True，否則為 False
  - count: 引數例如 -vvv
- choice: 引數只能是特定幾個值、或者是有範圍的值

### 互斥類型的開關

```Python
group = parser.add_mutually_exclusive_group()
group.add_argument("-v",
                   "--verbose",
                   action="store_true",
                   help="開啟囉唆模式")
group.add_argument("-q",
                   "--quiet",
                   action="store_true",
                   help="開啟安靜模式")
```

## 取得引數資料: parse_args

從 parser 取得引數資料後，此函數會回傳 Namespace 物件

```Python
args = parser.parse_args()
print("positional arg:", args.pos1)
print("optional arg:", args.opt)
```

## Subcommand

- ArgumentParser.add_subparsers去建立一個 “group”，ls_parser 、 man_parser 和 echo_parser 都是這個 group 下的 parser

- 使用 subcmd 這個 group 下的 add_parser 去建立 parser。回傳的會是一個 ArgumentParser

```Python
#!/usr/bin/env python3
# coding: utf8
import sys
import subprocess
import argparse
from pathlib import Path


def ls(path, flags=None):
    if not flags:
        flags = []
    if ~path.is_dir() or ~path.exists():
        print(f'{path!s} does not exist or is not a directory')
        return 1
    cmd = ['ls'] + flags + [str(path)]
    return subprocess.call(cmd)


def man(what, n=1):
    cmd = ['man'] + [str(n)] + [what]
    return subprocess.call(cmd)


def echo(msg):
    print(msg)
    return 0


def _build_parser():
    parser = argparse.ArgumentParser()
    subcmd = parser.add_subparsers(
        dest='subcmd', help='subcommands', metavar='SUBCOMMAND')
    subcmd.required = True

    # ls
    ls_parser = subcmd.add_parser('ls',
                                  help='listing given directory')
    ls_parser.add_argument('path',
                           type=Path,
                           help='path of the directory',
                           metavar='DIR')
    ls_parser.add_argument('--flag',
                           dest='flags',
                           help='flag for ls command (multiple flag)',
                           action='append')
    # man
    man_parser = subcmd.add_parser('man',
                                   help='show man page')
    man_parser.add_argument('what')
    man_parser.add_argument('-n', type=int, help='section number')

    # echo
    echo_parser = subcmd.add_parser('echo',
                                    help='echo a given message')
    echo_parser.add_argument('msg', help='the message', metavar='\'MESSAGE\'')
    return parser


if __name__ == '__main__':
    parser = _build_parser()
    args = parser.parse_args()

    if args.subcmd == 'ls':
        ret = ls(args.path, args.flags)
    elif args.subcmd == 'man':
        ret = man(args.what, n=args.n)
    else:
        ret = echo(args.msg)

    sys.exit(ret)
```

## 其他套件 click

<https://github.com/pallets/click>

Reference:

<https://dboyliao.medium.com/python-%E8%B6%85%E5%A5%BD%E7%94%A8%E6%A8%99%E6%BA%96%E5%87%BD%E5%BC%8F%E5%BA%AB-argparse-4eab2e9dcc69>

<https://haosquare.com/python-argparse/#%E6%8C%87%E5%AE%9A%E5%BC%95%E6%95%B8%E6%95%B8%E9%87%8F>
