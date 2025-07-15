## **Browser Navigation – Selenium with Python**

Browser navigation in Selenium refers to controlling the browser history and moving between pages. The `WebDriver` provides built-in methods to simulate actions like going back, forward, refreshing, and navigating to a URL.

---

### **Overview**

- Provided by: `WebDriver` interface  
- Allows control over browser history and page reloads  
- Useful for testing multi-page flows, navigation controls, and session behaviors  

---

### **Navigation Methods in Selenium**

| Method                              | Description |
|-------------------------------------|-------------|
| `driver.get(url)`                   | Opens a new page with the given URL |
| `driver.back()`                     | Simulates browser back button |
| `driver.forward()`                  | Simulates browser forward button |
| `driver.refresh()`                  | Refreshes the current page |
| `driver.current_url`                | Returns the current page URL |
| `driver.title`                      | Returns the current page title |
| `driver.page_source`                | Returns the full HTML source of the page |

---

### **Examples**

```python
from selenium import webdriver

driver = webdriver.Chrome()

# Open a website
driver.get("https://example.com")
print(driver.title)

# Navigate to another URL
driver.get("https://www.google.com")
print(driver.current_url)

# Go back to previous page
driver.back()

# Go forward
driver.forward()

# Refresh the current page
driver.refresh()

# Print page source
print(driver.page_source)

driver.quit()
```

---

### **Use Cases**

| Scenario                                   | Method to Use         |
|--------------------------------------------|------------------------|
| Test history navigation                    | `back()`, `forward()` |
| Test page reload and state retention       | `refresh()`           |
| Validate redirection or URL changes        | `current_url`         |
| Validate dynamic titles or meta info       | `title`               |
| Extract static content                     | `page_source`         |

---

### **Waiting After Navigation**

- Use **explicit wait** to wait for elements to load after navigation:

```python
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver.get("https://example.com")
WebDriverWait(driver, 10).until(EC.presence_of_element_located((By.ID, "main")))
```

---

### **Cautions**

- `get()` is synchronous: waits for the page to fully load.
- Avoid using `time.sleep()` after navigation; prefer explicit waits.
- After `refresh()`, all WebElement references become stale. Re-locate them.

---

### **Best Practices**

- Always verify navigation success via `title` or `current_url`.
- Use navigation methods only when the application under test has client-side navigation buttons or uses multi-page flows.
- Reuse `driver.get()` for jumping to a known URL directly instead of simulating back/forward chains unless testing browser behavior.

---
