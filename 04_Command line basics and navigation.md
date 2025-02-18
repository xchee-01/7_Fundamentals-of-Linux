# 4. Command line basic and navigation

The command line interface (CLI) is essential for bioinformatics workflows, offering precise control and automation capabilities that are crucial for handling medical data and genomic analyses. Understanding navigation and basic commands forms the foundation for efficient data processing.

## 4.1. Basic command structure 

Here is the basic syntax of how a command is used in the Terminal. 

```
command [options] [arguments]
```

## 4.2. Directory navigation 

To navigate between directories, you can use the following command

```
cd /path/to/directory    # Absolute path
cd ./relative/path       # Relative path
cd ..                    # Move up one directory
cd ~                     # Home directory
cd -                     # Previous directory
```

You can try out the command with the directory:

```
cd /home/<username>/Desktop/Files/RXR   # Absolute path
ls
cd RXR                                  # Relative path
ls
cd ..                                   # Move up one directory
ls
cd ~                                    # Home directory
ls
cd -                                    # Previous directory
ls
```

> [!NOTE]
> You can aso try a variations of these for `ls`
>
> ```
> ls              # List contents
> ls -l           # Long format
> ls -a           # Show hidden files
> ls -h           # Human-readable sizes
> ls -R           # Recursive listing
> ```
>
> You may even combine them:
>
> ```
> ls -lh          # Long format with human-readable sizes
> ls -lah         # Include hidden files
> ls -ltr         # Sort by time, reverse order
> ```

## 4.3. Essential Navigation Commands

You can find the files using commands below:

```
# Find files
locate <filename>             # Quick search using database
find . -name "<filename>"     # Detailed search from current directory

# View file contents
cat <filename>.txt             # Display entire file
less <filename>.txt            # Page through file
head -n 10 <filename>.txt      # First 10 lines
tail -n 10 <filename>.txt      # Last 10 lines
```

For example, 

```
# Find files
locate RXR_gene.txt             # Quick search using database
find . -name "RXR_gene.txt"     # Detailed search from current directory

# View file contents
cat RXR_gene.txt             # Display entire file
less RXR_gene.txt            # Page through file (press q to exit)
more RXR_gene.txt            # Show portion of the file (press Ctrl+C to exit)
head -n 10 RXR_gene.txt      # First 10 lines
tail -n 10 RXR_gene.txt      # Last 10 lines
```
