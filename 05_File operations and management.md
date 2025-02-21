# 5. File operations and management

File operations and permissions are critical in medical informatics where data security and integrity are paramount. 

## 5.1. Basic file operations 

We can create files using the code below:

```
touch file.txt               # Create empty file
echo "content" > file.txt    # Create with content 
vim file.txt     
```

> [!NOTE]
> On the line for `echo "content" > file.txt`, you can use >> if you want to append text to the file.

## 5.2. Copying files 

We can copy files using the syntax below:

```
cp [From where] [To where]
```

So in this case, we can use the following commands

```
cp file.txt ../        # Copy this file to one directory above this level
```

> [!NOTE]
> If you want to copy directories, you would need to use the flag `-r`
>
> For example,
>
> ```
> cp -r <dir1> <dir2>
> ```

## 5.3. Move and renaming files 

We can move and rename files using the syntax below:

```
mv [From where] [To where]
```

So for example:

```
mv old.txt new.txt              # Rename file
mv file.txt /new/location/      # Move file
```

Linux does not have a specific command to renaming, so you only use the `mv` command

## 5.4. Removing files 

We can remove files using the commands below:

```
rm file.txt                    # Remove file
rm -r directory/               # Remove directory
```

## 5.5. Checking file permissions

You can check the ownership of the files by using either one of these commands:

```
ls -l file.txt
stat file.txt
```

The file permission structure has three parts: owner (u), group (g) and other (o). 

```
-rwxrwxrwx
| |  |  |
| |  |  └── others' permissions (o)
| |  └───── group permissions (g)
| └──────── owner permissions (u)
└─────────── file type (- for file, d for directory)
```

**The symbolic permissions usedin these operators are:**
- `+` add permission
- `-` remove permission
- `=` set exact permission

**And these permission types are:**
- `r` read
- `w` write
- `x` execute

So for example, 

```
# Add execute for user
chmod u+x file.txt

# Remove write for others
chmod o-w file.txt

# Give read and write to user and group
chmod ug+rw file.txt

# Remove all permissions for others
chmod o-rwx file.txt

# Set specific permissions for user
chmod u=rx file.txt

# Add execute for all (user, group, others)
chmod a+x file.txt
```

You may even combine multiple changes together:

```
# Add read for user, remove write for group
chmod u+r,g-w file.txt

# Give read/write to user, read-only to group and others
chmod u+rw,go=r file.txt
```

## 5.6. Checking file information

You can check for file information using the info below:

```
file file.txt
stat file.txt
du -sh file.txt
```
