# FUTURE_CS_3 – API Security Risk Analysis

## 📌 Project Overview
This project presents a comprehensive API Security Risk Analysis conducted on a public demo REST API.  
The objective of this task is to identify common security weaknesses in APIs and propose effective mitigation strategies.

The assessment focuses on evaluating authentication, authorization, data exposure, input validation, and abuse prevention mechanisms.  
All testing was performed in a controlled and ethical manner using publicly available demo APIs.

This project was completed as part of the SkillCraft Technology Internship Program.

---

## 🎯 Objectives
The main objectives of this project are:

- To analyze API endpoints for security vulnerabilities
- To evaluate authentication and authorization mechanisms
- To identify risks related to data exposure and improper access controls
- To examine input validation and error handling practices
- To observe rate limiting and abuse protection mechanisms
- To document findings with impact analysis and remediation strategies

---

## 🖥 Environment and Tools
The following environment and tools were used:

- **Operating System:** Kali Linux  
- **Programming Language:** Python (for testing scripts, optional)  
- **API Testing Tools:** Postman / Insomnia  
- **Browser Tools:** Developer Tools  
- **Version Control:** Git and GitHub (SSH authentication)

---

## 🌐 Target API
A publicly available demo API was used for this assessment.

- **API Name:** JSONPlaceholder  
- **Base URL:** https://jsonplaceholder.typicode.com  
- **Purpose:** Testing and educational use only  

> Note: This API does not contain real user data and is intended for learning purposes.

---

## 🔍 Scope of Testing

### Included in Scope
- Endpoint discovery and enumeration
- HTTP method testing (GET, POST, PUT, PATCH, DELETE)
- Authentication and authorization checks
- Data exposure analysis
- Input validation and error handling review
- Rate limiting observation

### Excluded from Scope
- Exploiting vulnerabilities
- Attacking infrastructure
- Accessing private or confidential systems
- Performing denial-of-service attacks

---

## 🧪 Testing Methodology
The security assessment followed a structured methodology:

1. **Endpoint Analysis**
   - Identification of available API endpoints
   - Review of allowed HTTP methods

2. **Authentication Assessment**
   - Verification of token or key requirements
   - Testing access without credentials

3. **Authorization Review**
   - Analysis of privilege separation
   - Evaluation of object-level and function-level access

4. **Data Exposure Review**
   - Inspection of API responses
   - Identification of unnecessary fields

5. **Input Validation Testing**
   - Submission of unexpected or malformed inputs
   - Observation of server responses

6. **Rate Limiting Observation**
   - Repeated request testing
   - Analysis of throttling behavior

7. **Documentation of Findings**
   - Collection of evidence
   - Severity classification
   - Recommendation formulation

---

## 📂 Project Structure

FUTURE_CS_3
│
├── REPORT.md # Detailed security analysis report
├── README.md # Project documentation
├── screenshots/ # Evidence screenshots
│ ├── 01-get-posts.png
│ ├── 02-get-users.png
│ └── ...
├── postman/ # Optional Postman collections
│ └── collection.json


---

## ▶ How to Use This Repository

1. Clone the repository:
   ```bash
   git clone git@github.com:YOUR_USERNAME/FUTURE_CS_3.git


Navigate to the project directory:

cd FUTURE_CS_3


Read the full analysis report:

cat REPORT.md


Review evidence in the screenshots folder.

Import Postman collection (if available) for request testing.
