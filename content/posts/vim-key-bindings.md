---
title: "Vim Key Bindings"
author: ["Marco Ribeiro"]
date: 2020-01-10
tags: ["vim", "shortcuts"]
draft: false
---

Vim Command Language and examples of how to get things done.


### Verbs {#verbs}

```nil
v : visual
c : change
d : delete
y : yank/copy
```


### Modifiers {#modifiers}

```nil
i : inside
a : around
t : till..finds a character
f : find..like till except including the char
/ : search..find a string/regex
```


### Text Objects {#text-objects}

```nil
w : word
s : sentence
p : paragraph
b : block/parentheses,
t : tag, works for html/xml
```


## VIM Shortcuts {#vim-shortcuts}


### Navigation {#navigation}

```nil
zz  : current line to top
zt  : current line to middle
zb  : current line to bottom

C+y : scroll up one line
C+e : scroll down one line
C+u : scroll up half-page
C+d : scroll down half-page
C+b : scroll up full-page
C+f : scroll down full-page

H   : cursor to the top of the screen
M   : cursor to the middle of the screen
L   : cursor to the botton of the screen

e   : go to the end of the current word.
E   : go to the end of the current WORD.
b   : go to the previous (before) word.
B   : go to the previous (before) WORD.
w   : go to the next word.
W   : go to the next WORD.
g;  : go to the last editing place.

0   : beginning of line
^   : first char of line
$   : end of line

{   : Go to the beginning of the current paragraph.
}   : Go to the end of the current paragraph.

/i  : Search to the next occurrence of it.
?i  : Search to the previous occurrence of it.
–   : Go to the next occurrence of the current word under the cursor.
#   : Go to the previous occurrence of the current word under the cursor.

%   : Go to the matching braces, or parenthesis inside code.
```


### Folding {#folding}

```nil
zf#j      : creates a fold from the cursor down # lines.
zf/string : creates a fold from the cursor to string .
za        : opens/closes all folds
zj        : moves the cursor to the next fold
zk        : moves the cursor to the previous fold
zc        : closes a fold at the cursor
zo        : opens a fold at the cursor
zO        : opens all folds at the cursor
zm        : increases the foldlevel by one
zM        : closes all open folds
zr        : decreases the foldlevel by one
zR        : decreases the foldlevel to zero — all folds will be open
zd        : deletes the fold at the cursor
zE        : deletes all folds
[z        : move to start of open fold
]z        : move to end of open fold
```


### Jump {#jump}

```nil
C+o : go to origin
```


### Marks {#marks}

```nil
m + letter : create mark
' + letter : go to mark
```


### Yank / Paste {#yank-paste}

```nil
:reg : list registers
"1p  : paste previous deletes/yanks

yiw  : Yank inner word (copy word under cursor, say "first").
viwp : Select "second", then replace it with "first".

yi(  : equivalent to yib, yanks the contents inside parenthesis.
yi{  : equivalent to yiB, yanks the contents inside braces.
```


### Insert Multiple {#insert-multiple}

```nil
80i/<ESC>    : insert 80 '/' in a line
20Otest<ESC> : insert 20 lines of 'test'
```


### Change Multiple {#change-multiple}

```nil
 *      : to select all words
cgn+Esc : to change de word
.       : to change the next

Esc     : to enter 'command mode'
C-v     : to enter visual block mode and select the columns of text.
M-i     : to enter insert mode and type the text you want to insert.
Esc     : wait 1 second and the inserted text will appear on every line.

:%s/foo/bar/g
:s/foo/bar/g
:%s/foo/bar/gc
```


### Selection {#selection}

```nil
ggVG : select all
```


### Letter Case {#letter-case}

```nil
~    : changes the case of current character
guu  : change current line from upper to lower.
gUU  : change current LINE from lower to upper.
guw  : change to end of current WORD from upper to lower.
guaw : change all of current WORD to lower.
gUw  : change to end of current WORD from lower to upper.
gUaw : change all of current WORD to upper.
g~~  : invert case to entire line
guG  : change to lowercase until the end of document.
```


### Split {#split}

```nil
:sp           : horizontal split
:vs           : vertical split

C+W S         : horizontal splitting
C+W v         : vertical splitting
C+W q         : close split
C+W C+W       : switch between windows
C+W J K, H, L : switch to adjacent window ( up, down, left, right )

C-w t C-w K   : change two vertically split windows to horizonally split
C-w t C-w H   : Horizontally to vertically

C-w t         : makes the first (topleft) window current
C-w K         : moves the current window to full-width at the very top
C-w H         : moves the current window to full-height at far left
```


### Tags {#tags}


### Spaces {#spaces}

```nil
:%le	: Remove left spaces in the entire file
```


### Macros {#macros}

```nil
qd : start recording to register d
q  : stop recording
@d : execute your macro
@@ : execute your macro again
```


## VIM Plugins {#vim-plugins}


### Prettier {#prettier}

```nil
L-p : Manually trigger Prettier
```


### FZF {#fzf}

```nil
C-t : tab split
C-x : split
C-v : vsplit
```


### Surround {#surround}

```nil
cs"'  : replace " with '
cst"  : replace tag with "
ds"   : to remove " delimiters entirely.
ysiw] : add brackets arround a word.
cs]{  : add some space (use } instead of { for no space): cs]{
yssb  : wrap the entire line in parentheses with yssb or yss).
```


### Commenter {#commenter}

```nil
L-cc       : Comment out the current line or text selected in visual mode.
L-cn       : Same as cc but forces nesting.
L-c<space> : Toggles the comment state of the selected line(s).
L-cm       : Comments the given lines using only one set of multipart delimiters.
L-ci       : Toggles the comment state of the selected line(s) individually.
L-cs       : Comments out the selected lines with a pretty block formatted layout.
L-cy       : Same as cc except that the commented line(s) are yanked first.
L-c$       : Comments the current line from the cursor to the end of line.
L-cA       : Adds comment delimiters to the end of line and goes into insert mode between them.
L-ca       : Switches to the alternative set of delimiters.
L-cl       : Delimiters are aligned down the left side (<leader>cl) or both sides (<leader>cb).
L-cu       : Uncomments the selected line(s).
```


### vim-easy-align {#vim-easy-align}

```nil
vipga=  : visual-select inner paragraph, Start EasyAlign (ga), Align around =
gaip=   : Start EasyAlign for inner paragraph, Align around =
=       : Around the 1st occurrences
2=      : Around the 2nd occurrences
*=      : Around all occurrences
**=     : Left/Right alternating alignment around all occurrences
<Enter> : Switching between left/right/center alignment modes
```


### splitjoin.vim {#splitjoin-dot-vim}

```nil
gS : to split a one-liner into multiple lines
gJ : to join a block into a single-line statement.
```
