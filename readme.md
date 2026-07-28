# QA Automation Project - Agustina Rodriguez

## Description

Functional test automation project built with Python, Selenium WebDriver, and Pytest.

The tests cover the main flows of the Swag Labs web application: login, inventory viewing, and shopping cart management.

The project implements the Page Object Model (POM) pattern and different automation approaches, including Data-Driven Testing using CSV and JSON files, HTML report generation, logging, automatic screenshots on failure, and BDD testing using Gherkin and Behave. It also includes REST API testing with Requests and Behave as a complementary practice.

## Technologies used
- Python
- Selenium WebDriver
- Pytest
- Behave
- Gherkin
- Pytest HTML
- Logging
- CSV and JSON (Data-Driven Testing)
- Google Chrome + ChromeDriver
- Git
- GitHub Actions (CI/CD)
- Requests

## CI/CD

The project uses GitHub Actions to automatically run the tests on every push or pull request to the main branch.

The workflow runs the tests with Pytest on an Ubuntu environment with Chrome in headless mode, and generates an HTML report as a downloadable artifact from the GitHub Actions tab.

## Installation
`git clone https://github.com/Agusrodriguezx/Proyecto_final.git
cd Proyecto_final`


## Installing Dependencies
pip install -r requirements.txt


## Running tests

### With Pytest
```
pytest
```

### With Behave
```
python3 -m behave
```

## Generate HTML report
pytest --html=report.html --self-contained-html


## How the tests work

### test_login.py — Authentication tests

- `test_login_ok`
    - Verifies that the user is correctly redirected to the inventory page after logging in.

- `test_login_invalid_password`
    - Verifies that the corresponding error message is displayed when an invalid password is entered.

- Implements logging to record test execution.
- Generates HTML reports using pytest-html.
- Automatically captures a screenshot on failure.

---

### test_login_csv.py — Automation tests with parameterized data

- Implements Data-Driven Testing using `pytest.mark.parametrize()`.

- Uses external data stored in `data/users.csv`.

- Reads test data through `utils/data_reader.py`.

- Runs multiple authentication scenarios using a single test case.

- Validates both positive and negative scenarios:
    - Valid credentials → successful access to the inventory.
    - Invalid credentials → the corresponding error message is displayed.

---

### login.feature — BDD tests with Gherkin and Behave

- Implements authentication scenarios using Gherkin syntax.

- Defines positive and negative login scenarios.

- Uses 'Scenario Outline' to run multiple data sets.

- Separates the scenario descriptions from their implementation in 'login_steps.py'.

---

### login_steps.py

- Implements the steps defined in `login.feature`.

- Reuses the `LoginPage` class to interact with the application.

---

### environment.py

- Configures and manages the WebDriver for tests run with Behave.

---

### test_inventory.py — Inventory tests

- `test_inventory_title`
    - Verifies that the page title is "Swag Labs".

- `test_productos_visibles`
    - Verifies that at least one product is visible in the inventory.

- `test_ui_elements`
    - Verifies the presence of the hamburger menu and the product filter.

---

### test_cart.py — Cart tests

- `test_cart`
    - Adds a product to the cart.
    - Verifies the cart counter is updated.
    - Navigates to the cart.
    - Checks that the added product is the expected one.

---

### test_cart_json.py — Cart tests with external data

- Implements Data-Driven Testing using a JSON file.
- Uses data stored in `data/products.json`.
- Reads test data through `utils/data_reader.py`.
- Adds multiple products to the cart using data external to the test.
- Navigates to the cart and validates that the added products match those defined in the JSON file.
- Verifies both the name and price of each product.


## Design pattern used

### Page Object Model (POM)
The Page Object Model pattern was implemented to separate each page's elements and actions from the validations performed in the tests.

Pages are represented through independent classes:
- LoginPage
- InventoryPage
- CartPage

This improves code reuse and makes it easier to maintain the automated tests.
