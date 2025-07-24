# 🌐 Module 8: Calling APIs Using `curl` in Shell

---

## 🧠 8.1 What is `curl`?

`curl` is a command-line tool used to **transfer data to/from a server** using protocols like HTTP, HTTPS, FTP, etc.

> In shell scripts, it’s most commonly used for **REST API communication** — fetching data, triggering events, or posting content.

---

## ✅ 8.2 Basic `curl` Syntax

```bash
curl [options] [URL]
```

### 🔹 Example: Basic GET request

```bash
curl https://api.github.com
```

---

## 🔍 8.3 Commonly Used `curl` Flags

| Option | Description                           |
| ------ | ------------------------------------- |
| `-X`   | Specify request method (GET, POST...) |
| `-H`   | Add HTTP headers                      |
| `-d`   | Data to send in the request body      |
| `-s`   | Silent mode (no progress bar)         |
| `-o`   | Write output to a file                |
| `-w`   | Format and show HTTP status           |
| `-i`   | Include response headers              |

---

## 🔎 8.4 GET Request with Query Params

```bash
#!/bin/bash
curl -s "https://api.agify.io?name=ashfaq"
```

Output:

```json
{"name":"ashfaq","age":31,"count":44}
```

---

## 📤 8.5 POST Request with JSON Body

```bash
#!/bin/bash
curl -s -X POST https://jsonplaceholder.typicode.com/posts \
-H "Content-Type: application/json" \
-d '{"title":"Shell Rocks","body":"Module 8","userId":101}'
```

---

## 🧾 8.6 PUT and DELETE Requests

### PUT:

```bash
curl -X PUT -H "Content-Type: application/json" \
-d '{"title":"Updated"}' \
https://jsonplaceholder.typicode.com/posts/1
```

### DELETE:

```bash
curl -X DELETE https://jsonplaceholder.typicode.com/posts/1
```

---

## 🛡 8.7 Adding Custom Headers (e.g., Auth Token)

```bash
curl -X GET https://api.example.com/data \
-H "Authorization: Bearer YOUR_API_TOKEN" \
-H "Accept: application/json"
```

---

## 📦 8.8 Saving Output to File

```bash
curl -s https://api.github.com/users/octocat > user.json
```

---

## 🔍 8.9 Parsing JSON Using `jq`

Install jq:

```bash
sudo apt install jq  # Debian/Ubuntu
```

### Example:

```bash
curl -s https://api.agify.io?name=ashfaq | jq '.age'
```

---

## 🧠 8.10 Real-World Use Cases

| Use Case                    | Description                     |
| --------------------------- | ------------------------------- |
| API health checker          | Ping service and alert if down  |
| Trigger Jenkins/GitHub jobs | Start pipelines or builds       |
| LLM integration             | Send prompt to an AI agent      |
| Slack/Teams notifier        | POST message to webhook         |
| Config fetcher              | Load app config from remote API |

---

## 🔄 8.11 Reusable API Function in Script

```bash
call_api() {
  local endpoint=$1
  curl -s -H "Authorization: Bearer $API_KEY" "$endpoint"
}

call_api "https://api.example.com/data"
```

---

## ✅ Summary

| Concept             | Learned ✅                          |
| ------------------- | ---------------------------------- |
| `curl` GET/POST/PUT | Send requests to APIs              |
| `-H`, `-d`, `-X`    | Customize headers and body         |
| `jq`                | Parse JSON from responses          |
| Auth tokens         | Use `Authorization: Bearer` header |
| Response handling   | Save output, check status          |

---

## 🧪 Practice Exercises

1. **Create `get_weather.sh`**:

   * Accept city as input
   * Call `wttr.in/$city?format=3`
   * Display result

2. **Create `post_note.sh`**:

   * Accept title/body as input
   * POST to JSONPlaceholder

3. **Advanced:** Create a `trigger_job.sh` script that:

   * Calls a Jenkins webhook with a token
   * Verifies response and status

---