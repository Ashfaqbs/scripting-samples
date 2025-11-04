# Understanding systemd (Systemmd) Files and Service Management Across Operating Systems

A systemd file (often mistakenly called a “systemmd” file) is a configuration file used by **systemd** — the system and service manager used in most modern Linux distributions. It defines how services start, stop, and interact with the rest of the system. Systemd simplifies system initialization, service dependency handling, and process supervision.

---

## 1. Purpose of systemd

Before systemd, Linux systems used older init systems such as **SysVinit** or **Upstart**. These had limitations in managing service dependencies and monitoring processes efficiently.
systemd introduced a unified way to manage services with parallel startup, integrated logging (via `journald`), and precise dependency control.

---

## 2. How systemd Works

systemd uses **unit files** — text-based configuration files that define how services, sockets, mounts, and timers behave.
Each unit file contains sections like `[Unit]`, `[Service]`, and `[Install]`. These sections describe dependencies, startup commands, restart behavior, and installation targets.

### Example: Simple systemd Service

```ini
[Unit]
Description=Example Application
After=network.target

[Service]
User=ubuntu
ExecStart=/usr/bin/python3 /opt/app.py
Restart=always

[Install]
WantedBy=multi-user.target
```

---

## 3. Service Management in Different Operating Systems

### Linux (Ubuntu, Fedora, Debian, CentOS)

Most modern Linux distributions use systemd as their default init system.
Service files are typically stored in `/etc/systemd/system/` or `/lib/systemd/system/`.
Common commands include:

```bash
systemctl start <service>
systemctl stop <service>
systemctl enable <service>
systemctl status <service>
```

### Unix (Traditional)

Older Unix systems often use **SysVinit** or **BSD-style init scripts**, typically located in `/etc/init.d/`.
These are shell scripts executed sequentially at boot.
Modern Unix-like systems such as macOS use **launchd**, which functions similarly to systemd but with Apple’s own configuration format (`.plist` files).

### Windows

Windows uses the **Service Control Manager (SCM)** for managing background services.
Services can be created and configured using:

* `sc.exe`
* PowerShell (`New-Service`)
* The **Services** management console (`services.msc`)

While conceptually similar (defining how processes start, stop, and restart), systemd is more declarative and dependency-aware.

---

## 4. Real-World Example: Starting Two Java Services Sequentially

**Scenario:**
Two Java JAR files — `jar1.jar` and `jar2.jar` — are located in `/home/ubuntu/Downloads/`.
`jar1` must start first, followed by `jar2`, and both should start automatically at boot.

### Service File 1: jar1.service

```ini
[Unit]
Description=Java Service 1
After=network.target postgresql.service
Requires=postgresql.service

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/Downloads
ExecStart=/usr/bin/java -jar /home/ubuntu/Downloads/jar1.jar
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```

### Service File 2: jar2.service

```ini
[Unit]
Description=Java Service 2
After=jar1.service
Requires=jar1.service

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/Downloads
ExecStart=/usr/bin/java -jar /home/ubuntu/Downloads/jar2.jar
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```

### Enabling and Starting

```bash
sudo systemctl daemon-reload
sudo systemctl enable jar1.service
sudo systemctl enable jar2.service
```

After enabling, both services start automatically at boot with `jar1` starting before `jar2`.
To verify their state:

```bash
systemctl status jar1.service
systemctl status jar2.service
```

Logs can be viewed using:

```bash
journalctl -u jar1.service -f
journalctl -u jar2.service -f
```

---

## 5. Usage Commands

Once systemd services are configured, the following commands manage them:

| Command                       | Description                                     |
| ----------------------------- | ----------------------------------------------- |
| `systemctl start <service>`   | Start the service manually                      |
| `systemctl stop <service>`    | Stop the service                                |
| `systemctl restart <service>` | Restart (useful after updating JARs or configs) |
| `systemctl enable <service>`  | Enable automatic startup on boot                |
| `systemctl disable <service>` | Prevent service from starting automatically     |
| `systemctl status <service>`  | Check service status                            |
| `journalctl -u <service>`     | View logs                                       |

---

## 6. Services That Start Automatically (e.g., PostgreSQL)

Some services, such as **PostgreSQL**, start automatically after installation.
This occurs because their installation packages include pre-configured **systemd unit files** that are **enabled by default**.
When a service is enabled, systemd creates a **symbolic link** from its unit file to a boot target (for example, `multi-user.target`), ensuring it runs automatically during system startup.

### Example: PostgreSQL

When PostgreSQL is installed with:

```bash
sudo apt install postgresql
```

systemd automatically registers and enables `/lib/systemd/system/postgresql.service`.

To confirm:

```bash
systemctl is-enabled postgresql
systemctl status postgresql
```

If the output shows `enabled`, PostgreSQL starts automatically during every reboot.

This behavior is managed internally by systemd, which maintains a **dependency graph** of all enabled services.
During system initialization, systemd:

1. Reads all enabled unit files.
2. Determines the startup order based on `After=` and `Requires=` dependencies.
3. Starts them in parallel where possible for faster boot times.

PostgreSQL’s unit file typically depends on `network.target`, ensuring the database starts **after the network is available**.
If the service fails, systemd can automatically restart it based on the `[Service]` configuration.

Manual control remains available:

```bash
sudo systemctl disable postgresql
sudo systemctl enable postgresql
sudo systemctl restart postgresql
```

This architecture provides a reliable and dependency-aware mechanism for starting and supervising critical services automatically in the background.

---

## 7. Summary

* **systemd** standardizes how services are started, stopped, and monitored in Linux.
* **Unit files** define service behavior, dependencies, and restart policies.
* Many system packages, such as PostgreSQL, automatically register themselves as **enabled services** upon installation.
* Custom applications, such as JAR-based services, can be configured through simple `.service` files.
* The startup sequence can be controlled precisely using `After=` and `Requires=` directives.
