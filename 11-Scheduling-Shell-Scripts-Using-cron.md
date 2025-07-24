# ⏰ Module 11: Scheduling Shell Scripts Using `cron`

---

## 🧠 11.1 What is `cron`?

`cron` is a built-in Linux utility that schedules **commands or scripts** to run **automatically at a specified time or interval**.

Think:

* Nightly backups
* Hourly API data pulls
* Weekly email reports
* Auto cleanup of temp files

The scheduler is managed by a **daemon** called `crond`.

---

## 📘 11.2 The `crontab`

Each user has their own **crontab file** (`cron table`) that defines their scheduled tasks.

### ✅ View Current Cron Jobs

```bash
crontab -l
```

### ✅ Open Crontab Editor

```bash
crontab -e
```

> It opens in your default editor (usually `vim` or `nano`)

---

## 📅 11.3 Cron Time Syntax

Cron expressions have **5 fields** followed by the **command/script**:

```bash
*  *  *  *  *  command
|  |  |  |  |
|  |  |  |  └─── Day of week (0–6, Sunday=0)
|  |  |  └────── Month (1–12)
|  |  └───────── Day of month (1–31)
|  └──────────── Hour (0–23)
└─────────────── Minute (0–59)
```

---

## 🕰️ 11.4 Common Cron Schedule Examples

| Schedule         | Expression     | Meaning                  |
| ---------------- | -------------- | ------------------------ |
| Every minute     | `* * * * *`    | Runs every minute        |
| Every hour       | `0 * * * *`    | At start of every hour   |
| Daily at 1 AM    | `0 1 * * *`    | 01:00 AM every day       |
| Weekly on Sunday | `0 9 * * 0`    | 09:00 AM every Sunday    |
| Monthly on 1st   | `0 0 1 * *`    | Midnight on 1st of month |
| Every 15 minutes | `*/15 * * * *` | Every 15 minutes         |

---

## 🔁 11.5 Running a Script with Cron

Let's say you have this script:

```bash
/home/ashfaq/scripts/db_backup.sh
```

Make sure it's:

* **Executable:** `chmod +x db_backup.sh`
* **Working with full paths:** Always use **absolute paths** in cron scripts

### ✅ Example Cron Entry

```bash
0 2 * * * /home/ashfaq/scripts/db_backup.sh >> /home/ashfaq/logs/db_backup.log 2>&1
```

> Runs every day at 2 AM and logs both stdout and stderr.

---

## 🧪 11.6 Real-World Use Cases

### ✅ Daily Database Backup

```bash
0 3 * * * /usr/local/bin/backup.sh
```

### ✅ API Data Fetch Every Hour

```bash
0 * * * * /home/ashfaq/fetch_weather.sh
```

### ✅ Cleanup Temp Files Every 6 Hours

```bash
0 */6 * * * /home/ashfaq/cleanup.sh
```

---

## 🧾 11.7 Logging and Monitoring Cron Jobs

### ✅ Log stdout and stderr

```bash
*/30 * * * * /home/user/script.sh >> /home/user/script.log 2>&1
```

### ✅ Email Output (if configured)

```bash
MAILTO="ashfaq@example.com"
```

Add it as the first line in your `crontab`.

---

## ⚠️ 11.8 Troubleshooting Cron Jobs

| Problem                              | Fix / Tip                             |
| ------------------------------------ | ------------------------------------- |
| Script runs manually but not in cron | Use **full paths** for files/commands |
| No output                            | Redirect stdout/stderr to log         |
| Permissions error                    | Add `chmod +x`, run as correct user   |
| Env vars not available               | Set them inside script                |
| Cron daemon not running              | Use `sudo systemctl status cron`      |

---

## 🧰 11.9 Best Practices

✅ Use `bash -x` to debug scripts manually
✅ Log everything to a file
✅ Wrap logic in functions to isolate failures
✅ Use environment variables explicitly
✅ Test scripts outside cron first
✅ Always use absolute paths

---

## ✅ Summary

| Concept      | You Learned                            |
| ------------ | -------------------------------------- |
| `cron`       | Task scheduler                         |
| `crontab -e` | Edit scheduled jobs                    |
| Time format  | `* * * * *` (minute → week)            |
| Logging      | `>> log 2>&1`                          |
| Use cases    | Backups, cleanups, API fetches, alerts |

---

## 🧪 Practice Exercises

1. **Schedule `hello.sh`**

   * Prints "Good morning, Ashfaq"
   * Run every day at 9:00 AM
   * Log output to `~/cron_hello.log`

2. **Automated Cron + DB Backup**

   * Run `db_backup.sh` every midnight
   * Save backups with timestamp in filename
   * Log success/failure to file

3. **Hourly Weather Fetch**

   * Script calls `wttr.in` and saves response to a file
   * Cron runs it every hour and appends to a daily log

---