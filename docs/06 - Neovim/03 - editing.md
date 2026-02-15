# Editing

## Deletion

`d<movement command>` Delete any characters between the current cursor location and wherever the cursor ends up from executing the movement command. 

## Changing

`c<movement command>` Delete any characters between the current cursor location and wherever the cursor ends up from executing the movement command and puts Vim in insert mode so changes can be made immediately. 

- `x` stands for dl (delete character under the cursor) 
- `X` stands for dh (delete character left of the cursor) 
- `D` stands for d$ (delete to end of the line) 
- `C` stands for c$ (change to end of the line) 
- `s` stands for cl (change one character) 
- `S` stands for cc (change a whole line)

> [!info] Count logic
>The commands "3dw" and "d3w" delete three words. If you want to get really picky about things, the first command, "3dw", deletes one word three times; the command "d3w" deletes three words once. This is a difference without a distinction. You can actually put in two counts, however. For example, "3d2w" deletes two words, repeated three times, for a total of six words.

`r<character>` changes the character being hovered with typed character. Never puts Vim in insert mode so quick for single character changes.

`.` Repeats last change command. Example workflow: Delete HTML with `df>`, move to start of next tag. Press `.` to repeat last change command (`df>`). 

## Visual mode

 `v` to enter visual mode. In visual mode, the movement commands will select all characters between the cursor where visual mode started and the executed command. Then a change command can be run to apply the change to the selection.
 This helps with editing since the count does not have to be mentioned. A selection is made first and the change is done on the selection. 
 `V` to enter line visual mode. Select the entire line instantly and more lines above or below can be selected through `j` and `k`.
 ctrl + `q` to enter block visual mode (since ctrl + `v` conflicts with Windows paste command). Use `h` and `l` to go left and right from the cursor and use `j` or `k` to select the same block in the lines above or below.
 `o` in visual mode jumps to the other end of the selection.

## Putting text

Text deleted with `d` or `x` is saved. To put the deleted text elsewhere, move the cursor there and press `p`. `P` will put the text before the cursor.

> [!info] Swapping characters
> Since `p` puts the value behind the cursor, pressing `x` to delete the current character and `p` after will swap the character with the one behind it.

## Yanking

Yanking is copying in VIM.
`y<movement command>` to yank all the text between start and end position of cursor. Use `p` to put yanked text anywhere.

## Text objects

Text objects are selectors based on semantics of text. 
`<Movement command>aw` move A Word.
`<>is` move Inline Sentence (cursor till a . in text)
`<>as`move A Sentence (cursor till a . + whitespace in text)

## Replace mode

`R` to enter replace mode. Each typed character will replace the one currently on the cursor instead of placing it after it.
