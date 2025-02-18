# 6. Shell scripting foundation

Shell scripting is essential for automating bioinformatics workflows and medical data processing tasks. Understanding these foundations enables creation of reliable, reusable pipelines for handling patient data and genomic analyses.

## 6.1. Shell script basics

The basic structure of a shell script looks like this:

```
#!/bin/bash                  
# Script description
# Author: Name
# Date: YYYY-MM-DD

# Variables
# Functions
# Main script
```

The first line is known as the "shebang line". It's always placed at the very first line of a script and tells the system which interpreter should be used to execute the script.

The `/bin/bash` line in the shebang line refers to the full path to the Bash interpreter.

Besides, having a shebang line allows you to run the script directly with `./script.sh` (after making it executable with `chmod +x`). Or else, you would need to explicity type `bash script.sh` or `sh script.sh`

## 6.2. Running the scripts

To run the script, you can use:

```
chmod +x script.sh         # Make executable
./script.sh                # Run script
```

or you can explicitly type:

```
bash script.sh
```

## 6.3. Variables and data types

We can declare variables in bash scripts. For example:

```
# Basic variable assignment
name="value"             # String assignment
number=42                # Number assignment
array=(item1 item2)      # Array assignment

# Variable usage
echo $name               # Print variable
echo ${name}             # Print with disambiguation
echo "${name}"           # Print preserving spaces
```

Try and run the bash script for the following example:

```
#!/bin/bash
patient_id="P001"
vital_signs=(98.6 72 120/80)
last_visit="2025-02-16"

echo "Patient ID: $patient_id"
echo "Temperature: ${vital_signs[0]}"
echo "Last Visit: $last_visit"
```

## 6.4. Input and output operations

Bash scripts can also take inputs and output as well. 

```
# Output
echo "Message"            # Print to stdout

# Input
read -p "Enter value: " variable
read -s password         # Silent input
```

Try and run the following script a few times on terminal. 

```
#!/bin/bash
read "Please enter your DNA sequence: " dna_sequence
echo "You entered the DNA sequence: $dna_sequence"

echo $dna_sequence >> user_dna.txt    # You can try > and see the effect
echo "Your DNA sequence has been saved to user_dna.txt"
```


