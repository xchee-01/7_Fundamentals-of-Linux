# 7. Aliases, paths and environments

# 7.1. What are aliases? 

Aliases are custom shortcuts for commands in the shell. The syntax is as follow:

```
alias shortcut = 'your command'
```

Aliases created in terminal last only for that session. To make permanent, you need to add them to ~/.bashrc or ~/.bash_aliases.
The `.bashrc` is a shell script that Bash runs whenever it is started interactively. It initializes your shell configuration for each new terminal session.

**Purpose of the `.bashrc` script**
- It configures your shell environment
- Set up aliases
- Defines environment variables
- Customizes your prompt
- Sets `PATH` additions

Let's try it out how to set up aliases:

1. Type `alias` to see all the aliases available.

2. Create a bash script using VIM. Save the file as "dna_input.sh".

```
#!/bin/bash
echo "Please enter your DNA sequence:"
read dna_sequence                            # If user types "ATCG", then:
# Echo back the sequence
echo -e "\nYour DNA sequence is:"
echo "$dna_sequence"                         # This will print: ATCG
```

3. Make this an executable chmod +x dna_input.sh
  
4. Run it with: /dna_input.sh

5. Let's set a shortcut to run the program using alias

```
alias dna='/dna_input.sh'   # no spacing between dna and = sign
```

6. Type `alias` to see all the aliases available. You should see a new alias created.

7. Type `dna`. You should see your script being run.

> [!TIP]
> Once you close the terminal, the aliases that you set for the Terminal session would be lost. To make aliases more permanent, you would need to use the following command:
>
> ```
> echo "alias dna='/dna_input.sh'" >> ~/.bashrc
> source ~/.bashrc                                    #This applies the changes. 
> ```


# 7.2. What are PATHs? 

`PATH` tell shell where to find the executables (files to be run). 
You can check the PATHs that your shell has using the command:

```
echo $PATH
```

These paths are directories that are separated by colons. 
The order matters. The first match is used. 

Let's try to add a new path to run the script in Section 7.1. 

1. First, type `pwd` an note down the current path to your current working directory. Let's call this the "Files directory"

2. Next, type `cd ~`. This will do to the root directory. You can check this by typing `pwd`.

3. Try and run the script from Section 7.1 using `dna_input.sh`.
   This will likely throw you and error "No such file or directory"
   This is because the "dna_input.sh" file is not found in the root directory, it is found in your "Files directory"
   Additionally, the "Files directory" is not a place the terminal looks into because it's not in `PATH`. 


5. Now, let's try and add a new path so that the terminal will look for "dna_input.sh" in your "Files directory"

```
# Adding to PATH temporarily
export PATH=$PATH:/new/path                        # For example, PATH=$PATH:/home/xavierchee/Desktop/Files

# Adding to PATH permanently
echo 'export PATH=$PATH:/new/path' >> ~/.bashrc
source ./bashrc
```

6. Now, type `echo $PATH`. You should see a new path being added.

7. Run `dna_input.sh` and the script should launch. This is because now the Terminal will be able to look fo this file in your "Files directory".

# 7.3. What are environment variables? 

Environment variables are like containers that store information your system and programs can use. Think of them as labeled boxes holding specific information that any program can check.

You can try the example below:

```
# Setting an environment variable
export MY_NAME="John"

# Using the variable
echo $MY_NAME
# Output: John
```

Here are some of the common variable that have been preset:

```
# Home directory
echo $HOME
# Output: /home/username

# Current user
echo $USER
# Output: username

# Current shell
echo $SHELL
# Output: /bin/bash
```

These environment variables are **accessible by all prograins in the session**
They are usually written in UPPERCASE.
They are created using the `export` command and are accessed using $ before the name. 

You can check all the available env variables using `env`. 

Let's try and example:

1. On your terminal, type `env` to see all the available environment variables.

2. Next, type the following to set up a DNA sequence variable
```
export DNA_SEQUENCE="ATCG"
```

3. Now create the following script and run it. Remember to `chmod +x` it to run.
```
#!/bin/bash

# Print the environment variable if it exists
echo "DNA sequence from environment variable is:"
echo "$DNA_SEQUENCE"

echo -e "\nYour environment variable DNA sequence is:"
echo "$DNA_SEQUENCE"
```

Notice how your programme took a external environment variable. 
