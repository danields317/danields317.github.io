# Basics

This file explains the bascis of moving around in Neovim.

## Start Neovim

`nvim <filename>`
`~` means non existing line. Printed at end of file.

## Modes

Normal mode -> Used for commands
Insert mode -> Used to write text to file
Command line mode -> Used for Non-editing commands (e.g. save file, make backup)

Go into insert mode by pressing `i`
Exit any mode and return to normal mode with escape key.

## Movement

Available in normal mode.
`h` Left
`j` Down
`k` up
`l` right

## Deletion

Available in normal mode
`x` Delete on cursor
`dd` Delete line
`J` Delete line break (appends next line to current line)

## Undo/Redo

Available in normal mode
`u` Undoes last change
`ctrl + r` Redoes undone change

## Appending

`a` Start insertion after hovered field (`i` places the cursor in front)
`o` Start new line and begin inserting

## Using counts

A lot of commands allow a number in front of it. This number means the amount of times the command will be executed.
`5x` will delete five characters
`3k` will jump up three lines

## Getting out

`ZZ` Exit and save changes.
`:q!` Leave without saving