# API Testing – Restful-Booker (Postman)

**Base URL:** `https://restful-booker.herokuapp.com`  
**API Documentation:** [Restful-Booker API Docs](https://restful-booker.herokuapp.com/apidoc/index.html)  
**Tool:** Postman   

---

## 📋 Overview

This folder contains an exported Postman collection covering end-to-end REST API testing for a hotel booking service (**Restful-Booker**). The test suite validates authentication, CRUD operations (`GET`, `POST`, `PUT`, `DELETE`), HTTP status codes, response payloads, and negative scenarios.

---

## 🧪 Covered Scenarios & Assertions

| # | Method | Endpoint | Scenario | Automated Postman Assertions |
| :--- | :--- | :--- | :--- | :--- |
| **1** | `POST` | `/auth` | Generate authentication token with valid admin credentials | • Status code is `200 OK`<br>• Response contains non-empty `token` string<br>• Saves token to collection variable `{{auth_token}}` |
| **2** | `POST` | `/booking` | Create a new booking with valid JSON payload | • Status code is `200 OK`<br>• Response includes `bookingid`<br>• Returned `firstname`, `lastname`, and `totalprice` match request data<br>• Saves ID to `{{booking_id}}` |
| **3** | `GET` | `/booking/{{booking_id}}` | Retrieve details of the newly created booking | • Status code is `200 OK`<br>• Response time is under 1500ms<br>• Content-Type header is `application/json` |
| **4** | `PUT` | `/booking/{{booking_id}}` | Update an existing booking using `Cookie: token={{auth_token}}` | • Status code is `200 OK`<br>• Updated `totalprice` and `additionalneeds` are reflected in response |
| **5** | `DELETE` | `/booking/{{booking_id}}` | Delete the booking using valid auth token | • Status code is `201 Created` |
| **6** | `GET` | `/booking/{{booking_id}}` | Verify deleted booking no longer exists (Negative check) | • Status code is `404 Not Found` |

---

## 🚀 How to Run the Collection

1. Download [`restful-booker-collection.json`](./restful-booker-collection.json) from this folder.
2. Open **Postman** and click **Import** (top-left).
3. Select the downloaded `.json` file.
4. Open the imported collection **Restful-Booker API Tests** and click **Run** (Collection Runner) to execute all 6 requests sequentially with automated test assertions.
