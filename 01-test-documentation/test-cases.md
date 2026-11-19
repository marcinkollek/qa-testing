# Test Cases – SauceDemo E-Commerce Application

**Application Under Test (AUT):** [SauceDemo](https://www.saucedemo.com/)  
**Test Type:** Functional, Negative, Boundary Value, End-to-End (E2E)  
**Author:** Marcin Kołłek (ISTQB® CTFL)  

---

## 1. Authentication Module

| Test ID | Title | Preconditions | Test Steps | Test Data | Expected Result | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-001** | Successful login with valid credentials | User is on the login page | 1. Enter valid username.<br>2. Enter valid password.<br>3. Click **Login**. | User: `standard_user`<br>Pass: `secret_sauce` | User is redirected to `/inventory.html` and product catalog is displayed. | ![Pass](https://img.shields.io/badge/PASS-brightgreen) |
| **TC-002** | Login attempt with locked-out user | User is on the login page | 1. Enter locked-out username.<br>2. Enter valid password.<br>3. Click **Login**. | User: `locked_out_user`<br>Pass: `secret_sauce` | Login is blocked. Error banner displays: *"Epic sadface: Sorry, this user has been locked out."* | ![Pass](https://img.shields.io/badge/PASS-brightgreen) |
| **TC-003** | Login attempt with invalid password | User is on the login page | 1. Enter valid username.<br>2. Enter incorrect password.<br>3. Click **Login**. | User: `standard_user`<br>Pass: `wrong_pass123` | Login is blocked. Error banner displays: *"Epic sadface: Username and password do not match any user in this service"* | ![Pass](https://img.shields.io/badge/PASS-brightgreen) |
| **TC-004** | Login attempt with empty fields | User is on the login page | 1. Leave Username and Password empty.<br>2. Click **Login**. | User: `""`<br>Pass: `""` | Validation triggers. Error message displays: *"Epic sadface: Username is required"* | ![Pass](https://img.shields.io/badge/PASS-brightgreen) |

---

## 2. Inventory & Sorting Module

| Test ID | Title | Preconditions | Test Steps | Test Data | Expected Result | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-005** | Sort products by Price (low to high) | User is logged in (`standard_user`) on `/inventory.html` | 1. Click the sort dropdown in the top right.<br>2. Select **Price (low to high)**. | Filter: `Price (low to high)` | Products are reordered ascending by price, starting at $7.99 (`Sauce Labs Onesie`) and ending at $49.99 (`Sauce Labs Fleece Jacket`). | ![Pass](https://img.shields.io/badge/PASS-brightgreen) |
| **TC-006** | Add and remove item from cart on product list | User is logged in on `/inventory.html` | 1. Click **Add to cart** on `Sauce Labs Backpack`.<br>2. Verify cart badge.<br>3. Click **Remove**. | Product: `Sauce Labs Backpack` | Cart badge updates to `1`, button changes to **Remove**. After clicking **Remove**, badge disappears and button reverts to **Add to cart**. | ![Pass](https://img.shields.io/badge/PASS-brightgreen) |

---

## 3. Checkout Module (Boundary & Validation Testing)

| Test ID | Title | Preconditions | Test Steps | Test Data | Expected Result | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-007** | Complete end-to-end checkout flow | User has 1 item in cart and is on `/cart.html` | 1. Click **Checkout**.<br>2. Fill First Name, Last Name, Zip/Postal Code.<br>3. Click **Continue**.<br>4. Verify summary and click **Finish**. | First Name: `Marcin`<br>Last Name: `Kollek`<br>Zip: `70-001` | Order is placed. Confirmation page displays *"Thank you for your order!"* and cart badge is cleared. | ![Pass](https://img.shields.io/badge/PASS-brightgreen) |
| **TC-008** | Checkout validation with missing Postal Code | User is on `/checkout-step-one.html` | 1. Enter First Name and Last Name.<br>2. Leave Zip/Postal Code blank.<br>3. Click **Continue**. | First Name: `Marcin`<br>Last Name: `Kollek`<br>Zip: `""` | Form submission is blocked. Error message displays: *"Error: Postal Code is required"* | ![Pass](https://img.shields.io/badge/PASS-brightgreen) |
| **TC-009** | Checkout with whitespace-only input (Boundary/Negative) | User is on `/checkout-step-one.html` | 1. Enter single spaces in First Name, Last Name, and Zip Code.<br>2. Click **Continue**. | First Name: `"   "`<br>Last Name: `"   "`<br>Zip: `"   "` | Validation rejects whitespace-only strings and displays required field error. | ![Fail](https://img.shields.io/badge/FAIL-red)<br>*(See BUG-002)* |
