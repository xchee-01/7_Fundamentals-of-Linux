# 7. Text processing using Linux

For the following exercise, you would need to download the the file medical_record.txt.

## 7.1. Basic text processing using `grep`

grep (Global Regular Expression Print) is a powerful command-line utility for searching text patterns in files. In medical text processing, grep is invaluable for quickly finding and filtering patient information, diagnoses, and medical conditions.

The basic syntax would be:

```
grep [options] pattern [file...]
```

There are some common options that you can use:

- -i: Case-insensitive search
- -c: Count matching lines
- -n: Show line numbers
- -v: Invert match (show non-matching lines)
- -l: List only filenames with matches
- -r: Recursive search through directories
- -A n: Show n lines after match
- -B n: Show n lines before match
- -C n: Show n lines before and after match
- -E: Extended regular expressions
- -w: Match whole words only

You can try the following commands and try different variations of the flag: 

```
grep "Diabetes" medical_records.txt                # It will return every line containing the word "Diabetes"
grep -c "Gender: F" medical_records.txt            # Count number of female patients
                                                   # The -c flag in grep counts the number of lines that match the pattern
grep -A 2 "Temperature: 99" medical_records.txt    # The -A flag in grep shows the matching line plus the specified number of lines after it.
```

There are times where you also combine different commands together, for example, with `echo` and `grep`.

```
echo "Male patients: $(grep -c "Gender: M" medical_records.txt)"
echo "Female patients: $(grep -c "Gender: F" medical_records.txt)"
```

You may also consider trying to look for patients where you may not know the exact temperatures:

```
# Find patients with elevated temperature                  # "Temperature: 9[89]" matches either "Temperature: 98" or "Temperature: 99"
grep -A 2 "Temperature: 9[89]" medical_records.txt

# Find all temperature readings
grep "Temperature:" medical_records.txt

# Find temperatures above 99°F with context              
grep -B 2 -A 3 "Temperature: 9[9-9].[0-9]F" medical_records.txt            # 9[9-9].[0-9]F matches temperatures like "99.0F", "99.1F", "99.2F", etc.
```

## 7.1.1. Advanced text processing using `grep` and regular expression (regex)

Let me break down these grep commands and explain regular expressions:
Regular Expressions (regex) are patterns used to match character combinations in text. They're like a search language with special characters that have specific meanings.

For example,

```
# Find all numeric values
grep -o "[0-9]\+" medical_records.txt

# Extract dates
grep -o "[0-9]\{4\}-[0-9]\{2\}-[0-9]\{2\}" medical_records.txt

# Find dosages
grep -o "[0-9]\+mg" medical_records.txt
```

> [!NOTE]
> Here are the explanations for the code above
> 
> `grep -o "[0-9]\+" medical_records.txt`
> 
> - -o shows only the matched part
> - [0-9] matches any single digit from 0 to 9
> - \+ means "one or more" of the previous pattern
> - This will find all numbers like: 123, 45, 6789, etc.
> 
> `grep -o "[0-9]\{4\}-[0-9]\{2\}-[0-9]\{2\}" medical_records.txt`
> 
> - [0-9]\{4\} matches exactly 4 digits
> - - matches a literal hyphen
> - [0-9]\{2\} matches exactly 2 digits
> - This finds dates in format YYYY-MM-DD like: 2024-02-19
> 
> `grep -o "[0-9]\+mg" medical_records.txt`
> - [0-9]\+ matches one or more digits
> - mg matches literal "mg"
> - This finds dosages like: 500mg, 50mg, 1000mg

"Extended Regular Expressions" which provides a more modern and readable way to write regex patterns. The main difference is that you don't need to escape special characters with backslashes. You can use this for `-E` flag. 

Without a `-E` flag, you may need `grep "[0-9]\{3\}-[0-9]\{3\}-[0-9]\{4\}" file.txt`
`
But with a `-E`flag, you can do `Without a `-E` flag, you may need `grep "[0-9]\{3\}-[0-9]\{3\}-[0-9]\{4\}" file.txt``, which makes it clearer to read. 

Here's another alternate example, 

Without a `-E` flag, you may need `grep "a\+b" file.txt`
But with a `-E`flag, you can do `grep -E "a+b" file.txt`

For example: 

```
# Find patients with multiple conditions
grep -E "Diagnosis:.*,.*" medical_records.txt

# Find patients with specific age ranges
grep -E "Age: [2-3][0-9]" medical_records.txt  # 20-39 years
grep -E "Age: [4-5][0-9]" medical_records.txt  # 40-59 years
grep -E "Age: [6-9][0-9]" medical_records.txt  # 60+ years
```

## 7.2. Basic text processing using `sed`

The Stream Editor (sed) is a powerful text processing tool that performs operations on text streams line by line. In medical text processing, sed is invaluable for standardizing formats, updating records, and transforming medical data. Unlike `grep` which just searches and displays text, `se`d can modify text content.

The basic syntax of `sed` is as follows:

```
sed [options] 'command' file
sed [options] -f script-file file
```

There are some common options that you can use:

- -i: Edit files in place
- -i.bak: Edit files in place, create backup with .bak extension
- -e: Multiple commands (scripts)
- -n: Suppress automatic printing of pattern space
- -r or -E: Use extended regular expressions
- -f: Read commands from a file
- -g: global

**(a) For replacements of words**

The syntax is as below:

```
sed 's/pattern/replacement/flags'
```

So for example, 

```
# Replace first occurrence of 'mg' with 'MG' on each line
sed 's/mg/MG/' medical_records.txt

# Replace all occurrences of 'mg' with 'MG' (global flag)
sed 's/mg/MG/g' medical_records.txt

# Replace first occurrence of 'mg' with 'MG' on each line
sed 's/mg/MG/' medical_records.txt

# Replace all occurrences of 'mg' with 'MG' (global flag)
sed 's/mg/MG/g' medical_records.txt
```

**(b) Line operations**

You can also print, delete or add text using `sed`.

```
# Print specific lines (e.g., lines 1-5)
sed -n '1,5p' medical_records.txt

# Delete specific lines
sed '1d' medical_records.txt  # Delete first line
sed '1,5d' medical_records.txt  # Delete lines 1-5

# Add text before/after specific patterns
sed '/Patient ID/i\NEW RECORD' medical_records.txt  # Insert before
sed '/Patient ID/a\END RECORD' medical_records.txt  # Append after
```

## 7.3. Basic text processing using `awk`

**(a) Field processing**
You can use `awk` to print specific fields. 

```
# Print specific fields
awk '{print $1, $2}' medical_records.txt

# Change field separator
awk -F: '{print $1, $2}' medical_records.txt   # -F: sets the field separator to a colon (:)
```

**(b) Pattern matching**

```
# Simple pattern matching
awk '/Diabetes/' medical_records.txt

# Multiple patterns
awk '/Diabetes/ || /Hypertension/' medical_records.txt

# Field-specific matching
awk '{print $3}' medical_data_with_columns.txt
awk '{print $1, $12}' medical_data_with_columns.txt
awk '$7 > 140 {print $1, $7, $8, $12}' medical_data_with_columns.txt
```


The choice between grep, sed, and awk depends on what you're trying to accomplish with your text processing task. Each tool has its strengths and ideal use cases.

**`Grep` is your search tool** - use it when you simply need to find or filter text based on patterns. It's perfect for quick searches through files to locate specific information, like finding all instances of a particular medical condition or counting occurrences of a term.

**`Sed` is your transformation tool** - use it when you need to make changes to text. It's ideal for tasks like find-and-replace operations, reformatting text, or making systematic changes throughout a file. Think of it as a stream editor that modifies text as it flows through.

**`Awk` is your data processing tool** - use it when you need to work with structured data, perform calculations, or generate reports. It's best for handling columnar data, computing averages or totals, and creating formatted output from raw data.
In simple terms: use grep to find things, sed to change things, and awk to process things. 
