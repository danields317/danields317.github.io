# Advanced Movement

## Word movement

`w` Jump to start of next word.
`b` Jump to start of previous word.
`e` Jump to next end of word.
`ge` Jump to previous end of word.

## Horizontal line movement

`$` or End key Jump to end of line
`0`or Home key Jump to start of a line
`^` Jump to first non-blank character of a line

## Character movement

`f<character>` Move to specified character right of cursor.
`F<character>` Move to specified character left of cursor.
`%` When cursor on a opening bracket, move to the closing one or vice versa.
When it is not on a bracket, move to the first one right of the cursor.

## Vertical line movement

`G`Go to end of file
`gg` go to top of file
`<count>G` go to line defined by `<count>`
`<count>%` go to a percentage through the file. E.g. 50% go to line halfway through the file.
`H` Go to first line visible on screen
`M` Go to middle line visible on screen
`L` Go to last line visible on screen

## Finding line number

`:set number/nonumber` toggle numbers in front of lines
`:set ruler/noruler` toggle line info in bottom right
CTRL + `g` get current quick file info

## Scrolling

ctrl + `e` scroll down
ctrl + `y` scroll up
ctrl + `u` jump down half screen
ctrl + `d` jump up half screen

`zz` move line with cursor to middle of screen
`zt` move line with cursor to top of screen
`zb` move line with cursor to bottom of screen

## Searching

`/<word>` to find occurrences of letters.
After typing the search, press enter to 'save' it.
Press `n` to jump to the next occurrence of the search.
`?<word>` does the same as `/` but when pressing `n` it will go to the previous one. 
Searching allows for Regex expressions for complex matching.

`:set ignorecase/noignorecase` to toggle case ignore for searches

## Marks

Usually, when you move the cursor more than one line through a command, this is called a jump. A mark is being saved from the previous spots that have been jumped from.
ctrl + `o` jump to previous mark
ctrl + `i` jump to next mark

## Named marks

`m<a-z>` Place mark on cursor named with the pressed letter (26 marks max)
`'<a-z>` Jump to placed mark
