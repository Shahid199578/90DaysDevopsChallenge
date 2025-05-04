# Day 15 - Introduction to Shell Scripting

## 🧠 What is Shell Scripting?

A shell script is a program written for the shell (command line interpreter) of an operating system. It helps automate tasks that would otherwise be executed one-by-one manually.



[![](https://img.youtube.com/vi/dD2BCyNhswU/0.jpg)](https://www.youtube.com/watch?v=dD2BCyNhswU)

[Watch the video](https://www.youtube.com/watch?v=dD2BCyNhswU)

---

## 🔤 Variables in Shell Scripting

Variables store data that can be used later in the script.

### Syntax:
```bash
variable_name=value
```

### Example:
```bash
#!/bin/bash
name="DevOps Student"
echo "Hello, $name!"
```

### Output:
```
Hello, DevOps Student!
```

> ❗ Note: No spaces around the equal sign when assigning variables.

---

## 📥 User Input

Shell can read user input and store it in variables.

### Example:
```bash
#!/bin/bash
echo "Enter your favorite language:"
read language
echo "You chose $language"
```

---

## 🔁 Conditionals (if-else)

Use conditionals to execute code based on specific conditions.

### Syntax:
```bash
if [ condition ]; then
  # code
elif [ another_condition ]; then
  # code
else
  # code
fi
```

### Example:
```bash
#!/bin/bash
read -p "Enter a number: " num
if [ $num -gt 10 ]; then
  echo "Greater than 10"
else
  echo "10 or less"
fi
```
Comparison Operators:
| Operator | Meaning               |
| -------- | --------------------- |
| `-eq`    | equal to              |
| `-ne`    | not equal to          |
| `-gt`    | greater than          |
| `-lt`    | less than             |
| `-ge`    | greater than or equal |
| `-le`    | less than or equal    |

---

## 🔄 For Loop

Executes a block of code for each item in a list.

### Syntax:
```bash
for var in list
```

### Example:
```bash
#!/bin/bash
for i in 1 2 3 4 5
do
  echo "Iteration $i"
done
```

### Output:
```
Iteration 1
Iteration 2
Iteration 3
Iteration 4
Iteration 5
```

---

## 🔄 While Loop

Repeats as long as a condition is true.

### Example:
```bash
#!/bin/bash
count=1
while [ $count -le 5 ]
do
  echo $count
  ((count++))
done
```

### Output:
```
1
2
3
4
5
```

---

## 📚 Arrays

Used to store multiple values in a single variable.

### Example:
```bash
#!/bin/bash
fruits=("Apple" "Banana" "Mango")
echo "First fruit: ${fruits[0]}"
```

### Output:
```
First fruit: Apple
```

### Looping through an array:
```bash
for fruit in "${fruits[@]}"
do
  echo $fruit
done
```

---

## 🧩 Functions

Functions help reuse code and make scripts modular.

### Syntax:
```bash
function_name() {
  # commands
}
```

### Example:
```bash
#!/bin/bash
greet() {
  echo "Hello, $1!"
}
greet "DevOps"
```

### Output:
```
Hello, DevOps!
```

---

## 🐞 Debugging with `set -x`

Debug mode prints each command before executing it.

### Example:
```bash
#!/bin/bash
set -x
fruits=("Apple" "Banana" "Mango")
for fruit in "${fruits[@]}"
do
  echo $fruit
done
set +x
```

### Sample Output:
```
+ fruits=("Apple" "Banana" "Mango")
+ for fruit in "${fruits[@]}"
+ echo Apple
Apple
+ echo Banana
Banana
+ echo Mango
Mango
```

---

## 📌 Summary

| Concept     | Use                                     |
|-------------|------------------------------------------|
| Variables   | Store and reuse values                   |
| Input       | Accept user input                        |
| If-Else     | Execute logic based on conditions        |
| Loops       | Automate repetitive tasks                |
| Arrays      | Store multiple values                    |
| Functions   | Modularize code                          |
| Debugging   | Trace command execution                  |

