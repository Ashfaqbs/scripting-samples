# 🧩 Module 3: Keywords and Basic Syntax in Shell

---

## 🧠 3.1 What are Keywords?

**Keywords** are reserved words used to control the flow and structure of shell scripts. You’ll use them to create **conditions**, **loops**, and **logic blocks**.

---

## 🔑 3.2 Most Common Keywords

| Keyword                               | Purpose                       |
| ------------------------------------- | ----------------------------- |
| `if`, `then`, `else`, `elif`, `fi`    | Conditional logic (if-else)   |
| `for`, `while`, `until`, `do`, `done` | Loops                         |
| `function`                            | Define reusable code blocks   |
| `case`, `esac`                        | Multi-branch condition        |
| `break`, `continue`                   | Control loop execution        |
| `exit`                                | Exit the script with a status |

---

## 📐 3.3 Basic Syntax Rules

### ✔️ Structure

```bash
# If statement
if [ condition ]; then
  # statements
fi

# Loops
for i in 1 2 3; do
  echo $i
done
```

---

## 🧪 3.4 Conditional Expressions

### ✅ Common Test Operators (Used inside `[ ]`)

| Expression      | Meaning             |
| --------------- | ------------------- |
| `-e file`       | File exists         |
| `-d dir`        | Directory exists    |
| `-z string`     | String is empty     |
| `-n string`     | String is not empty |
| `int1 -eq int2` | Equal               |
| `int1 -gt int2` | Greater than        |
| `int1 -lt int2` | Less than           |
| `str1 == str2`  | Strings are equal   |

### 🔁 Boolean Operators

| Operator | Description |
| -------- | ----------- |
| `!`      | NOT         |
| `-a`     | AND         |
| `-o`     | OR          |

---

## ✍️ 3.5 `if-else` Examples

### Example 1: Check if a file exists

```bash
#!/bin/bash
if [ -e "myfile.txt" ]; then
  echo "File exists!"
else
  echo "File not found!"
fi
```

### Example 2: Check user input

```bash
#!/bin/bash
read -p "Enter your age: " age

if [ "$age" -ge 18 ]; then
  echo "You are an adult."
else
  echo "You are a minor."
fi
```

---

## 🔄 3.6 `case` Statement (Switch Alternative)

```bash
#!/bin/bash
read -p "Choose (start|stop|status): " action

case $action in
  start)
    echo "Starting service...";;
  stop)
    echo "Stopping service...";;
  status)
    echo "Service is running.";;
  *)
    echo "Invalid option";;
esac
```

---

## 💥 3.7 Error Handling with `exit`

```bash
#!/bin/bash
echo "Doing something..."
exit 1  # Exits with error status
```

You can check the last command status using:

```bash
echo $?
```

---

## 🧪 Practice Exercises

1. **Write a script `compare.sh`** that:

   * Takes two numbers as input
   * Compares them and prints which one is greater

2. **Write a script `check_file.sh`** that:

   * Accepts a filename from user
   * Prints if it exists and if it's a file or directory

---

## ✅ Summary

| Concept      | You Learned                                     |
| ------------ | ----------------------------------------------- |
| Keywords     | `if`, `then`, `else`, `for`, `case`, etc.       |
| Conditions   | File, string, and numeric checks                |
| Syntax       | `[ condition ]` with spaces                     |
| Logic blocks | Structured flow control with `fi`, `done`, etc. |

---