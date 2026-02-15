
# Keymap

Neovim and its plugins have a bunch of keybinds that make your life easier. There are more keybinds than you will ever use and finding the ones you enjoy using in all the lists in multiple different help files is a chore. I summarized the keybinds that I personally think are important to know and use. This file contains Neovim native keybinds and default keybinds for some of the more popular plugins that I use myself.

\## Movement

| Keybind              | Usage                                                                  |
| -------------------- | ---------------------------------------------------------------------- |
| `h`, `j`, `k`, `l`   | Move left, down, up, right                                             |
| `w`, `W`             | Jump to next word/next space separated word                            |
| `b`, `B`             | Jump to previous word/previous space separated word                    |
| `e`, `E`             | Jump to end of next word/end of next space separated word              |
| `0`, `$`, `^`        | Move to start/end of line, first none blank character on line          |
| `f[char]`, `F[char]` | Go to first next/previous instance of given char.                      |
| `t[char]`, `T[char]` | Go to one character before first next/previous instance of given char. |
| `,`, `;`             | Repeat last `f`, `F`, `t` or `T` to next/previous instance.            |
| `%`                  | Jump between connected brackets                                        |

## Operators

| Keybind                       | Usage                                          |
| ----------------------------- | ---------------------------------------------- |
| `x`, `X`                      | Delete character on cursor/one before cursor.  |
| `d[move]`, `D[move]`          | Delete characters based on movement command.   |
| `y[move]`                     | Copy (yank) characters based on movement.      |
| `p`                           | Paste copied lines.                            |
| `/<search>` -> `enter` -> `n` | Search for query and cycle through occurrences |
| `=[move]`                     | Indent lines moved on.                         |

## Find and Replace

| Keybind                     | Usage                                                                    |
| --------------------------- | ------------------------------------------------------------------------ |
| `:s/<pattern>/<replace>/g`  | Find pattern and replace with value for each occurrence on current line. |
| `:%s/<pattern/<replace>/g ` | Same as above but for entire file                                        |

`g` stands for Global so the action is done more than once.

## Windows

`<C-w>` to start each window command.

| Keybind            | Usage                                              |
| ------------------ | -------------------------------------------------- |
| `s`                | New window horizontal                              |
| `v`                | New window vertical                                |
| `h`, `j`, `k`, `l` | Move to window left, down, up or right of current  |
| `H`, `J`, `K`, `L` | Move the window left, down, up or right of current |
| `=`                | Resize all to same size                            |

## Buffers

## Nvim Tree

| Keybind  | Usage                                            |
| -------- | ------------------------------------------------ |
| `<CR>`   | Open folder/file                                 |
| `<BS>`   | Close folder                                     |
| `<C-]>`  | Set selected folder as root                      |
| `<C-t>`  | Open selected file in new tab                    |
| `<C-v>`  | Open selected file vertical                      |
| `<C-x>`  | Open selected file horizontal                    |
| `a`      | New file or folder. For folder end name with `\` |
| `r`      | Rename                                           |
| `D`      | Trash file                                       |
| `c`, `p` | Copy and Paste files                             |
