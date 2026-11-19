# Bug Reports – SauceDemo Application

---

## BUG-001: Broken product images displayed for `problem_user` on the Inventory page

* **Status:** Open
* **Severity:** Major
* **Priority:** High
* **Environment:** Windows 11, Google Chrome (latest, Nov 2026), Desktop 1440p (2560x1440)
* **Test Account:** `problem_user` / `secret_sauce`

### Description
After logging in with the `problem_user` account, all product thumbnails on the inventory page display the exact same placeholder image (a dog photo) instead of the actual product images.

### Steps to Reproduce
1. Navigate to [https://www.saucedemo.com/](https://www.saucedemo.com/).
2. Enter `problem_user` in the **Username** field.
3. Enter `secret_sauce` in the **Password** field.
4. Click the **Login** button.
5. Observe the product cards on [https://www.saucedemo.com/inventory.html](https://www.saucedemo.com/inventory.html).

### Expected Result
Each product card should display its corresponding product image (e.g., backpack, bike light, t-shirt).

### Actual Result
All 6 product cards display the identical incorrect image ([https://https://www.saucedemo.com/assets/sl-404-Cq1a9k9X.jpg](https://www.saucedemo.com/assets/sl-404-Cq1a9k9X.jpg)).

---

## BUG-002: Checkout form accepts whitespace-only strings in required fields

* **Status:** Open
* **Severity:** Minor
* **Priority:** Medium
* **Environment:** Windows 11, Google Chrome (latest, Nov 2026), Desktop 1440p (2560x1440)
* **Test Account:** `standard_user` / `secret_sauce`
* **Related Test Case:** `TC-009`

### Description
The Checkout Information form (`Checkout: Your Information`) validates whether input fields are empty, but fails to trim leading/trailing spaces. Entering only spaces allows the user to proceed to the order overview without providing valid shipping details.

### Steps to Reproduce
1. Log in as `standard_user` on [https://www.saucedemo.com/](https://www.saucedemo.com/).
2. Add any item to the cart and navigate to [https://www.saucedemo.com/cart.html](https://www.saucedemo.com/cart.html).
3. Click **Checkout**.
4. Enter `"   "` (three spaces) into **First Name**, **Last Name**, and **Zip/Postal Code**.
5. Click **Continue**.

### Expected Result
Input should be trimmed, and validation should block progression with an error message (*"Error: First Name is required"*).

### Actual Result
The form accepts whitespace-only values and redirects the user to [https://www.saucedemo.com/checkout-step-two.html](https://www.saucedemo.com/checkout-step-two.html).

---

## BUG-003: Product sorting filter does not reorder items for `problem_user`

* **Status:** Open
* **Severity:** Major
* **Priority:** Medium
* **Environment:** Windows 11, Google Chrome (latest, Nov 2026), Desktop 1440p (2560x1440)
* **Test Account:** `problem_user` / `secret_sauce`

### Description
Selecting any sorting option from the product filter dropdown (e.g., *Price (low to high)* or *Name (Z to A)*) has no effect on the order of displayed products.

### Steps to Reproduce
1. Log in as `problem_user` on [https://www.saucedemo.com/](https://www.saucedemo.com/).
2. Click the sorting dropdown menu in the top-right corner of [https://www.saucedemo.com/inventory.html](https://www.saucedemo.com/inventory.html).
3. Select **Price (low to high)**.

### Expected Result
Products are sorted by price in ascending order ($7.99 to $49.99).

### Actual Result
The product order remains unchanged (default A-Z order), even though the dropdown label updates.
