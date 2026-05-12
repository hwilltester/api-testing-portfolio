# 🔌 API Testing Portfolio - Postman & Newman

> REST API test collection covering full booking lifecycle - Auth, Create, Read, Update, Delete, and Filter.
> Built with Postman · JavaScript test scripts · No API key required · All tests pass ✅

---

## 📌 About This Project

This project demonstrates my API testing skills using **restful-booker.herokuapp.com** - a public REST API built specifically for testing practice by QA engineer Mark Winteringham.

It covers the full lifecycle of a record from creation to deletion, with authentication required at every sensitive step.

**What I was testing for:**
- Does auth actually protect update and delete operations?
- Is the data saved correctly after a create?
- Does the API handle invalid input cleanly - no crashes, correct error codes?
- After a delete, is the record actually gone?

These are the same questions I ask when testing any system, whether it's a hotel booking API or an enterprise application.

---

## 📁 Folder Structure

```
api-testing-portfolio/
│
├── collections/
│   └── api_testing_portfolio.json    ← import this into Postman
│
├── reports/
│   └── postman-run-results.png       ← screenshot of actual test run
│
└── README.md
```

---

## ⚙️ How To Run

### Option 1 - Postman

1. Open Postman
2. Click **Import**
3. Choose `collections/api_testing_portfolio.json`
4. Click **Run collection**

Run requests in order - the auth token and booking ID are saved automatically between requests.

---

### Option 2 - Newman (command line)

```
npm install -g newman newman-reporter-htmlextra

newman run collections/api_testing_portfolio.json \
  -r htmlextra \
  --reporter-htmlextra-export reports/newman-report.html
```

---

## 🧪 Test Cases Summary

| # | Test Name | Type | Expected Result |
|---|-----------|------|----------------|
| 1 | Create Token - Valid Credentials | Positive | 200 + token |
| 2 | Create Token - Wrong Password | Negative | 200 + Bad credentials, no token |
| 3 | Get All Bookings | Positive | 200 + non-empty array |
| 4 | Create New Booking | Positive | 200 + booking ID + correct data |
| 5 | Get Booking by ID | Positive | 200 + saved data matches |
| 6 | Update Booking - With Auth | Positive | 200 + updated data |
| 7 | Update Booking - Without Auth | Security | 403 Forbidden |
| 8 | Get Booking - Non-Existent ID | Negative | 404 Not Found |
| 9 | Filter Bookings by Name | Positive | 200 + filtered results |
| 10 | Delete Booking - With Auth | Positive | 201 Deleted |
| 11 | Verify Booking Deleted | Negative | 404 - record gone |

---

## 🧠 Testing Approach

**Full lifecycle - not just happy path.**
I test create, read, update, delete, and then verify the delete actually worked. A lot of bugs hide in the last step - systems that say "Deleted" but still return the record on a GET request.

**Auth checks on every sensitive operation.**
I always test what happens when auth is missing or wrong. The update-without-auth test catches a common developer mistake - forgetting to protect PUT and DELETE endpoints.

**Post-action verification.**
After creating a record, I fetch it and compare the response to what I submitted. After deleting, I GET it again to confirm it's gone. The API response alone is not enough evidence.

**Clean negative cases.**
Wrong credentials, non-existent IDs - these must return proper error codes and not crash the server. A 500 on bad input is always a bug.

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| Postman | Build and run API tests |
| Newman | Run collection from command line |
| newman-reporter-htmlextra | Generate HTML test report |
| restful-booker.herokuapp.com | Public REST API for testing practice |
| JavaScript | Test scripts inside Postman |

---

## 🔗 Other Projects

| Project | Link |
|---------|------|
| UI Automation (Robot Framework) | [OrangeHRM_Automation](https://github.com/hwilltester/OrangeHRM_Automation) |
| Banking UAT Test Cases + RTM | [banking-uat-portfolio](https://github.com/hwilltester/banking-uat-portfolio) |
| SQL Test Scripts | [banking-sql-scripts](https://github.com/hwilltester/banking-sql-scripts) |

---

## 🙋 Author

**Will**

[GitHub](https://github.com/hwilltester) · [LinkedIn](https://linkedin.com/in/htuuwill)
