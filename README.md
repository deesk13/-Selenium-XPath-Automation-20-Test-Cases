# Selenium XPath Automation – 20 Test Cases

## Project Overview

This project demonstrates web automation and XPath techniques using Selenium with Python.

The automation uses the Selenium Web Form as a real-life student registration form scenario.

Website:
https://www.selenium.dev/selenium/web/web-form.html

The project contains 20 test cases covering different XPath concepts and Selenium operations.

---

## Real-Life Scenario

Consider an online college student registration system.

A student needs to:

1. Enter student name
2. Enter password
3. Enter additional information
4. Select a dropdown option
5. Select a checkbox
6. Select a radio button
7. Submit the registration form
8. Verify successful registration

Selenium automates this entire process and verifies that the expected elements and results are available.

---

## Technologies Used

- Python
- Selenium WebDriver
- XPath
- Google Chrome
- ChromeDriver

---

## XPath Concepts Covered

| Test Case | Description | XPath / Selenium Concept |
|-----------|-------------|--------------------------|
| TC01 | Open registration page | `get()` |
| TC02 | Locate username | Attribute XPath |
| TC03 | Enter password | Attribute XPath |
| TC04 | Locate Submit button | `text()` |
| TC05 | Locate textbox dynamically | `contains()` |
| TC06 | Locate element using prefix | `starts-with()` |
| TC07 | Find input using two attributes | `and` |
| TC08 | Find element using alternatives | `or` |
| TC09 | Find immediate parent | `parent` |
| TC10 | Find form from input | `ancestor` |
| TC11 | Find child input | `child` |
| TC12 | Find next element | `following` |
| TC13 | Find checkbox | Attribute XPath |
| TC14 | Find radio button | Attribute XPath |
| TC15 | Select dropdown | XPath + `Select` |
| TC16 | Find second textbox | XPath Index |
| TC17 | Verify submitted message | `text()` |
| TC18 | Find all input fields | `find_elements()` |
| TC19 | Find dynamic element | `contains()` |
| TC20 | Complete registration | Multiple XPath concepts |

---

## Project Structure

```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait, Select
from selenium.webdriver.support import expected_conditions as EC


URL = "https://www.selenium.dev/selenium/web/web-form.html"


def start_driver():
    driver = webdriver.Chrome()
    driver.maximize_window()
    driver.get(URL)

    WebDriverWait(driver, 10).until(
        EC.presence_of_element_located((By.TAG_NAME, "form"))
    )

    return driver


def run_test(tc_number, test_function):
    driver = None

    try:
        driver = start_driver()
        test_function(driver)

        print(f"TC{tc_number:02d} - PASS")
        return True

    except Exception as e:
        print(f"TC{tc_number:02d} - FAIL")
        print(f"       Reason: {e}")
        return False

    finally:
        if driver:
            driver.quit()


# ============================================================
# TC01 - Open Student Registration Page
# Concept: get()
# ============================================================

def tc01(driver):

    assert "web-form" in driver.current_url


# ============================================================
# TC02 - Locate Username
# Concept: Attribute XPath
# ============================================================

def tc02(driver):

    username = driver.find_element(
        By.XPATH,
        "//input[@name='my-text']"
    )

    assert username.is_displayed()


# ============================================================
# TC03 - Enter Password
# Concept: Attribute XPath
# ============================================================

def tc03(driver):

    password = driver.find_element(
        By.XPATH,
        "//input[@name='my-password']"
    )

    password.send_keys("Test@123")

    assert password.get_attribute("value") == "Test@123"


# ============================================================
# TC04 - Locate Submit Button
# Concept: text()
# ============================================================

def tc04(driver):

    submit = driver.find_element(
        By.XPATH,
        "//button[text()='Submit']"
    )

    assert submit.is_displayed()


# ============================================================
# TC05 - Locate Textbox Dynamically
# Concept: contains()
# ============================================================

def tc05(driver):

    element = driver.find_element(
        By.XPATH,
        "//input[contains(@name, 'my-text')]"
    )

    assert element.is_displayed()


# ============================================================
# TC06 - Locate Element Using Prefix
# Concept: starts-with()
# ============================================================

def tc06(driver):

    element = driver.find_element(
        By.XPATH,
        "//input[starts-with(@name, 'my')]"
    )

    assert element.is_displayed()


# ============================================================
# TC07 - Find Input Using Two Attributes
# Concept: and
# ============================================================

def tc07(driver):

    element = driver.find_element(
        By.XPATH,
        "//input[@name='my-text' and @type='text']"
    )

    assert element.is_displayed()


# ============================================================
# TC08 - Find Element Using Alternatives
# Concept: or
# ============================================================

def tc08(driver):

    element = driver.find_element(
        By.XPATH,
        "//input[@name='my-text' or @name='my-password']"
    )

    assert element.is_displayed()


# ============================================================
# TC09 - Find Immediate Parent
# Concept: parent
# ============================================================

def tc09(driver):

    parent = driver.find_element(
        By.XPATH,
        "//input[@name='my-text']/parent::*"
    )

    assert parent.tag_name == "label"


# ============================================================
# TC10 - Find Form From Input
# Concept: ancestor
# ============================================================

def tc10(driver):

    form = driver.find_element(
        By.XPATH,
        "//input[@name='my-text']/ancestor::form"
    )

    assert form.tag_name == "form"


# ============================================================
# TC11 - Find Child Input
# Concept: child
# ============================================================

def tc11(driver):

    child_inputs = driver.find_elements(
        By.XPATH,
        "//label/child::input"
    )

    assert len(child_inputs) > 0


# ============================================================
# TC12 - Find Next Element
# Concept: following
# ============================================================

def tc12(driver):

    following = driver.find_elements(
        By.XPATH,
        "//input[@name='my-text']/following::input[1]"
    )

    assert len(following) > 0


# ============================================================
# TC13 - Find Checkbox
# Concept: Attribute XPath
# ============================================================

def tc13(driver):

    checkbox = driver.find_element(
        By.XPATH,
        "//input[@type='checkbox']"
    )

    checkbox.click()

    assert checkbox.is_selected()


# ============================================================
# TC14 - Find Radio Button
# Concept: Attribute XPath
# ============================================================

def tc14(driver):

    radio = driver.find_element(
        By.XPATH,
        "//input[@type='radio']"
    )

    radio.click()

    assert radio.is_selected()


# ============================================================
# TC15 - Select Dropdown
# Concept: XPath + Select
# ============================================================

def tc15(driver):

    dropdown = driver.find_element(
        By.XPATH,
        "//select[@name='my-select']"
    )

    select = Select(dropdown)
    select.select_by_visible_text("Two")

    assert select.first_selected_option.text == "Two"


# ============================================================
# TC16 - Find Second Textbox
# Concept: XPath Index
# ============================================================

def tc16(driver):

    textboxes = driver.find_elements(
        By.XPATH,
        "//input[@type='text']"
    )

    assert len(textboxes) >= 2

    second_textbox = driver.find_element(
        By.XPATH,
        "(//input[@type='text'])[2]"
    )

    assert second_textbox.is_displayed()


# ============================================================
# TC17 - Verify Submitted Message
# Concept: text()
# ============================================================

def tc17(driver):

    username = driver.find_element(
        By.XPATH,
        "//input[@name='my-text']"
    )

    username.send_keys("Deva")

    password = driver.find_element(
        By.XPATH,
        "//input[@name='my-password']"
    )

    password.send_keys("Test@123")

    submit = driver.find_element(
        By.XPATH,
        "//button[text()='Submit']"
    )

    submit.click()

    message = WebDriverWait(driver, 10).until(
        EC.visibility_of_element_located(
            (By.XPATH, "//h1[text()='Form submitted']")
        )
    )

    assert message.text == "Form submitted"


# ============================================================
# TC18 - Find All Input Fields
# Concept: find_elements()
# ============================================================

def tc18(driver):

    inputs = driver.find_elements(
        By.XPATH,
        "//input"
    )

    assert len(inputs) > 0


# ============================================================
# TC19 - Find Dynamic Element
# Concept: contains()
# ============================================================

def tc19(driver):

    elements = driver.find_elements(
        By.XPATH,
        "//*[contains(@class, 'form')]"
    )

    assert len(elements) > 0


# ============================================================
# TC20 - Complete Student Registration Automation
# Concept: Multiple XPath Concepts
# ============================================================

def tc20(driver):

    # Student Name
    username = driver.find_element(
        By.XPATH,
        "//input[@name='my-text']"
    )

    username.send_keys("Deva")

    # Password
    password = driver.find_element(
        By.XPATH,
        "//input[@name='my-password']"
    )

    password.send_keys("Test@123")

    # Additional Information
    textarea = driver.find_element(
        By.XPATH,
        "//textarea[@name='my-textarea']"
    )

    textarea.send_keys("AI and ML Student")

    # Dropdown
    dropdown = driver.find_element(
        By.XPATH,
        "//select[@name='my-select']"
    )

    Select(dropdown).select_by_visible_text("Two")

    # Checkbox
    checkbox = driver.find_element(
        By.XPATH,
        "//input[@type='checkbox']"
    )

    if not checkbox.is_selected():
        checkbox.click()

    assert checkbox.is_selected()

    # Radio Button
    radio = driver.find_element(
        By.XPATH,
        "//input[@type='radio']"
    )

    if not radio.is_selected():
        radio.click()

    assert radio.is_selected()

    # Submit
    submit = driver.find_element(
        By.XPATH,
        "//button[text()='Submit']"
    )

    submit.click()

    # Verify successful submission
    success_message = WebDriverWait(driver, 10).until(
        EC.visibility_of_element_located(
            (By.XPATH, "//h1[text()='Form submitted']")
        )
    )

    assert success_message.text == "Form submitted"


# ============================================================
# MAIN EXECUTION
# ============================================================

if __name__ == "__main__":

    print()
    print("==========================================")
    print(" SELENIUM XPATH - 20 TEST CASES")
    print(" Student Registration Automation")
    print("==========================================")
    print()

    test_cases = [
        ("01", tc01),
        ("02", tc02),
        ("03", tc03),
        ("04", tc04),
        ("05", tc05),
        ("06", tc06),
        ("07", tc07),
        ("08", tc08),
        ("09", tc09),
        ("10", tc10),
        ("11", tc11),
        ("12", tc12),
        ("13", tc13),
        ("14", tc14),
        ("15", tc15),
        ("16", tc16),
        ("17", tc17),
        ("18", tc18),
        ("19", tc19),
        ("20", tc20),
    ]

    passed = 0
    failed = 0

    for number, test in test_cases:

        if run_test(number, test):
            passed += 1
        else:
            failed += 1

    print()
    print("==========================================")
    print(" TEST EXECUTION SUMMARY")
    print("==========================================")
    print(f"Total Test Cases : {len(test_cases)}")
    print(f"Passed           : {passed}")
    print(f"Failed           : {failed}")

    if failed == 0:
        print()
        print("ALL 20 TEST CASES PASSED")
    else:
        print()
        print("SOME TEST CASES FAILED")

    print("=========================================="
```
## output:
<img width="637" height="501" alt="image" src="https://github.com/user-attachments/assets/bbf978a7-af80-4a9d-a1d9-66245bd2fbba" />
<img width="1917" height="941" alt="image" src="https://github.com/user-attachments/assets/004f2952-a739-4852-a5bd-92d8e45de0ca" />
<img width="1917" height="877" alt="image" src="https://github.com/user-attachments/assets/748aec79-6509-4f6f-8e6b-81862846fe5c" />


