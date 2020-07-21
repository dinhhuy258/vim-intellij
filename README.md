# Vintellij
Make Intellij as a server language protocol.

## Installation

### Vim

#### Dependencies
- [fzf](https://github.com/junegunn/fzf.vim)

#### Install

```
Plug 'dinhhuy258/vintellij'
```
The default mapping is
- <leader>gcd to go to the definition from the symbol under cursor
- <leader>co to open the current file from vim by intelliJ
- <leader>ci to suggest possible imports by the symbol under cursor

if you want to make your own custom keymap, then put the following in your `.vimrc`

```
let g:vintellij_use_default_keymap = 0
nnoremap <Leader>gcd :VintellijGoToDefinition<CR>
nnoremap <Leader>co :VintellijOpenFile<CR>
nnoremap <Leader>ci :VintellijSuggestImports<CR>
```

### Intellij plugin

1. Import the project into Intellij
2. Run `gradle buildPlugin`
3. Install your plugin into Intellij. (Preferences -> Plugins -> Install Plugin from Disk...)

## Vim functions

- `vintellij#SuggestImports()`: suggest a list of importable classes for an element at the current cursor

- `vintellij#GoToDefinition()`: go to the position where an element at the current cursor is defined

- `vintellij#OpenFile()`: open the current file in Intellij

- `vintellij#RefreshFile()`: tell IntelliJ to refresh the VirtualFile element otherwise the `suggest imports` and `go to definition` features will not work correctly. This method will be called automatically each time the java/kotlin buffer is saved to file. If you want to disable it, set variable `g:vintellij_refresh_on_save` to 0 (It may cause the problem on the `suggest imports` and `go to definition` features)

  To disable auto refresh file, use the command
  ```
    VintellijEnableAutoRefreshFile!
    ```
  To enable again
  ```
      VintellijEnableAutoRefreshFile
      ```
- `vintellij#HealthCheck()`: check if the plugin server is working or not. This method will be called automatically each time the java/kotlin buffer is loaded. If you want to disable it, set variable `g:vintellij_health_check_on_load` to 0.

  To disable auto health check, use the command
    ```
    VintellijEnableHealthCheckOnLoad!
        ```
  To enable again
    ```
    VintellijEnableHealthCheckOnLoad
        ```
## Features

| Name | Kotlin | Java |
| ---- | ------ | ---- |
| Go to definition | :white_check_mark: | :white_check_mark: |
| Suggest imports | :white_check_mark: |  |
| Find references |   |  |
| Auto complete |   |   |

## Issues

- To make it work, the Intellij must open the same project as Vim.
- Saving file before using `suggest imports`, `go to definition`... features otherwise the features will not work correctly.
- Always open Intellij otherwise everything will be slow - the workarround maybe:
  - Get IntelliJ focused by having it in your secondary screen
  - Get vim transparent and putting IntelliJ behind
