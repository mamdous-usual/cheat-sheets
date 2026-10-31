# Basics

- `esc` - for normal mode
- `i` - for insert mode
- `:w` - write the file (save)
- `:q` - quit the file 
- `:wq` or `:x` - write and quit
- `:q!` - quit without writing
- `h,j,k,l` - Basic navigation
  - `h` - right
  - `j` - down
  - `k` - up
  - `l` - down
- `a` - append next
- `I` - insert before line
- `A` - append after line
- `o` - new line below
- `O` - new line above

# Intermediate

- `w` - next word
- `b` - previous word
- `W` - next word (ignore special characters)
- `B` - next word (ignore special characters)
- `r` - replace letter (replace a character without going insert mode)
- `R` - replace a word (replace a word without going insert mode)
- `cw` - change word
- `8w` - jump eight words
- `c7w` - change seven words
- `4j` - move four lines down
- `C` - change rest of the line
- `dw` - delete word
- `D` - Delete rest of the line
- `d4w` - delete four lines
- `dd` - delete line (deletes the whole line where ever the cursor is)
- `cc` - change line (changes the whole line where ever the cursor is)
- `4dd` - change four lines
- `8cc` - change 8 lines
- `x` - delete a character (without going insert mode)

# Do Stuffs

- `u` - for undo
- `ctrl + r` - redo 
- `ctrl + u` - undo in insert mode 
- `ciw` - change in inner word
- `diw` - delete in inner word (in the middle of the word delete without going to the first character)
- `J` - deletes an empty line (without going insert mode)
- `P` - inserts an empty line (without going insert mode)
- `ci)` / `]` / `}` - change inner parenthesis/brackets
- `%` - jump to the parenthesis/brackets
- `^` - Jump to the first of the line
- `gg` - jump to the beginning of the line
- `G` - jump to the end of the line
- `17G` - go to line 17
- `:17` - go to line 17 
- `0` - navigate to the beginning of the line
- `$` - navigate to the end of the line

# Visual Mode

- `v` - enter visual mode
- `d` - delete
- `c` - change
- `y` - yanking (copying)
- `Y` - yank immediately without going visual mode
- `p` - paste after 
- `P` - paste before
- `yy` - yank line
- `5yy` - yank 5 lines
- `9p` - paste nine times
- `y5w` - yank 5 words
- `yi)` - yank in inner brackets
- `yiw` - yank in inner words

# More About Visual Mode

- `V` - visual line
- `ctrl + v` - Visual block
- `dot(.)` - repeat last operation
- `zz` - center selection
- `>` - shift right 
- `<` - shift left
- `=` - indent
- `>>` & `<<` - indent
- `==` - indent line
- `gg=G` - indent whole file
- `ggdG` - delete the whole file

## Buffers and Windows

### Buffers

- `:ls` or `:buffers` — List buffers
- `:e <file>` - open file in new buffer
- `:bnext` / `:bn` — Next buffer  
- `:bprevious` / `:bp` — Previous buffer  
- `:b <num>` — Go to buffer by number  
- `:bd` — Delete (close) buffer  

### Windows (Splits)

- `:split` / `:sp` — Horizontal split  
- `:vsplit` / `:vsp` — Vertical split  
- `Ctrl + w h/j/k/l` — Move between splits  
- `Ctrl + w q` — Close current split  
- `Ctrl + w =` — Equalize split sizes  
- `:resize +5` — Increase height  
- `:vertical resize +10` — Increase width  

# Commands
- `/word` - search for word
- `n` - next occurrence
- `N` - previous occurrence
- `+` - next token occurrence
- `#` - previous token occurrence
- `:s/old/new` - replace
- `:%s/old/new/g` - replace everywhere
- `:set number/nu` - line numbers
- `:set relativenumbers/rnu` - relative numbers
- `:colorscheme <theme>` - select theme
- `:set tabstop=4` - tab width to 4
- `:set autoindent` - auto indentation
- `:set mouse=a` - activate mouse
- `:set mouse=""` - deactivate mouse
