# 3. Reviewing of vim, process management and job control

Now, let's review back the previous two chapters. 

Try the following:

1. Using vim, create a file called `simulate_analysis.sh` and save on your Desktop

```
#!/bin/bash

echo "Starting analysis..."

while true; do
    echo "Analyzing data..."
    sleep 10
done
```

3. After creating the file, type `chmod +x simulate_analysis.sh`. 

> [!NOTE]
> `chmod` stands for "change mode" - it's the command used to change permissions on Unix-like systems
> 
> `+x` means "add executable permission"
> 
> After running this command, the file can be executed directly using ./simulate_analysis.sh instead of having to run it through an interpreter like `bash simulate_analysis.sh`.
>
> An equivalent code to this would be just typing `bash simulate_analysis.sh &`

3. Run multiple instances of this script. The `&` at the end means it will run in the background. 

```
./simulate_analysis.sh &    
```

4. Type `jobs -l` to show PID. 

> [!TIP]
> Alternatively, you can use `ps aux | grep simulate`. This is more general and is able to find processes system-wide.
> 
> - `ps` shows the process status
> - `a` shows processes for all users
> - `u` shows detailed user-oriented format
> - `x` shows processes not attached to a terminal
> - `|` sends the output to `grep simulate`
> - `grep` shows lines containing the keywords "simulate"
>
> We will learn more about this in the later chapters.

5. Kill the `simulate_analysis.sh` process by typing `kill <PID>` e.g. `kill 8905`
