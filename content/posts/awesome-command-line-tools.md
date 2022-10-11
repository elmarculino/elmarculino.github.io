+++
title = "Best command line tools"
author = ["Marco Ribeiro"]
date = 2020-02-10
draft = false
+++

## [broot](https://github.com/Canop/broot) {#broot}

```sh
br -dp # replace 'ls', display dates and permissions
br -s  # to identify what is taking disk space
:gf    # display git statuses
```


## [fasd](https://github.com/clvv/fasd) {#fasd}

```sh
alias a='fasd -a'        # any
alias s='fasd -si'       # show / search / select
alias d='fasd -d'        # directory
alias f='fasd -f'        # file
alias sd='fasd -sid'     # interactive directory selection
alias sf='fasd -sif'     # interactive file selection
alias z='fasd_cd -d'     # cd, same functionality as j in autojump
alias zz='fasd_cd -d -i' # cd with interactive selection
alias v='f -e vim'       # quick opening files with vim
```


## [fd](https://github.com/sharkdp/fd) {#fd}

```sh
# Convert all jpg files to png files:
fd -e jpg -x convert {} {.}.png

fd passwd /etc   # Searching 'passwd' in the /etc folder
fd -e md         # Searching for a particular file extension
fd -H pre-commit # Include hidden files
fd -E '*.bak'    # Excluding  specific files or directories
```


## [fzf](//github.com/junegunn/fzf) {#fzf--github-dot-com-junegunn-fzf}

```sh
vim **<TAB>       # Select multiple items with TAB key
fd --type f | fzf # Feed the output of fd into fzf

# Setting fd as the default source for fzf
export FZF_DEFAULT_COMMAND='fd --type f'
```


## [ripgrep](https://github.com/BurntSushi/ripgrep) {#ripgrep}

```sh
rg 'fast\w+' README.md
```
