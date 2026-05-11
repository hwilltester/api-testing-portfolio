# 🔌 Fintech API Testing - Postman Portfolio Project

> API test collection simulating core banking scenarios - Auth, User Account, Fund Transfer, and Loan Application.
> Built with Postman · JavaScript test scripts · No API key required

---

## 📌 What This Project Tests

This collection covers 4 main flows that are common in any banking or fintech API:

- **Auth** - login with valid and invalid credentials, JWT token validation
- **User Account** - fetch account details, handle non-existent accounts
- **Fund Transfer** - create transfer, verify it was saved, test invalid IDs
- **Loan Application** - submit loan, test missing fields, test unauthorized access

The base URL is **dummyjson.com** - a free public REST API that supports real JWT authentication. No API key needed, no account required.

The test logic (status codes, response fields, negative cases, security checks) reflects what I tested professionally at Yoma Bank across mobile banking and loan origination systems.

---

## 📁 Folder Structure

```
fintech-api-testing/
│
├── collections/
│   └── fintech_banking_api_v2.json   ← import this into Postman
│
├── reports/
│   └── postman-run-results.png       ← screenshot of actual test run
│
└── README.md
```

---

## ⚙️ How To Run

### Option 1 - Postman (manual)

1. Open Postman
2. Click **Import**
3. Choose `collections/fintech_banking_api_v2.json`
4. Click **Run collection**

No environment setup needed - the collection handles token automatically.

---

### Option 2 - Newman (command line)

Install Newman:
```
npm install -g newman
npm install -g newman-reporter-htmlextra
```

Run the collection:
```
newman run collections/fintech_banking_api_v2.json -r htmlextra --reporter-htmlextra-export reports/newman-report.html
```

Then open `reports/newman-report.html` in your browser.

---

## 🧪 Test Cases Summary

| # | Folder | Test Name | Type |
|---|--------|-----------|------|
| 1 | Auth | Login with valid credentials | Positive |
| 2 | Auth | Login with wrong password | Negative |
| 3 | Auth | Login with empty username | Negative |
| 4 | Auth | Verify token - get current user | Positive |
| 5 | Auth | Verify token - invalid token | Security |
| 6 | User Account | Get account details | Positive |
| 7 | User Account | Get account - invalid user ID | Negative |
| 8 | Fund Transfer | Create successful transfer | Positive |
| 9 | Fund Transfer | Get transaction by ID | Positive |
| 10 | Fund Transfer | Invalid transaction ID | Negative |
| 11 | Loan Application | Submit valid application | Positive |
| 12 | Loan Application | Missing required field | Negative |
| 13 | Loan Application | Unauthorized - no token | Security |

---

## 🧠 What I Focused On

**Negative and security cases are the priority.**
In banking, the happy path usually works fine out of the box. What breaks things is edge cases - expired tokens, missing required fields, accessing resources that don't exist. That's where I spent most of my testing time at Yoma Bank, and I followed the same mindset here.

**Token flow is automatic.**
The login request saves the JWT token as a collection variable. All subsequent requests pick it up automatically - no manual copy-paste needed between requests.

**Every request has test scripts.**
Not just status code checks - I also verify response body fields, data types, and that no sensitive data leaks on failed requests.

**Production behavior is documented.**
For cases where the mock API behaves differently from a real banking API, I added `[Expected in production]` comments in the test scripts. This shows I understand real-world requirements, not just what the mock returns.

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| Postman | Build and run API tests |
| Newman | Run collection from command line |
| newman-reporter-htmlextra | Generate HTML report |
| dummyjson.com | Free public REST API with real JWT auth |
| JavaScript | Test scripts inside Postman |

---

## 🔗 Related Projects

| Project | Link |
|---------|------|
| UI Automation (Robot Framework) | [OrangeHRM_Automation](https://github.com/hwilltester/OrangeHRM_Automation) |
| Banking UAT Test Cases + RTM | [banking-uat-portfolio](https://github.com/hwilltester/banking-uat-portfolio) |
| Banking SQL Test Scripts | [banking-sql-scripts](https://github.com/hwilltester/banking-sql-scripts) |

---

## 🙋 Author

**Htuu Will Oo** - QA Engineer with 7+ years in banking and fintech

[GitHub](https://github.com/hwilltester) · [LinkedIn](https://linkedin.com/in/htuuwill)
