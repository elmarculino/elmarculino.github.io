---
title: "Vim Personal Minimal Setup"
author: ["Marco Ribeiro"]
date: 2020-02-10
tags: ["vim"]
draft: false
---

Use Vim without your own .vimrc is not an easy task. Trainning to a certification test I was forced to use an virtual machine without my customizations. So, I had to find an minimal setup that would make the default Vim usable for me. That one-liner is what I type every time I open Vim without my config:

```sh
set nocp rnu ai et sw=4 ts=4 bs=2
```

To start Vim without loading your configs:

```sh
vim -u NONE
```

Each config option explained:

```sh
set nocp # nocompatible
set nu   # number
set rnu  # relativenumber
set et   # expandtab
set ai   # autoindent "automatic indentation
set ts=4 # tabstop
set sw=4 # shiftwidth
set bs=2 # backspace "allows the backspace to work
```
