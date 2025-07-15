## **Explicit Waits – Selenium with Python**

Explicit Waits in Selenium are used to wait for a certain condition to occur before proceeding with the next step. Unlike **Implicit Waits**, which are applied globally to all element searches, **Explicit Waits** allow you to wait for specific elements to satisfy a condition, offering more control and flexibility over the waiting process.

---

### **Overview**

- **Explicit Wait** is used for waiting for specific conditions to be met before proceeding with the next step in the test.
- You define a condition, such as waiting for an element to become clickable, visible, or present in the DOM.
- **WebDriverWait** is the core utility for implementing Explicit Waits in Selenium.

---

### **Setting Explicit Wait**

To use an explicit wait in Selenium, we need to use the `WebDriverWait` class, along with an **Expected Condition** that defines the condition to wait for.

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

# Initialize WebDriver
driver = webdriver.Chrome()

# Open a website
driver.get("https://example.com")

# Set an explicit wait for an element to be visible
wait = WebDriverWait(driver, 10)  # 10 seconds timeout
element = wait.until(EC.visibility_of_element_located((By.ID, "element_id")))
```

- **`WebDriverWait(driver, timeout)`**: Initializes the wait with a specified timeout (in seconds).
- **`until(condition)`**: Waits until the given condition is met.

---

### **Common Expected Conditions**

Selenium provides various **Expected Conditions** to use with **Explicit Waits**:

| Expected Condition                          | Description |
|---------------------------------------------|-------------|
| `presence_of_element_located(locator)`     | Wait until the element is in the DOM (not necessarily visible) |
| `visibility_of_element_located(locator)`   | Wait until the element is visible (displayed on the page) |
| `element_to_be_clickable(locator)`         | Wait until the element is clickable (visible and enabled) |
| `text_to_be_present_in_element(locator, text)` | Wait for a specific text to appear inside an element |
| `title_contains(title)`                    | Wait for the page title to contain a specific string |
| `alert_is_present()`                        | Wait for an alert to appear on the page |
| `frame_to_be_available_and_switch_to_it(locator)` | Wait for a frame to be available and switch to it |
| `element_to_be_selected(locator)`          | Wait for a checkbox or dropdown option to be selected |
| `staleness_of(element)`                    | Wait for an element to be removed from the DOM |
| `visibility_of_all_elements_located(locator)` | Wait for multiple elements to be visible |

---

### **Example of Explicit Wait with Expected Conditions**

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

# Initialize WebDriver
driver = webdriver.Chrome()

# Navigate to the webpage
driver.get("https://example.com")

# Set explicit wait
wait = WebDriverWait(driver, 10)

# Wait until the element is visible
element = wait.until(EC.visibility_of_element_located((By.ID, "login_button")))

# Click the element once it's visible
element.click()

# Quit the driver
driver.quit()
```

In this example, the script waits until the element with ID `"login_button"` is visible on the page. After the condition is met, it clicks the button.

---

### **Best Practices for Using Explicit Waits**

- **Use with Specific Elements**: Explicit waits are best used when you need to wait for a specific condition related to a particular element (e.g., visibility or clickability).
- **Avoid Unnecessary Waits**: Do not use explicit waits if the element is already immediately available or if it can be handled with implicit waits.
- **Timeout Handling**: Explicit waits are ideal when you need to wait for longer periods, such as when waiting for AJAX calls to complete or elements to load after JavaScript execution.
- **Use Expected Conditions**: Selenium provides many built-in expected conditions that simplify the use of explicit waits. Use them instead of manually checking conditions.

---

### **Combining Explicit and Implicit Waits**

- It is generally **not recommended** to use **Explicit Waits** and **Implicit Waits** together, as they can interfere with each other, leading to unexpected delays.
- If you use both, implicit waits might introduce unnecessary delays even when the explicit wait condition is already satisfied.

---

### **Example with TimeoutException Handling**

When the explicit wait exceeds the given time without meeting the condition, a `TimeoutException` is raised. It’s useful to handle such exceptions gracefully:

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.common.exceptions import TimeoutException

# Initialize WebDriver
driver = webdriver.Chrome()

# Open a webpage
driver.get("https://example.com")

try:
    # Set explicit wait for an element to be clickable
    element = WebDriverWait(driver, 10).until(EC.element_to_be_clickable((By.ID, "submit_button")))
    element.click()
except TimeoutException:
    print("Element was not clickable in time.")

# Quit the driver
driver.quit()
```

In this example, if the element is not clickable within 10 seconds, a `TimeoutException` is caught and a message is printed.

---

### **Summary**

- **Explicit Waits** are used to wait for specific conditions (such as visibility, presence, or clickability) to be met before performing an action.
- They provide more control than **Implicit Waits** and are best suited for dynamic content or complex page interactions.
- **WebDriverWait** and **Expected Conditions** are key components for implementing Explicit Waits.
- Explicit Waits should be used when you need fine-grained control over the wait conditions, while **Implicit Waits** should be used for simpler scenarios.

---
