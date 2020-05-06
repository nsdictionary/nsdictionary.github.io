vim
===

- example
```
:autocmd FileType javascript nnoremap <buffer> <localleader>c I//<esc>
:autocmd FileType python     nnoremap <buffer> <localleader>c I#<esc>
```

- pandoc
```
nnoremap <leader>r :!pandoc % --to=html5 > %.html
```
