## **Core components of Selenium with Python**:

---

### **1. selenium**
- **Usage**: The main package that provides the WebDriver API to automate web browsers using Python.
- **Submodules**:
  - **selenium.webdriver**: Core API for controlling web browsers.
    - **selenium.webdriver.Chrome / Firefox / Edge**: Browser-specific drivers.
    - **selenium.webdriver.common.by**: Locators to find elements (e.g., `By.ID`, `By.XPATH`).
    - **selenium.webdriver.common.keys**: Simulate keyboard inputs.
    - **selenium.webdriver.common.action_chains**: Perform complex user gestures (drag, hover, etc.).
    - **selenium.webdriver.common.alert**: Handle browser alerts, prompts, and confirmations.
    - **selenium.webdriver.support.ui**: Tools for waits (`WebDriverWait`, `Select` for dropdowns).
    - **selenium.webdriver.support.expected_conditions**: Predefined conditions for waits.
  - **selenium.common.exceptions**: All exception classes like `NoSuchElementException`, `TimeoutException`.

---

### **2. WebDriver**
- **Usage**: Main interface to launch and control the browser.
- **Examples**:
  - `webdriver.Chrome()`
  - `webdriver.Firefox()`
  - `webdriver.Edge()`

---

### **3. WebElement**
- **Usage**: Object returned by `find_element()` or `find_elements()` representing HTML elements.
- **Methods**:
  - `.click()`
  - `.send_keys()`
  - `.text`
  - `.get_attribute()`

---

### **4. Locator Strategies (`By`)**
- **Usage**: Mechanism to find elements on a webpage.
- **Types**:
  - `By.ID`
  - `By.CLASS_NAME`
  - `By.NAME`
  - `By.TAG_NAME`
  - `By.XPATH`
  - `By.CSS_SELECTOR`
  - `By.LINK_TEXT`, `By.PARTIAL_LINK_TEXT`

---

### **5. Actions (ActionChains)**
- **Usage**: Automate advanced user interactions.
- **Methods**:
  - `move_to_element()`
  - `click_and_hold()`
  - `drag_and_drop()`
  - `double_click()`
  - `context_click()` (right-click)

---

### **6. Wait Mechanisms**
- **Explicit Wait**: `WebDriverWait` with `ExpectedConditions` (e.g., `element_to_be_clickable()`).
- **Implicit Wait**: `driver.implicitly_wait(seconds)` to wait before throwing exceptions.

---

### **7. Alerts and Pop-ups**
- **Handle JavaScript Alerts**:
  - `driver.switch_to.alert.accept()`
  - `driver.switch_to.alert.dismiss()`
  - `alert.text`, `alert.send_keys()`

---

### **8. Frames and Windows**
- **Switch between contexts**:
  - `driver.switch_to.frame()`
  - `driver.switch_to.window()`
  - `driver.window_handles`, `driver.current_window_handle`

---

### **9. Headless Browsing**
- **Usage**: Run browser without UI.
- **Example**: Use `Options()` class to set `headless=True` in Chrome or Firefox.

---

### **10. Screenshots and Logs**
- **Capture State**:
  - `driver.save_screenshot("page.png")`
  - `element.screenshot("elem.png")`

---

### **11. File Downloads and Uploads**
- **Upload**: `element.send_keys("path/to/file")`
- **Download Handling**: Needs custom profile setup for Chrome/Firefox to auto-save.

---
