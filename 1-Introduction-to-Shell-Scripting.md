# 🧑‍🏫 Module 1: Introduction to Shell Scripting

---

## 🌟 1.1 What is Shell?

A **shell** is a command-line interface (CLI) that lets users interact with the operating system by typing commands.

The **shell** acts as an interpreter between the user and the operating system kernel.

### Popular Shells:

| Shell  | Description                        | Command |
| ------ | ---------------------------------- | ------- |
| `sh`   | Bourne shell (original UNIX shell) | `sh`    |
| `bash` | Bourne Again SHell (most common)   | `bash`  |
| `zsh`  | Z shell with enhancements          | `zsh`   |
| `ksh`  | Korn shell                         | `ksh`   |

---

## 🤖 1.2 What is Shell Scripting?

A **shell script** is a file containing a series of commands that the shell can execute.

Instead of typing commands one by one, a script lets you run a whole set of them in sequence — **like a recipe or batch job**.

### 🔹 Example: Basic Script

```bash
#!/bin/bash
echo "Hello, world!"
```

---

## 🤔 1.3 Why Learn Shell Scripting?

Shell scripting is essential in real-world systems for:

✅ **Automation**: Backups, file moves, builds
✅ **System Monitoring**: Health checks, alerts
✅ **DevOps**: CI/CD, container orchestration
✅ **Cloud Operations**: AWS CLI, GCP CLI
✅ **Data Pipelines**: Running batch jobs, triggering Python

---

## 🏢 1.4 Where is Shell Scripting Used in Industry?

| Area          | Use Case Example                                   |
| ------------- | -------------------------------------------------- |
| **DevOps**    | Automate build, test, and deploy workflows         |
| **SRE**       | Health checks, system cleanup, service monitors    |
| **Cloud**     | Manage AWS/GCP/Azure resources using CLI tools     |
| **Data Eng.** | Schedule ETL jobs, run Python jobs, move files     |
| **Security**  | Log scrapers, user access checks, intrusion alerts |
| **AI/ML Ops** | Trigger model retraining, monitor GPU usage        |

---

## 🧱 1.5 How Shell Scripts Work

1. You write commands in a `.sh` file
2. Start with a **shebang** line:

   ```bash
   #!/bin/bash
   ```
3. Save and make the script executable:

   ```bash
   chmod +x myscript.sh
   ```
4. Run the script:

   ```bash
   ./myscript.sh
   ```

---

## 🧰 1.6 Tools You’ll Use

| Tool                  | Purpose                        |
| --------------------- | ------------------------------ |
| `bash`                | The shell interpreter          |
| `nano`, `vim`, `code` | Editors for writing scripts    |
| `chmod`               | To set script file permissions |
| `cron`                | Scheduler for timed tasks      |
| `curl`, `jq`          | For API interactions           |
| `psql`                | PostgreSQL client for DB tasks |

---

## 📝 1.7 Best Practices

* Start scripts with: `#!/bin/bash`
* Use comments generously: `# This is a comment`
* Modularize your logic using functions
* Log script output to a file
* Always check exit codes using `$?`

---

## ✅ Summary

| Concept            | You Learned                               |
| ------------------ | ----------------------------------------- |
| What is a shell    | CLI interface for the OS                  |
| Shell scripting    | Writing command sequences in `.sh` files  |
| Why use it?        | For automation, orchestration, monitoring |
| Industry use cases | DevOps, CloudOps, Data Engineering, SRE   |
| Running scripts    | `chmod +x script.sh` then `./script.sh`   |

---

## ✅ Mini Practice

Create your first script:

1. Open terminal

2. Create a file:

   ```bash
   nano hello.sh
   ```

3. Paste:

   ```bash
   #!/bin/bash
   echo "Hi Ashfaq, welcome to Shell Scripting!"
   ```

4. Save with `Ctrl+O`, `Enter`, exit with `Ctrl+X`

5. Make it executable:

   ```bash
   chmod +x hello.sh
   ```

6. Run it:

   ```bash
   ./hello.sh
   ```
