# 📘 Module 9: Full CRUD Operations with APIs in Shell (Headers + JSON + Error Handling)

This module covers **Create, Read, Update, Delete (CRUD)** operations using REST APIs with `curl`, and how to handle JSON, headers, and responses professionally in shell scripts.

---

## 🧠 9.1 Overview: What is CRUD in API Context?

| Operation | HTTP Method | Purpose                     |
| --------- | ----------- | --------------------------- |
| Create    | POST        | Add new resource            |
| Read      | GET         | Fetch one or more resources |
| Update    | PUT/PATCH   | Modify an existing resource |
| Delete    | DELETE      | Remove a resource           |

We’ll demonstrate with [JSONPlaceholder](https://jsonplaceholder.typicode.com/) — a public REST API for testing.

---

## 🛠️ 9.2 Set Up Reusable API Structure

```bash
#!/bin/bash

BASE_URL="https://jsonplaceholder.typicode.com"
CONTENT_HEADER="Content-Type: application/json"
```

---

## 🧾 9.3 CREATE — POST

### ✅ Create a New Post

```bash
#!/bin/bash

TITLE="Shell Scripting Rocks"
BODY="You're learning CRUD!"
USER_ID=101

RESPONSE=$(curl -s -X POST "$BASE_URL/posts" \
  -H "$CONTENT_HEADER" \
  -d "{\"title\":\"$TITLE\",\"body\":\"$BODY\",\"userId\":$USER_ID}")

echo "Post created:"
echo "$RESPONSE" | jq
```

### 🔍 What it does:

* Uses `-X POST` to send data
* Sends JSON with `-d`
* Adds header `Content-Type: application/json`

---

## 🔍 9.4 READ — GET

### ✅ Read All Posts

```bash
curl -s "$BASE_URL/posts" | jq '.[0:5]'
```

> Gets the first 5 posts and formats them using `jq`.

### ✅ Read a Specific Post by ID

```bash
POST_ID=1
curl -s "$BASE_URL/posts/$POST_ID" | jq
```

---

## ✏️ 9.5 UPDATE — PUT and PATCH

### ✅ PUT (Replaces whole object)

```bash
POST_ID=1
UPDATED_TITLE="Updated by Shell Script"
UPDATED_BODY="This replaces the entire post."

curl -s -X PUT "$BASE_URL/posts/$POST_ID" \
-H "$CONTENT_HEADER" \
-d "{\"id\":$POST_ID,\"title\":\"$UPDATED_TITLE\",\"body\":\"$UPDATED_BODY\",\"userId\":1}" | jq
```

### ✅ PATCH (Modifies specific fields)

```bash
curl -s -X PATCH "$BASE_URL/posts/1" \
-H "$CONTENT_HEADER" \
-d '{"title": "Patched Title"}' | jq
```

---

## ❌ 9.6 DELETE

```bash
curl -s -X DELETE "$BASE_URL/posts/1" -w "\nDeleted post 1\n"
```

> Deletes a post (mock delete, since the test API doesn’t persist changes)

---

## 🧪 9.7 Error Handling and HTTP Status Codes

Use `-w` to extract HTTP status, and `-o` to suppress content.

```bash
response=$(curl -s -o /dev/null -w "%{http_code}" "$BASE_URL/posts/1")

if [ "$response" -eq 200 ]; then
  echo "✅ Resource found!"
elif [ "$response" -eq 404 ]; then
  echo "❌ Not found!"
else
  echo "ℹ️ Received HTTP code: $response"
fi
```

---

## 🛡 9.8 Using Authentication Headers (Example Style)

For APIs that require tokens or API keys:

```bash
API_TOKEN="your_api_key"
curl -H "Authorization: Bearer $API_TOKEN" \
-H "Content-Type: application/json" \
https://secure-api.company.com/endpoint
```

---

## 🧰 9.9 Full Example: CRUD Utility Script

```bash
#!/bin/bash

BASE_URL="https://jsonplaceholder.typicode.com"
HEADER="Content-Type: application/json"

# CREATE
create_post() {
  read -p "Title: " title
  read -p "Body: " body
  curl -s -X POST "$BASE_URL/posts" -H "$HEADER" \
  -d "{\"title\":\"$title\",\"body\":\"$body\",\"userId\":1}" | jq
}

# READ
read_post() {
  read -p "Post ID: " pid
  curl -s "$BASE_URL/posts/$pid" | jq
}

# UPDATE
update_post() {
  read -p "Post ID: " pid
  read -p "New Title: " title
  curl -s -X PATCH "$BASE_URL/posts/$pid" -H "$HEADER" \
  -d "{\"title\":\"$title\"}" | jq
}

# DELETE
delete_post() {
  read -p "Post ID: " pid
  curl -s -X DELETE "$BASE_URL/posts/$pid"
  echo "Post $pid deleted"
}

echo "Choose an action: create | read | update | delete"
read -p "Action: " action

case $action in
  create) create_post ;;
  read) read_post ;;
  update) update_post ;;
  delete) delete_post ;;
  *) echo "Unknown action" ;;
esac
```

> Run the above as `bash crud.sh` and follow prompts.

---

## ✅ Summary

| Concept       | Covered ✅                            |
| ------------- | ------------------------------------ |
| Full CRUD API | POST, GET, PUT/PATCH, DELETE         |
| Headers       | `Content-Type`, `Authorization`      |
| JSON Handling | Inline and from files                |
| Status Codes  | Handled with `-w`, `-o`, `$?`        |
| jq            | Used for parsing and pretty-printing |

---

## 🧪 Practice Exercises

1. **`api_note.sh`**

   * Accept title/body from user input
   * Send a POST request
   * Confirm with a success message and display the ID

2. **`get_user.sh`**

   * Take a user ID
   * Fetch user details using `curl`
   * If not found (404), display a custom error

3. **`api_batch_creator.sh`**

   * Read a CSV file of titles/bodies
   * Loop through and send POST requests for each row

4. **Optional: Auth Token**

   * Add header-based auth using a dummy bearer token
   * Create a function `call_api_with_auth` and reuse it

---