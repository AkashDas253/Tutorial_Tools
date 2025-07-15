## **Waits in Selenium – Comprehensive Note**

Web elements may not be immediately available on the page due to JavaScript execution or AJAX calls. Selenium provides **waits** to handle these situations and ensure reliable test execution. Waits help synchronize your test with the state of the page.

---

### **Types of Waits**

| Wait Type        | Description |
|------------------|-------------|
| **Implicit Wait** | Waits for a certain amount of time while locating elements globally |
| **Explicit Wait** | Waits for specific conditions before proceeding |
| **Fluent Wait**   | Customizable version of explicit wait with polling and exception handling |

---

### **1. Implicit Wait**

- Applies globally for all elements.
- Selenium waits for the element to appear for the defined duration.

```python
driver.implicitly_wait(10)  # seconds
```

#### Notes:
- Applies only to `find_element` and `find_elements`.
- Once set, it remains active until the driver is closed or changed.

---

### **2. Explicit Wait**

- Waits for a **specific condition** to be met before proceeding.
- Recommended for dynamic elements and conditions.

```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.by import By

wait = WebDriverWait(driver, 10)
element = wait.until(EC.presence_of_element_located((By.ID, "username")))
```

#### Common Expected Conditions:

| Condition                             | Description |
|----------------------------------------|-------------|
| `presence_of_element_located`         | Element is in the DOM, not necessarily visible |
| `visibility_of_element_located`       | Element is visible and in the DOM |
| `element_to_be_clickable`             | Element is visible and enabled |
| `text_to_be_present_in_element`       | Specific text appears inside an element |
| `title_is`, `title_contains`          | Title matches or contains text |
| `alert_is_present`                    | Alert popup appears |
| `element_to_be_selected`              | Used for checkboxes or dropdown options |
| `frame_to_be_available_and_switch_to_it` | Wait for an iframe to load and switch to it |

---

### **3. Fluent Wait**

- Waits with fine-grained control over polling frequency and exceptions to ignore.

```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.common.exceptions import NoSuchElementException

wait = WebDriverWait(driver, timeout=10, poll_frequency=1,
                     ignored_exceptions=[NoSuchElementException])

element = wait.until(EC.visibility_of_element_located((By.ID, "email")))
```

#### Fluent Wait Features:
- Customize polling frequency (default: 500ms).
- Ignore specific exceptions (e.g., `NoSuchElementException`).
- Can be used to reduce resource usage.

---

### **Differences Between Wait Types**

| Feature             | Implicit Wait           | Explicit Wait             | Fluent Wait |
|---------------------|--------------------------|----------------------------|--------------|
| Scope               | Global                   | Specific elements/actions | Specific     |
| Condition-based     | ❌                       | ✅                         | ✅           |
| Exception handling  | ❌                       | ✅                         | ✅           |
| Polling control     | ❌                       | ❌                         | ✅           |

---

### **Best Practices**

- Prefer **explicit waits** over implicit waits for precise control.
- Avoid combining implicit and explicit waits – can cause unpredictable delays.
- Use **expected conditions** instead of `time.sleep()` for dynamic content.
- Keep polling intervals short for fast responsiveness with minimal CPU impact.
- Always handle possible `TimeoutException` using `try-except`.

---

### **Example with Multiple Waits**

```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.by import By

driver.get("https://example.com")

try:
    WebDriverWait(driver, 15).until(EC.presence_of_element_located((By.ID, "login")))
    print("Login field is ready.")
except TimeoutException:
    print("Login field did not load in time.")
```

---
