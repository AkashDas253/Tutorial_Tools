## **Selenium for Python – All Concepts and Subconcepts**

### **Introduction to Selenium**
- What is Selenium?
- Features of Selenium
- Limitations of Selenium
- Components of Selenium
  - Selenium WebDriver
  - Selenium IDE
  - Selenium Grid

---

### **Setup and Environment**
- Installing Selenium (`pip install selenium`)
- WebDrivers
  - ChromeDriver
  - GeckoDriver (Firefox)
  - EdgeDriver
  - SafariDriver
- Setting PATH for WebDriver
- WebDriver Manager (for automatic driver management)

---

### **Launching Browsers**
- `webdriver.Chrome()`
- `webdriver.Firefox()`
- `webdriver.Edge()`
- `webdriver.Safari()`

---

### **WebDriver Interface**
- `get(url)`
- `close()`
- `quit()`
- `title`
- `current_url`
- `page_source`

---

### **Locating Elements (Find Elements)**
- By ID
- By Name
- By Class Name
- By Tag Name
- By Link Text
- By Partial Link Text
- By XPath
- By CSS Selector

---

### **WebElement Methods**
- `click()`
- `send_keys()`
- `clear()`
- `submit()`
- `get_attribute()`
- `text`
- `is_displayed()`
- `is_enabled()`
- `is_selected()`
- `screenshot(filename)`

---

### **Working with Forms and Inputs**
- Text input
- Checkboxes
- Radio buttons
- Dropdowns (Select class)
  - `select_by_value()`
  - `select_by_visible_text()`
  - `select_by_index()`
- File upload

---

### **Browser Navigation**
- `back()`
- `forward()`
- `refresh()`

---

### **Waits in Selenium**
- **Implicit Waits**
  - `driver.implicitly_wait(seconds)`
- **Explicit Waits**
  - `WebDriverWait`
  - Expected Conditions
    - `element_to_be_clickable()`
    - `presence_of_element_located()`
    - `visibility_of_element_located()`
    - `text_to_be_present_in_element()`
- **Fluent Waits** (custom polling + timeout)

---

### **Browser Windows and Tabs**
- `window_handles`
- `switch_to.window(handle)`
- `current_window_handle`
- `switch_to.new_window()`

---

### **Frames and IFrames**
- `switch_to.frame()`
- `switch_to.default_content()`
- `switch_to.parent_frame()`

---

### **Alerts and Popups**
- `switch_to.alert`
  - `accept()`
  - `dismiss()`
  - `send_keys()`
  - `text`

---

### **Actions Chains (Mouse and Keyboard)**
- `ActionChains(driver)`
  - `click()`
  - `double_click()`
  - `context_click()`
  - `move_to_element()`
  - `drag_and_drop()`
  - `send_keys_to_element()`
  - `key_down()`, `key_up()`
  - `perform()`

---

### **Screenshots**
- Full page: `driver.save_screenshot()`
- Element: `element.screenshot()`

---

### **Cookies**
- `get_cookies()`
- `get_cookie(name)`
- `add_cookie(dict)`
- `delete_cookie(name)`
- `delete_all_cookies()`

---

### **Page Scrolling**
- JavaScript execution
  - `execute_script("window.scrollTo(...)")`
- Scroll to element

---

### **JavaScript Execution**
- `execute_script()`
- `execute_async_script()`

---

### **Handling Timeouts and Exceptions**
- `TimeoutException`
- `NoSuchElementException`
- `ElementNotInteractableException`
- `StaleElementReferenceException`
- `WebDriverException`

---

### **Headless Browser Testing**
- ChromeOptions for headless
- Firefox headless mode

---

### **Logging and Debugging**
- Logging driver actions
- Using `print()` and `logs`

---

### **Selenium Grid**
- Hub and Node architecture
- Parallel test execution
- Running tests on remote machines

---

### **Integration with Test Frameworks**
- Unittest
- PyTest
- Nose2
- Behave (BDD)

---

### **Best Practices**
- Use waits over sleeps
- Page Object Model (POM)
- Separation of test logic and driver logic
- Reusable locators and functions
- Exception handling

---
