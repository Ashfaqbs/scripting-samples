# 📋 Module 7: Data Structures in Shell Scripting

---

## 📦 7.1 Arrays (Lists)

### ✅ Declare an Array

```bash
fruits=("apple" "banana" "cherry")
```

### ✅ Access Elements

```bash
echo ${fruits[0]}     # apple
echo ${fruits[1]}     # banana
```

### ✅ Print All Elements

```bash
echo "${fruits[@]}"   # apple banana cherry
```

### ✅ Array Length

```bash
echo "${#fruits[@]}"  # 3
```

### ✅ Iterate Through Array

```bash
for fruit in "${fruits[@]}"; do
  echo "Fruit: $fruit"
done
```

---

## 🗃️ 7.2 Associative Arrays (Key-Value Pairs)

### 🔐 Supported only in `bash 4+`

### ✅ Declare and Populate

```bash
declare -A user
user["name"]="Ashfaq"
user["email"]="ashfaq@example.com"
```

### ✅ Access by Key

```bash
echo "${user["name"]}"   # Ashfaq
```

### ✅ Iterate Key-Value Pairs

```bash
for key in "${!user[@]}"; do
  echo "$key => ${user[$key]}"
done
```

---

## 📌 7.3 Strings as Data

Remember: Everything in Bash is essentially a string. You can still simulate lists and maps.

### ✅ String as CSV-style data

```bash
line="Ashfaq,Developer,India"
IFS=',' read -r name role country <<< "$line"
echo "Name: $name, Role: $role"
```

---

## 🧪 7.4 Real Use Cases

### 📂 Example 1: File Metadata Storage

```bash
declare -A file_info
file_info["filename"]="report.txt"
file_info["size"]="24KB"
file_info["modified"]="2025-07-21"
```

---

### 📊 Example 2: Count Words in Each File

```bash
declare -A word_counts

for file in *.txt; do
  word_counts["$file"]=$(wc -w < "$file")
done

for f in "${!word_counts[@]}"; do
  echo "$f: ${word_counts[$f]} words"
done
```

---

## 🧵 7.5 Nested Data (Simulated)

Bash does not support nested structures natively, but you can use structured formats like:

### ✅ JSON-style data

```bash
user='{"name":"Ashfaq","age":30}'
name=$(echo $user | jq -r '.name')
```

> We'll dive deeper into `jq` in API and JSON processing modules.

---

## 🛠️ 7.6 Modifying Arrays

```bash
arr=("one" "two" "three")

arr+=("four")               # Add
unset arr[1]                # Remove index 1
arr[0]="ONE"                # Update index 0

echo "${arr[@]}"            # Print all
```

---

## ✅ Summary

| Data Type           | Description                     |
| ------------------- | ------------------------------- |
| Indexed Array       | List-like structure             |
| Associative Array   | Key-value pair (dictionary/map) |
| String w/ Delimiter | Simulate records (CSV/TSV)      |
| `declare -A`        | Used to define key-value maps   |
| `IFS`               | Used for splitting/parsing      |

---

## 🧪 Practice Exercises

1. **Create `user_list.sh`**:

   * Define an array of 5 usernames
   * Loop through and greet each user

2. **Create `config_loader.sh`**:

   * Define a key-value map of settings like `env=prod`, `region=us-east`
   * Print them all

3. **Bonus:** Load user data from a CSV-like string and parse it using `IFS`.

---