# 🧬 Hybrid Shell + Python Scripting

> Use Shell for **orchestration** + Python for **data/logic-heavy tasks**.

---

## ✅ 1. Run a Python Script from Shell

```bash
#!/bin/bash
echo "Calling Python script..."
python3 my_script.py
```

**`my_script.py`:**

```python
print("Hello from Python!")
```

---

## 📥 2. Pass Input from Shell to Python

```bash
#!/bin/bash
echo "Passing input to Python..."
name="Ashfaq"
python3 greet.py "$name"
```

**`greet.py`:**

```python
import sys
name = sys.argv[1]
print(f"Hello, {name}!")
```

---

## 📤 3. Return Output from Python to Shell

```bash
#!/bin/bash
sum=$(python3 calc.py 7 5)
echo "Result: $sum"
```

**`calc.py`:**

```python
import sys
a = int(sys.argv[1])
b = int(sys.argv[2])
print(a + b)  # Printed value is captured in shell
```

---

## 🔁 4. Read File in Shell → Process in Python

**Shell:**

```bash
#!/bin/bash
python3 upper.py < input.txt > output.txt
```

**Python `upper.py`:**

```python
import sys
for line in sys.stdin:
    print(line.strip().upper())
```

---

## 🌐 5. Use Python for API Call from Shell

**Shell:**

```bash
#!/bin/bash
echo "Fetching data..."
python3 weather_fetch.py > weather.txt
```

**Python:**

```python
import requests
r = requests.get("https://wttr.in/Bangalore?format=3")
print(r.text)
```

---

## 🧪 6. Call Python with JSON and Parse Response

**Shell:**

```bash
#!/bin/bash
output=$(python3 parse_json.py '{"name":"Ashfaq","age":30}')
echo "Name from JSON: $output"
```

**Python `parse_json.py`:**

```python
import sys, json
data = json.loads(sys.argv[1])
print(data["name"])
```

---

## 🔗 7. Python Inside Shell Script (Inline)

You can embed Python inside Bash:

```bash
#!/bin/bash
echo "Sum is: $(python3 -c 'print(2 + 3)')"
```

---

## 🔒 8. Virtualenv Activation + Python Script

```bash
#!/bin/bash
source venv/bin/activate
python3 app.py
```

---

## 🧰 9. Real-World Hybrid Script (Validate User)

**Shell:**

```bash
#!/bin/bash
read -p "Enter user ID: " uid
valid=$(python3 check_user.py "$uid")
if [[ "$valid" == "true" ]]; then
  echo "✅ User is valid"
else
  echo "❌ Invalid user"
fi
```

**Python `check_user.py`:**

```python
import sys
uid = sys.argv[1]
if uid.isdigit() and len(uid) == 5:
    print("true")
else:
    print("false")
```

---

## ✅ Summary

| Hybrid Technique            | Benefit                            |
| --------------------------- | ---------------------------------- |
| Pass args to Python         | Shell → Python control flow        |
| Read/return values via echo | Output data to shell               |
| Embed Python in Bash        | One-liner logic (math, JSON, etc.) |
| Combine API + shell script  | Best of both worlds                |

---

## 🧪 Practice Exercises

1. **`get_day.sh`**
   Call `python3 get_day.py` → return current weekday.

2. **`check_temp.sh`**
   Shell script fetches temp via `curl`, passes to Python → Python checks if it’s too hot/cold.

3. **`process_users.sh`**
   Reads usernames from `users.txt`, passes each to `validate.py`, logs results.

---