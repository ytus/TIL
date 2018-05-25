# IDE

## WebStorm

### Where to install (not only) WebStorm in Ubuntu

Into `/opt`.

### Enter doesn't press the selected button in pop-up dialog

When you select a button in a pop-up dialog with arrow keys, pressing `Enter` will still press the ogiriginally hignlighted button with blue background. This is a feature, not a bug. To press the selected button, use `Space`. 

> Looks like this is a standard UI behaviour on Mac - Enter activates default button, while Space activates focused button.

(~ https://youtrack.jetbrains.com/issue/IDEA-125537#comment=27-1296095 )

### Troubleshooting
 
 * `File > Invalidate Caches / Restart...` 
 * `Help > Show Log in Files`. 

### Create / update shortcut in Ubuntu's Launcher

Start WebStorm and run this in the menu:

    Tools -> Add Desktop entry

The shortcuts definition is here: `~/.local/share/applications/jetbrains-webstorm.desktop`

## Vim

### copy & paste

    Cut and paste:
    
      Position the cursor where you want to begin cutting.
      Press v to select characters (or uppercase V to select whole lines, or Ctrl-v to select rectangular blocks).
      Move the cursor to the end of what you want to cut.
      Press d to cut (or y to copy).
      Move to where you would like to paste.
      Press P to paste before the cursor, or p to paste after. 
    
    Copy and paste is performed with the same steps except for step 4 where you would press y instead of d:
    
      d stands for delete in Vim, which in other editors is usually called cut
      y stands for yank in Vim, which in other editors is usually called copy 
      
(And the text is available through middle-click outside of Vim.)

(~ http://vim.wikia.com/wiki/Copy,_cut_and_paste )

### find & replace

> :%s/foo/bar/g

    Find each occurrence of 'foo' (in all lines), and replace it with 'bar'. 

> :s/foo/bar/g

    Find each occurrence of 'foo' (in the current line only), and replace it with 'bar'. 

> :%s/foo/bar/gc

    Change each 'foo' to 'bar', but ask for confirmation first. 

(~ http://vim.wikia.com/wiki/Search_and_replace )
