# 2.1. Vim in Linux

Vim is a highly efficient text editor that operates in different modes, allowing for rapid text manipulation without using a mouse. It's particularly useful for editing configuration files, scripts, and code in bioinformatics.

You can install `vim` with the command `sudo apt install vim`

There are four basic modes that `vim` has:
1. Normal mode - for navigation and commands. You can press `Esc` to return to this mode
2. Insert mode - for typing text. You can press `i` to enter this mode
3. Visual mode - for selecting text. You can enter this mode with `v`
4. Command mode - for executing commands. You can enter this mode with `:`

Try the following:

**File setup**
1. Download the [precision_med.txt](https://github.com/xchee-01/7_Fundamentals-of-Linux/blob/main/Files/precision_med.txt). It should be downloaded to your Downloads folder on Linux.
2. Go into your Downloads directory on terminal using the command `cd Downloads`

> [!NOTE]
> You can use several commands to navigate between directories.
> `cd` - change directory
> `pwd` - to view path of present working directory

3. Now, we will move the file to the Desktop using the command `mv precision_med.txt ~/Desktop`. You should see the file appear on your Desktop.

4. Navigate your terminal back to Desktop by typing `cd ~/Desktop`
   
5. Type `more precision_med.txt` to view the text. To exit the view, press Ctrl+C 

**Starting with Vim**
4. Let's open the file by typing `vim precision_med.txt`

> [!NOTE]
> You can use variations of this command to open the file 
> vim +10 filename      # Open file at line 10, for example, vim +10 file precision_med.txt
> vim +/pattern file    # Open file at first pattern match, for example, vim +/AI file precision_med.txt

5. Here are some of the basic movements that you can:
   
```
h       # Left
j       # Down
k       # Up
l       # Right
w       # Next word start
b       # Previous word start
e       # Next word end
$       # End of line
0       # Start of line
^       # First non-blank character
gg      # Go to first line
G       # Go to last line
:n      # Go to line n, for example, :10 
Ctrl+f  # Page down
Ctrl+b  # Page up
```

6. Let's try and edit the file by adding the title of the document. You can do this by pressing `gg` (go to first line), followed by `i`, then enter to create new line, then type in the title of the document "The importance of precision health and medicine".

> [!NOTE]
> There are other basic editing commands that you can try out:
>
> ```
> i       # Insert before cursor
> a       # Append after cursor
> I       # Insert at line beginning
> A       # Append at line end
> o       # Open new line below
> O       # Open new line above
> r       # Replace single character
> R       # Replace mode
> ```

8. To save the document, you can press `Esc` to enter normal mode, and then type `:x!`. If you do not want to save the document, you can do `:q!`

9. Type `more precision_med.txt` to view

There are some other commands that you can play around:
**(a) Delete operations**

```
x       # Delete character under cursor
X       # Delete character before cursor
dd      # Delete line
dw      # Delete word
d$      # Delete to end of line
d0      # Delete to start of line
D       # Delete to end of line
```

**(b) Copy and paste**

```
yy      # Yank (copy) line
yw      # Yank word
y$      # Yank to end of line
p       # Paste after cursor (small case)
P       # Paste before cursor (upper case)
```


