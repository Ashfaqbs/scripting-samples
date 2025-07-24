# 🗃️ Module 10: Connecting to PostgreSQL from Shell Scripts

---

## 🧠 10.1 Why Connect to PostgreSQL in Shell?

Shell + PostgreSQL allows you to:

* Run queries in CI/CD pipelines
* Automate backups and restores
* Validate DB health/status
* Trigger data cleanup or audits
* Feed database results into Python/LLM workflows

---

## ⚙️ 10.2 Requirements

Make sure you have the PostgreSQL CLI tools installed.

### ✅ Installation:

**Ubuntu/Debian:**

```bash
sudo apt update && sudo apt install postgresql-client
```

**macOS:**

```bash
brew install libpq
brew link --force libpq
```

---

## 🔑 10.3 Common `psql` Syntax

```bash
psql -h <host> -U <user> -d <database> -c "<SQL>"
```

* `-h` → hostname
* `-U` → user
* `-d` → database
* `-c` → SQL command (quoted)

---

## 🔐 10.4 Authentication Options

1. **Prompt for Password:**

```bash
PGPASSWORD="mypassword" psql -U myuser -d mydb -c "SELECT NOW();"
```

2. **Use `.pgpass` file (recommended for automation):**

```bash
# In ~/.pgpass:
hostname:port:database:username:password
```

Then:

```bash
chmod 600 ~/.pgpass
psql -h hostname -U username -d database -c "SELECT version();"
```

---

## 🧪 10.5 Query Examples via Script

### ✅ Select Query

```bash
#!/bin/bash

PGPASSWORD="admin"
psql -h localhost -U postgres -d mydb -c "SELECT * FROM users LIMIT 5;"
```

### ✅ Capture Output

```bash
result=$(psql -h localhost -U postgres -d mydb -t -c "SELECT count(*) FROM users;")
echo "User count: $result"
```

> `-t` removes headers/formatting for easy parsing

---

## 📥 10.6 Insert / Update / Delete

```bash
# INSERT
psql -U postgres -d mydb -c "INSERT INTO logs(message) VALUES('Shell script inserted this');"

# UPDATE
psql -U postgres -d mydb -c "UPDATE users SET active = false WHERE last_login < now() - interval '1 year';"

# DELETE
psql -U postgres -d mydb -c "DELETE FROM logs WHERE created_at < now() - interval '30 days';"
```

---

## 📤 10.7 Export Query Results to a File

```bash
psql -U postgres -d mydb -c "SELECT * FROM users" -F $'\t' --no-align -o users.tsv
```

| Flag         | Meaning                      |
| ------------ | ---------------------------- |
| `-F`         | Output field separator       |
| `--no-align` | Unaligned output (flat file) |
| `-o`         | Output to file               |

---

## 📦 10.8 Automating Backups and Restores

### ✅ Backup:

```bash
PGPASSWORD=admin pg_dump -U postgres -h localhost -F c mydb > backup.dump
```

### ✅ Restore:

```bash
PGPASSWORD=admin pg_restore -U postgres -h localhost -d mydb backup.dump
```

---

## 🔁 10.9 Running SQL Files

```bash
psql -U postgres -d mydb -f ./create_tables.sql
```

> Useful for running migrations or batch insertions.

---

## 🧰 10.10 Real-World Script: DB Health Monitor

```bash
#!/bin/bash

PGPASSWORD=admin
host="localhost"
user="postgres"
db="mydb"

result=$(psql -h $host -U $user -d $db -t -c "SELECT pg_is_in_recovery();")

if [[ "$result" == " f" ]]; then
  echo "✅ DB is in primary mode."
else
  echo "⚠️ DB is in recovery mode!"
fi
```

---

## 🛠️ 10.11 Error Handling and Exit Codes

```bash
PGPASSWORD=wrong psql -U postgres -d mydb -c "SELECT 1"
if [ $? -ne 0 ]; then
  echo "❌ Failed to connect or run query"
  exit 1
fi
```

---

## ✅ Summary

| Task                 | Tool & Flag                          |
| -------------------- | ------------------------------------ |
| Run query            | `psql -c "SQL"`                      |
| Insert/update/delete | Same as select                       |
| Export results       | `-F` (delimiter), `--no-align`, `-o` |
| Backup/restore       | `pg_dump`, `pg_restore`              |
| SQL from file        | `psql -f filename.sql`               |
| Password handling    | `PGPASSWORD=...`, `.pgpass`          |

---

## 🧪 Practice Exercises

1. **Create `user_count.sh`**

   * Connect to a DB
   * Count rows in `users` table
   * Display the number

2. **Create `auto_backup.sh`**

   * Dump a PostgreSQL DB to a timestamped file
   * Schedule with cron (next module!)

3. **Create `batch_update.sh`**

   * Run an update query from a `.sql` file
   * Handle errors and log output

---