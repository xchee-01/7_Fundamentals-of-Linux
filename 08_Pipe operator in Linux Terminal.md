# 8. Pipe operator in Linux Terminal 

The pipe operator | is one of the most powerful features in Linux/Unix systems. It takes the output (stdout) of one command and feeds it as input (stdin) to another command.

The basic syntax is as follows:

```
command 1 | command 2
```

For example

```
ls | grep ".txt"    # Lists only files containing ".txt"
```

or 

```
echo "5 + 3" | bc
```

or 

```
echo "10 20 30" | awk '{print $1 + $2 + $3}'
```
