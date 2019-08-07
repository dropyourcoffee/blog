---
layout: post
title:  "NerdTree basics"
date:   2019-07-11 11:43:53 +0900
tags: vim
categories: Linux
---

  NERDTree is a sort of file system explorer for the Vim editor that makes users easier
   - Visually browse complex directory hierarchies
   - Quickly open files for reading or editing
   - Perform basic file system operations
  
  
  Basic keymaps for NERDTree explorer
  
  | Key |  Function                                                   |
  |-----|-------------------------------------------------------------|
  | t   |  Open file in new tab                                       |
  | i   |  Open file in new horizontal split view                     |
  | s   |  Open file in new vertical split view                       |
  | C   |  Cursored directory will be the new root in the explorer.   |
  | U   |  Parent of the current root directory will be the new root. |
  
  
  
  Custom Optimisation
  
  ```bash
  nmap <C-n> :NERDTreeToggle<CR>
  nmap <C-h> <C-w><C-w>
  nmap <C-j> <C-w><C-j>
  nmap <C-k> <C-w><C-k>
  nmap <C-l> <C-w><C-l>
```
  
  - allows me to turn on/off nerd tree in vim with [Ctrl-N]
  - allows me to navigate between tabs in vim with [Ctrl-J, Ctrl-K, Ctrl-H, Ctrl-L]
  
