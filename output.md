# API Security Testing – Commands and Outputs (Task 3)

This file documents the terminal commands executed on Kali Linux and their corresponding outputs
during the API Security Risk Analysis task.

---

## 1. Checking Base URL (Homepage Response)

### Command
```bash
curl https://jsonplaceholder.typicode.com
Output
html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <title>JSONPlaceholder - Free Fake REST API</title>
  ...
</head>
<body>
  ...
</body>
</html>
Observation:
The base URL returns an HTML webpage, not JSON. API responses are available only on resource endpoints.

# 2. Fetching Posts (GET /posts)
#Command
bash

curl -s https://jsonplaceholder.typicode.com/posts | head
Output
json
[
  {
    "userId": 1,
    "id": 1,
    "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
    "body": "quia et suscipit
suscipit recusandae consequuntur expedita et cum
reprehenderit molestiae ut ut quas totam
nostrum rerum est autem sunt rem eveniet architecto"
  },
  {
    "userId": 1,
Observation:
The API returns a list of posts in JSON format without requiring authentication.

#3. Fetching Users (GET /users)
Command
bash

curl -s https://jsonplaceholder.typicode.com/users | head
Output
json
Copy code
[
  {
    "id": 1,
    "name": "Leanne Graham",
    "username": "Bret",
    "email": "Sincere@april.biz",
    ...
Observation:
User objects are publicly accessible, which may lead to excessive data exposure in production systems.

#4. Creating a Post Without Authentication (POST /posts)
Command
bash
curl -i -X POST https://jsonplaceholder.typicode.com/posts \
-H "Content-Type: application/json" \
-d '{"title":"test","body":"demo","userId":1}'
Output
http
Copy code
HTTP/2 201 Created
content-type: application/json; charset=utf-8

{
  "title": "test",
  "body": "demo",
  "userId": 1,
  "id": 101
}
Observation:
The API allows data creation without authentication, indicating missing access control.

#5. Updating a Post Without Authentication (PUT /posts/1)
Command
bash
curl -i -X PUT https://jsonplaceholder.typicode.com/posts/1 \
-H "Content-Type: application/json" \
-d '{"title":"changed","body":"updated","userId":1}'
Output
http
Copy code
HTTP/2 200 OK
content-type: application/json; charset=utf-8

{
  "title": "changed",
  "body": "updated",
  "userId": 1,
  "id": 1
}
Observation:
Existing resources can be modified without authentication.

#6. Deleting a Post Without Authentication (DELETE /posts/1)
Command
bash
curl -i -X DELETE https://jsonplaceholder.typicode.com/posts/1
Output
http
Copy code
HTTP/2 200 OK
Observation:
Resources can be deleted without authorization checks.

#7. Rate Limiting Observation
Command
bash
for i in {1..20}; do curl -s -o /dev/null -w "%{http_code}\n" https://jsonplaceholder.typicode.com/posts/1; done
Output
text
Copy code
200
200
200
200
200
200
200
200
200
200
200
200
200
200
200
200
200
200
200
200
Observation:
All requests returned status code 200, indicating no visible rate limiting.

8. Summary
Test Area	Result	Risk Indication
Base URL	HTML Page	Informational
GET /posts	Accessible	Public data exposure
GET /users	Accessible	Excessive data exposure
POST /posts	Allowed	Missing authentication
PUT /posts/1	Allowed	Missing authorization
DELETE /posts/1	Allowed	Missing access control
Rate Limit	Not observed	Abuse potential

Conclusion
The outputs demonstrate that the demo API allows unrestricted access to multiple endpoints.
In a production environment, such behavior would present serious security risks.
Implementing authentication, authorization, rate limiting, and validation controls is recommended.

