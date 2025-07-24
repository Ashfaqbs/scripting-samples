# 🧮 Module 4: Variables and Data Types

---

## 📦 4.1 What Are Variables?

Variables are containers used to store information that can be referenced and manipulated later.

### ✅ Declaration Syntax:

```bash
variable_name=value   # NO SPACES around =
```

✅ Good:

```bash
name="Ashfaq"
```

❌ Bad:

```bash
name = "Ashfaq"  # This will break
```

---

## 🔄 4.2 Accessing Variables

```bash
echo "Hello, $name"
```

Always prefix with `$` to get the value. You can also use:

```bash
echo "Hello, ${name}"
```

---

## 🧪 4.3 Reading Input into Variables

```bash
read -p "Enter your name: " user
echo "Hi $user!"
```

---

## 🧠 4.4 Simulated Data Types in Shell

Bash treats all variables as **strings** by default, but you can simulate types.

### ✅ Strings

```bash
greeting="Hello"
```

### ✅ Integers (Arithmetic Support)

```bash
a=10
b=5
sum=$((a + b))
echo "Sum: $sum"
```

Supported operators:

* `+`, `-`, `*`, `/`, `%` (mod)
* Comparison: `-eq`, `-ne`, `-lt`, `-gt`, `-le`, `-ge`

---

## 🧪 4.5 String Operations

```bash
str="Hello Ashfaq"

echo "${#str}"         # Length of string
echo "${str:6}"        # Substring from index 6
echo "${str:0:5}"      # First 5 characters
```

---

## 🔄 4.6 Type Checking and Validation

```bash
read -p "Enter number: " num
if [[ "$num" =~ ^[0-9]+$ ]]; then
  echo "It's a number."
else
  echo "Not a number!"
fi
```

---

## 📄 4.7 Exporting Variables (Environment)

```bash
export API_KEY="abc123"
```

* Makes the variable accessible to child processes
* Useful for secrets, config, paths

---

## ⚠️ 4.8 Special Variables

| Variable   | Meaning                                 |
| ---------- | --------------------------------------- |
| `$0`       | Script name                             |
| `$1`, `$2` | Positional arguments                    |
| `$@`, `$*` | All arguments                           |
| `$#`       | Total number of arguments               |
| `$$`       | PID of the current script               |
| `$?`       | Exit code of last command (0 = success) |

### 🧪 Example:

```bash
#!/bin/bash
echo "Script name: $0"
echo "First argument: $1"
echo "Total args: $#"
```

Run:

```bash
./myscript.sh hello world
```

---

## 🔒 4.9 Constants (Read-only Variables)

```bash
readonly pi=3.14159
pi=22   # This will cause an error
```

---

## ✅ Summary

| Concept    | You Learned             |
| ---------- | ----------------------- |
| Declare    | `var=value`             |
| Access     | `$var`, `${var}`        |
| Read input | `read -p "msg" varname` |
| Math       | `$((a + b))`            |
| Strings    | Substrings, length      |
| Arguments  | `$1`, `$#`, `$@`, `$?`  |

---

## 🧪 Practice Exercises

1. **Create `calculator.sh`**:

   * Ask for two numbers
   * Ask for operator (+, -, \*, /)
   * Perform and display result

2. **Create `user_info.sh`**:

   * Read name, age, email
   * Display all in formatted string

---