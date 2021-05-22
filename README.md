# About this repo

 This is my fork of the
 [skywind3000/quickmenu.vim](https://github.com/skywind3000/quickmenu.vim).  
 I use this just for fun and experiments.

## Preface

There are many keymaps defined in my `.vimrc`. Getting tired to check my
`.vimrc` again and again when I forget some, so I made this `quickmenu` plugin
which can be fully customized:

- Well formatted and carefully colored to ensure neat and handy.
- Press `<F12>` to popup `quickmenu` on the right, use `j` and `k` to move up
  and down.
- Press `<Enter>` or `1` to `9` to select an item.
- `Help` details will display in the cmdline when you are moving the cursor
  around.
- Items can be filtered by `filetype`, different items for different filetypes.
- Scripts in the `%{...}` form from `text` and `help` will be evaluated and
  expanded.
- No longer have to be afraid for forgetting keymaps.

## Install

Copy `autoload/quickmenu.vim` and `syntax/quickmenu.vim` to your
`~/.vim/autoload` and `~/.vim/syntax`.  or use
[vim-plug](https://github.com/junegunn/vim-plug) to install it just add this
line to your plugins section: `Plug 'vladimir-popov/quickmenu.vim'`. 

## Configuration

Add these lines to your `.vimrc` (outside of the plugins section in case of
`vim-plug`):

```VimL 
" choose a favorite key to show/hide quickmenu 
noremap <silent><F12>
                \ :call quickmenu#toggle(0)<cr>

" enable cursorline (L) and cmdline help (H) 
let g:quickmenu_options = "HL" 
```

## Tutorial

### Add new section

To add a new section to your menu simply use the function below:

```VimL 
function quickmenu#append('#' . '<Section name>') 
```

The argument of the function here is a name of the section. It must
begin from the '#' character, but that character will not be drawen.

### Add new item

To add a new item you should use the same function as for adding a new 
section, but with more arguments and without restiction about '#':

```VimL 
function quickmenu#append(text, action[, help]) 
```

- `text` will be show in the quickmenu, vimscript in `%{...}` will be evaluated
  and expanded.
- `action` is a piece of vimscript to be executed when a item is selected.
- `help` will display in the cmdline if g:quickmenu_options contains `H`.

A item will be treated as "static text" (unselectable) If `action` is empty.

### Add bookmark 

You can add a bookmark to the menu. To do so, use the function:

```VimL 
function quickmenu#bookmark(path) 
```

- `path` if this is a path to a file, then it file will be opened;
         if this is a path to the directory, then this path will be set as the
         working directory. Optionally, the `NERDTree` window can be opened if
         a corresponding plugin has been installed.
