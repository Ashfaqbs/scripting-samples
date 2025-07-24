# 🔁 Module 6: Loops in Shell Scripting

---

## 🧠 6.1 Why Use Loops?

Loops help you **execute a block of code multiple times**, making scripts:

* More concise
* Easier to manage
* Perfect for batch tasks like processing files, users, or API calls

---

## 📦 6.2 `for` Loop

### 🔹 Syntax:

```bash
for var in value1 value2 value3; do
  # commands
done
```

### ✅ Example 1: Simple list

```bash
for name in Ashfaq Sara John; do
  echo "Hello, $name"
done
```

### ✅ Example 2: Range loop

```bash
for i in {1..5}; do
  echo "Number: $i"
done
```

Or using C-style syntax:

```bash
for ((i=1; i<=5; i++)); do
  echo "i: $i"
done
```

---

## ⏳ 6.3 `while` Loop

### 🔹 Syntax:

```bash
while [ condition ]; do
  # commands
done
```

### ✅ Example:

```bash
count=1
while [ $count -le 3 ]; do
  echo "Count: $count"
  count=$((count + 1))
done
```

---

## ⛔ 6.4 `until` Loop

### 🔹 Syntax:

```bash
until [ condition ]; do
  # commands
done
```

Runs **until** the condition becomes **true** (opposite of `while`).

### ✅ Example:

```bash
x=1
until [ $x -gt 3 ]; do
  echo "x: $x"
  x=$((x + 1))
done
```

---

## 🔂 6.5 `break` and `continue`

### ✅ `break` → Exit the loop immediately

### ✅ `continue` → Skip to next iteration

```bash
for i in {1..5}; do
  if [ $i -eq 3 ]; then
    echo "Skipping 3"
    continue
  fi
  if [ $i -eq 4 ]; then
    echo "Breaking at 4"
    break
  fi
  echo $i
done
```

---

## 🧪 6.6 Real-World Loop Examples

### 🔍 Example 1: Loop through files

```bash
for file in *.txt; do
  echo "Processing $file"
  cat "$file"
done
```

### 🧑‍🤝‍🧑 Example 2: Loop through user input

```bash
read -p "How many times to greet? " n
for ((i=1; i<=n; i++)); do
  echo "Hello, $i"
done
```

### 🔄 Example 3: Retry until success

```bash
attempt=1
while ! ping -c1 google.com &>/dev/null; do
  echo "Try $attempt: Waiting for internet..."
  sleep 2
  attempt=$((attempt + 1))
done
echo "Connected!"
```

---

## 📌 6.7 Looping Through Arrays (Preview for next module)

```bash
arr=("apple" "banana" "cherry")

for item in "${arr[@]}"; do
  echo "$item"
done
```

---

## ✅ Summary

| Loop Type  | When to Use                           |
| ---------- | ------------------------------------- |
| `for`      | Fixed iterations or lists             |
| `while`    | Run while condition is true           |
| `until`    | Run until condition becomes true      |
| `break`    | Exit the loop early                   |
| `continue` | Skip current iteration, continue loop |

---

## 🧪 Practice Exercises

1. **Create `loop_practice.sh`**:

   * Loop from 1 to 10
   * Print even numbers only

2. **Create `file_reader.sh`**:

   * Read each `.log` file from a directory
   * Count lines in each

---