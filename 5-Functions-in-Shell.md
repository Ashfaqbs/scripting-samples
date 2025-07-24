# 🔁 Module 5: Functions in Shell

---

## 🧠 5.1 What is a Function?

A **function** is a reusable block of code you define once and call multiple times. It helps:

* Reduce repetition
* Organize logic
* Modularize large scripts

---

## 🔧 5.2 Defining a Function

### ✅ Basic Syntax

```bash
function_name() {
  # commands
}
```

Or

```bash
function function_name {
  # commands
}
```

### Example:

```bash
greet() {
  echo "Hello, $USER!"
}

greet  # Function call
```

---

## 🎯 5.3 Functions With Parameters

Functions can receive input like positional arguments `$1`, `$2`, etc.

### Example:

```bash
greet_user() {
  echo "Hello, $1!"
}

greet_user "Ashfaq"
```

---

## 🧮 5.4 Functions With Return Values

Functions in bash **return exit codes** (0 = success), but to return actual values, use `echo` and capture it.

### Example:

```bash
add() {
  result=$(( $1 + $2 ))
  echo $result
}

sum=$(add 5 10)
echo "Sum is: $sum"
```

---

## 🔁 5.5 Function Scope

* Variables declared inside a function are **global by default**
* Use `local` for function-local variables

### Example:

```bash
calculate() {
  local x=10
  echo "Inside: $x"
}

calculate
echo "Outside: $x"  # Will be empty
```

---

## 🔄 5.6 Nesting and Recursion

Yes, functions can call other functions:

```bash
greet() {
  echo "Hi, $1!"
  cheer
}

cheer() {
  echo "Have a great day!"
}

greet "Ashfaq"
```

---

## 🔥 5.7 Real-World Example: Validation Function

```bash
is_number() {
  if [[ $1 =~ ^[0-9]+$ ]]; then
    return 0  # Success
  else
    return 1  # Failure
  fi
}

read -p "Enter number: " num
if is_number "$num"; then
  echo "Valid number!"
else
  echo "Invalid input!"
fi
```

---

## 🚀 5.8 Multi-Purpose Function

```bash
calculate() {
  case $2 in
    +) echo $(($1 + $3));;
    -) echo $(($1 - $3));;
    \*) echo $(($1 * $3));;
    /) echo $(($1 / $3));;
    *) echo "Unknown operation";;
  esac
}

result=$(calculate 20 + 5)
echo "Result: $result"
```

---

## ✅ Summary

| Feature         | You Learned                      |
| --------------- | -------------------------------- |
| Define function | `function_name() {}`             |
| Call function   | `function_name`                  |
| Use parameters  | `$1`, `$2`, etc.                 |
| Return values   | Use `echo` and capture via `$()` |
| Local variables | Use `local`                      |

---

## 🧪 Practice Exercises

1. **Create `math_utils.sh`**:

   * Add functions: `add`, `subtract`, `multiply`, `divide`
   * Take inputs, call respective function

2. **Create `login_checker.sh`**:

   * Function `check_login user` — checks if Linux user exists
   * Use `id "$1"` or `getent passwd "$1"` for checking

---