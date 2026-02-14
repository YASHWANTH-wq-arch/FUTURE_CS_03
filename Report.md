# API Security Risk Analysis Report (Task 3)

---

## 1. Executive Summary

This report analyzes the security posture of a public demo REST API (JSONPlaceholder) using basic API security testing techniques. The assessment focused on key areas such as authentication, authorization, data exposure, input validation, and rate limiting.

The analysis identified multiple security weaknesses, including the absence of authentication for write operations, lack of authorization controls, excessive data exposure, and missing rate limiting. Although the tested API is intended for demonstration purposes, these weaknesses would represent serious risks in a production environment.

---

## 2. Scope

**API Name:** JSONPlaceholder (Demo REST API)  
**Base URL:** https://jsonplaceholder.typicode.com  
**Testing Tools:** curl (Kali Linux Terminal)  
**Test Date:** 14-02-2026  

### In Scope
- Endpoint accessibility testing  
- Authentication and authorization behavior  
- Data exposure analysis  
- Input validation behavior  
- Rate limiting observation  

### Out of Scope
- Exploitation of real systems  
- Attacking infrastructure  
- Accessing private or confidential user data  

---

## 3. Methodology

The following high-level checks were performed:

- Endpoint review (methods, responses, error handling)
- Authentication and authorization behavior analysis
- Data exposure review (user and post data)
- Input validation and error message review
- Rate limiting and abuse protection observation

The testing approach was aligned conceptually with the OWASP API Security Top 10 guidelines.

---

## 4. Endpoints Tested

| Endpoint | Method | Purpose | Auth Required? | Notes |
|----------|--------|---------|---------------|-------|
| /posts | GET | Fetch all posts | No | Publicly accessible |
| /users | GET | Fetch all users | No | Returns full user data |
| /posts | POST | Create new post | No | Works without authentication |
| /posts/1 | PUT | Update post | No | Works without authentication |
| /posts/1 | DELETE | Delete post | No | Works without authentication |

---

## 5. Findings Summary

| ID | Risk | Severity | Evidence | Impact | Recommendation |
|----|------|----------|----------|--------|----------------|
| F1 | Missing Authentication | High | POST/PUT/DELETE screenshots | Unauthorized data modification | Enforce authentication |
| F2 | Missing Authorization Controls | High | Same access for all users | Privilege escalation | Implement RBAC/ABAC |
| F3 | Excessive Data Exposure | Medium | GET /users screenshot | Privacy leakage | Limit response fields |
| F4 | No Rate Limiting | Medium | Rate test screenshot | Abuse and DoS risk | Apply rate limiting |
| F5 | Weak Input Validation | Low/Medium | Payload test output | Data integrity issues | Enforce validation rules |

---

## 6. Detailed Findings

---

### F1: Missing Authentication for Write Operations

**Severity:** High  

**Description:**  
The API allows POST, PUT, and DELETE operations without requiring any form of authentication such as API keys, tokens, or sessions.

**Steps to Reproduce:**
1. Send a POST request to `/posts` without authentication.
2. Observe that the API successfully creates a resource.

**Evidence:**  
See screenshots:  
- `03-post-no-auth.png`  
- `04-put-no-auth.png`  
- `05-delete-no-auth.png`

**Impact:**  
In production systems, attackers could create, modify, or delete data, leading to loss of integrity and trust.

**Recommendation:**  
- Enforce authentication on all write endpoints.
- Use JWT, OAuth2, or API key mechanisms.
- Reject unauthorized requests with `401 Unauthorized`.

---

### F2: Missing Authorization Controls

**Severity:** High  

**Description:**  
The API does not differentiate between user roles. All users can perform privileged operations without restriction.

**Steps to Reproduce:**
1. Perform PUT or DELETE requests without any role information.
2. Observe successful responses.

**Evidence:**  
Write operation screenshots.

**Impact:**  
Leads to privilege escalation and unauthorized administrative actions.

**Recommendation:**  
- Implement Role-Based Access Control (RBAC).
- Enforce object-level ownership checks.
- Restrict sensitive endpoints.

---

### F3: Excessive Data Exposure

**Severity:** Medium  

**Description:**  
The `/users` endpoint returns complete user objects including unnecessary fields.

**Steps to Reproduce:**
1. Send GET request to `/users`.
2. Review returned fields.

**Evidence:**  
`02-get-users.png`

**Impact:**  
Increases risk of privacy breaches and user enumeration.

**Recommendation:**  
- Return only required fields.
- Apply response filtering.
- Use Data Transfer Objects (DTOs).

---

### F4: No Rate Limiting Observed

**Severity:** Medium  

**Description:**  
Multiple rapid requests were accepted without any throttling.

**Steps to Reproduce:**
1. Send multiple requests in a loop.
2. Observe all responses return `200 OK`.

**Evidence:**  
`06-rate-limit.png`

**Impact:**  
Enables scraping, abuse, and denial-of-service patterns.

**Recommendation:**  
- Apply rate limiting per IP or token.
- Implement throttling at API gateway level.
- Monitor abnormal traffic.

---

### F5: Weak Input Validation

**Severity:** Low/Medium  

**Description:**  
The API accepts payloads without strict schema validation.

**Steps to Reproduce:**
1. Send malformed or oversized payloads.
2. Observe lack of strict rejection.

**Evidence:**  
Payload test screenshots.

**Impact:**  
May result in invalid data storage and potential injection risks.

**Recommendation:**  
- Enforce schema validation.
- Validate data types and length.
- Return safe error messages.

---

## 7. Remediation Plan (Prioritized)

### Immediate (High Severity)
- Enforce authentication for write operations.
- Implement authorization and role validation.

### Short-Term
- Apply rate limiting and abuse detection.
- Reduce data exposure in responses.

### Long-Term
- Integrate security testing in CI/CD pipelines.
- Implement continuous monitoring and logging.
- Conduct regular security audits.

---

## 8. Conclusion

The security assessment revealed several weaknesses that would be critical in a real-world production API. The absence of authentication and authorization represents the highest risk, followed by insufficient abuse protection and excessive data exposure.

By implementing strong access controls, validation mechanisms, and monitoring systems, the overall security posture of the API can be significantly improved.

---

## 9. Appendix

- Screenshots stored in: `/screenshots`  
- Commands and outputs stored in: `output.md`  
- Testing performed using Kali Linux terminal tools  
