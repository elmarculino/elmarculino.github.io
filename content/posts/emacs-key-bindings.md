+++
title = "Emacs Key Bindings"
author = ["Marco Ribeiro"]
date = 2020-01-10
draft = false
+++

## Emacs Key Biddings {#emacs-key-biddings}

1.  C-x reserved for Emacs native essential keybindings: buffer, window, frame, file, directory, etc…
2.  C-c reserved for user and major mode:
    -   C-c letter reserved for user. &lt;F5&gt;-&lt;F9&gt; reserved for user.
    -   C-c C-letter reserved for major mode.
3.  Don't rebind C-g, C-h and ESC.

4.  Examples:
    -   C-x C-f	find-file: first prompts for a filename and then loads that file into a editor buffer of the same name
    -   C-x C-s	save-buffer: saves the buffer into the associated filename
    -   C-x C-w	write-named-file: prompts for a new filename and writes the buffer into it
    -   C-x b      switch-to-buffer: display a different buffer on the screen
    -   C-x o      other-window: move the cursor to the other window
    -   C-x C-b	list-buffers: lists those buffers currently loaded into emacs
    -   C-g        to cancel any action you have started.


## Doom Emacs Key Bindings {#doom-emacs-key-bindings}

-   SPC h b b    Abre lista de atalhos de teclado
-   M-d          Cria multiplos cursores
-   SPC h v      Able lista de variaveis


### evil-snipe <span class="tag"><span class="navigation">navigation</span></span> {#evil-snipe}

f or t
; - next
, - previous


### avy <span class="tag"><span class="navigation">navigation</span></span> {#avy}

g s SPC - Começa a busca no buffer pelo avy


### evil-lion {#evil-lion}

glip=  # gl - left align operator, ip - text paragraph, = separator
gLip,  # gL - right align operator, ',' separator


### Org Mode {#org-mode}

[Org Mode Key Bindings](https://orgmode.org/orgcard.txt)

C-M-i      (complete-symbol) complete word at point
C-c '      for editing the current code block.


#### [setting tags](https://orgmode.org/manual/setting-tags.html) {#setting-tags}

C-c C-q     (org-set-tags-command) enter new tags for the current headline.


#### [handling links](https://www.gnu.org/software/emacs/manual/html_node/org/handling-links.html) {#handling-links}

C-c C-l     (org-insert-link) insert a link.


#### [property syntax](https://orgmode.org/manual/property-syntax.html) {#property-syntax}

C-c C-x p     (org-set-property) set a property.
C-c C-c s     (org-set-property) set a property in the current entry.
C-c C-c d     (org-delete-property) remove a property from the current entry.


#### [structure editing](https://orgmode.org/manual/structure-editing.html) {#structure-editing}

C-c C-x C-w     (org-cut-subtree) kill subtree.
C-c C-x M-w     (org-copy-subtree) copy subtree to kill ring.
C-c C-x C-y     (org-paste-subtree) yank subtree from kill ring.
C-c C-x c       (org-clone-subtree-with-time-shift) Clone a subtree by making a number of sibling copies of it.
C-c C-w         (org-refile) Refile entry or region to a different location.


## doom emacs links {#doom-emacs-links}

[doom emacs workflows](https://noelwelsh.com/posts/2019-01-10-doom-emacs.html)
[emacs doom for newbies](https://medium.com/urbint-engineering/emacs-doom-for-newbies-1f8038604e3b)


## ox-hugo {#ox-hugo}

C-c C-x p      Set property
SPC m o        Set property
C-c C-e H H    Export
C-c C-e H A    Export all
[
Exemplo all-posts](https://github.com/hlissner/doom-emacs/blob/develop/modules/config/default/+evil-bindings.el)


## Org Mode Code Snippets {#org-mode-code-snippets}

Para adicionar um Code Snippet digite &lt;s + TAB para autocompletar.

Para que o print() funcione em códigos python, adicionar o argumento no header ':results output'.


### Exemplo Closure Javascript {#exemplo-closure-javascript}

```js
const counter = () => {
    let n = 0;
    return {
        count: () => n++,
        reset: () => { n = 0; }
    };
}

const c = counter(), d = counter(); // Create two counters
console.log(c.count()) // => 0
console.log(d.count()) // => 0: they count independently
console.log(c.reset()) // reset() and count() methods share state
console.log(c.count()) // => 0: because we reset c
console.log(d.count()) // => 1: d was not reset
```


### Exemplo Python {#exemplo-python}

```python
def hamming(a, b):
    return len([i for i in filter(lambda x: x[0] != x[1], zip(a, b))])

a = "Teste string 1"
b = "Teste string 2"

result = hamming(a, b)
print(result)
```

```python
a = [1, 2, 3]
b = ['a', 'b', 'c']

print(list(zip(a, b)))
```
