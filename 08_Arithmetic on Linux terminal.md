# 12. Arithmetic on Linux terminal 

## 12.1. Basic arithmetic with `expr`

The `expr` command is one of the oldest ways to perform arithmetic in the shell.

```
# Basic operations
expr 5 + 3    # Addition
expr 10 - 4   # Subtraction
expr 6 \* 2   # Multiplication (note the escape character)
expr 15 / 3   # Division
expr 17 % 5   # Modulus (remainder)
```

## 12.2. Using `bc` for Advanced calculations

The `bc` (basic calculator) command is more powerful than expr and supports floating-point arithmetic.

For example, 

```
# One-line calculations
echo "5.7 * 3.2" | bc                 
echo "scale=2; 10/3" | bc       #scale means decimal points

# More complex calculations
echo "scale=4; sqrt(2)" | bc            
echo "scale=2; 3.14159 * 5^2" | bc
```

## 12.3. Shell arithmetic 

Bash provides its own arithmetic expansion:

For example, 

```
# Using (( )) for integer arithmetic
echo $((5 + 3))
echo $((10 * 5))

# Using variables
x=5
y=3
echo $((x + y))
echo $((x * y))
```

You can also do array mathematics on shell

```
numbers=(1 2 3 4 5)
sum=0
for num in "${numbers[@]}"; do
    ((sum += num))
done
echo "Sum: $sum"
```
