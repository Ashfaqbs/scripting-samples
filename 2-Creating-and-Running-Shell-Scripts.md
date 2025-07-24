# 🧱 Module 2: Creating and Running Shell Scripts

---

## 📁 2.1 Creating a Shell Script File

Shell scripts are just plain text files that contain command-line instructions.

### 🧑‍💻 Step-by-Step:

1. **Open a terminal**
2. **Create a file** with `.sh` extension (conventionally):

   ```bash
   touch hello.sh
   ```
3. **Edit the file** with your preferred editor:

   * Using `nano`:

     ```bash
     nano hello.sh
     ```
   * Using `vim`, `code`, or any editor you prefer.

---

## 🧵 2.2 Shebang Line (Very Important)

The **first line** of a shell script should be:

```bash
#!/bin/bash
```

This is called a **shebang**. It tells the system which interpreter to use to run the script (in this case, `bash`).

✅ **Other options:**

* `#!/bin/sh` — POSIX-compliant shell
* `#!/usr/bin/env bash` — Portable way if you’re unsure of the bash path

---

## ✍️ 2.3 Writing Your First Script

```bash
#!/bin/bash
# This script greets the user

echo "Hello, $USER!"
echo "Today is $(date)"
```

Save the file (`Ctrl+O`, then `Enter` in `nano`) and exit (`Ctrl+X`).

---

## 🔓 2.4 Making the Script Executable

To run the script, you need to make it executable:

```bash
chmod +x hello.sh
```

This sets the **execute (x)** permission on the file.

---

## 🚀 2.5 Running the Script

### ✅ Run using current shell:

```bash
./hello.sh
```

### ⚠️ If you see `Permission denied`:

Make sure the script has execute permission:

```bash
ls -l hello.sh
```

Output should show something like:
`-rwxr-xr-x`

---

### ✅ Alternative Way: Use Interpreter

You can also run the script by explicitly calling `bash`:

```bash
bash hello.sh
```

---

## 🧪 2.6 Examples to Try

### Example 1: Display Current Directory

```bash
#!/bin/bash
echo "You're in: $(pwd)"
```

### Example 2: List Files

```bash
#!/bin/bash
echo "Files in this directory:"
ls -l
```

### Example 3: Show Date and Time

```bash
#!/bin/bash
echo "Today is: $(date)"
```

---

## 📁 2.7 Organizing Scripts

* Store your scripts in a dedicated folder:

  ```bash
  mkdir ~/scripts
  mv *.sh ~/scripts/
  ```

* Add to your `PATH` for global access (optional but useful):
  Add this to your `.bashrc` or `.zshrc`:

  ```bash
  export PATH=$PATH:$HOME/scripts
  ```

---

## 🔁 2.8 Run Script Automatically (Optional Peek Ahead)

* You can schedule scripts using `cron` (covered in Module 11)

---

## ✅ Summary

| Concept            | Learned ✅                     |
| ------------------ | ----------------------------- |
| Script file        | Created with `.sh` extension  |
| Shebang line       | `#!/bin/bash`                 |
| Make it executable | `chmod +x file.sh`            |
| Run the script     | `./file.sh` or `bash file.sh` |

---

## 📚 Practice

Create a script named `userinfo.sh`:

```bash
#!/bin/bash
echo "Hi $USER!"
echo "Your home directory is: $HOME"
echo "Current working directory: $(pwd)"
echo "Shell in use: $SHELL"
```

Run it and observe the output.

---