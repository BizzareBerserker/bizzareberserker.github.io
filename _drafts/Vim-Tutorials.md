---
layout: post
title: "Vim Tutorials"
tags: vim linux
category: essay
---

## Stage 1

Move cursor, Close, Save, Delete, Insert, Append

### Move cursor

<kbd>h</kbd> Move cursor left

<kbd>l</kbd> Move cursor right

<kbd>j</kbd> Move cursor down

<kbd>k</kbd> Move cursor up

### Close

`:q` Close file

`:q!` Close file don't save changes

### Save & Open & Read

`:w` Save change to the file

`:wq or :x or ZZ` Save changes and close file

`:w play.rb` Save current file as "play.rb"

`:e sun.rb` Open file "sun.rb"

`:r hat.rb` Read in file "hat.rb"

### Insert

<kbd>i</kbd> Insert at cursor

<kbd>I</kbd> Insert at beginning of line

### Append

<kbd>a</kbd> Append at cursor

<kbd>A</kbd> Append at end of line

<kbd>Esc</kbd>or <kbd>ctrl</kbd>+<kbd>[</kbd> Exit insert mode

## Stage 2

### Delete

<kbd>x</kbd> Delete character at cursor

`dw` Delete word

`d$` or `D` Delete to end of line

`d2w` Delete two words

`dd` Delete entire line

`2dd` Delete two lines

### Navigate in line

`w` Next word

`$` Go to end of text on current line

`^` Go to beginning of text on current line

`0` Go to beginning of current line

`2w` Go two words forward

`3e` Go to end of third word ahead

### Undo / Redo

`u` Undo last change

`U` Undo changes on entire line

<kbd>ctrl</kbd>+<kbd>r</kbd> Redo changes

## Stage 3

### Paste

<kbd>p</kbd> paste after cursor

<kbd>P</kbd> paste before cursor

### Replace

<kbd>R</kbd> Enter replace mode

<kbd>r</kbd> Replace character under cursor

`cw` change word

`c$` or `C` change to the end of the line 

`c2w` change 2 words

## Stage 4

### Navigate across lines

`50G` or `:50` Go to line 50

<kbd>G</kbd> Go to last line in file

`gg` Go to first line in file

### Search

`/waldo` Search for "waldo"

<kbd>n</kbd> Go to next search result

<kbd>N</kbd> Go to previous search result

`?carmen` Search backwards for "carmen"

<kbd>ctrl</kbd>+<kbd>o</kbd> Jump to previous location (jump back)

<kbd>ctrl</kbd>+<kbd>i</kbd> Jump to next location (jump forward)

<kbd>%</kbd> Go to matching parentheses or brackets

### Search & Replace

`:%s/bad/good` Replace bad with good in current line

`:%s/hi/bye/g` Replace hi with bye in entire file

`:%s/x/y/gc` Replace x with y in entire file, prompt for changes

## Stage 5

### Shell

`:!ls` Run shell command ls

### Visual

<kbd>v</kbd> Open visual mode

`vw` Visual select word

`vwd` or `vwx` Visual select word, then delete word

## Stage 6

### Open line

<kbd>o</kbd> Open new line below

<kbd>O</kbd> Open new line above

### Copy

`yw` Yank word

`vwy` Visual select word, then yank

`y$` Yank to end of current line

### Settings

`set ignorecase` or `set ic` Change search settings to ignore case

`set noignorecase` or `set noic` Change search settings to use case

## Stage 7

### Help

`:help w` Get help for "w" command

`:help e` Get help for "e" command
