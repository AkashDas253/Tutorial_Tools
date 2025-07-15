
## 🧩 Selenium for Python – Concepts & Subconcepts

### ⚙️ Setup & Installation
- Installation via pip
- WebDriver installation
  - ChromeDriver
  - GeckoDriver
  - EdgeDriver
- PATH configuration
- Browser version compatibility

---

### 🚦 WebDriver Basics
- `webdriver` module
- Initializing drivers
- Opening web pages (`get`)
- Closing drivers (`quit`, `close`)
- Browser navigation
  - `back()`
  - `forward()`
  - `refresh()`

---

### 🔍 Locating Elements
- Locator strategies (`By`)
  - ID
  - Name
  - Class Name
  - Tag Name
  - CSS Selector
  - XPath
  - Link Text
  - Partial Link Text
- Single vs multiple element selection
  - `find_element`
  - `find_elements`

---

### 🧪 Element Interactions
- `click()`
- `send_keys()`
- `clear()`
- `submit()`
- Get attributes (`get_attribute`)
- Get text (`text`)
- Visibility check (`is_displayed()`)

---

### ⏳ Waits
- Implicit Wait
- Explicit Wait
  - `WebDriverWait`
  - `expected_conditions`
- Fluent Wait (via `until` with polling)

---

### 🧰 Advanced User Interactions
- `ActionChains` class
  - Mouse hover
  - Drag and drop
  - Right-click
  - Double-click
- Keyboard actions (`Keys`)

---

### 🌐 Frames, Tabs, and Windows
- Switching frames
  - `switch_to.frame()`
  - `switch_to.default_content()`
- Multiple tabs/windows
  - `window_handles`
  - `switch_to.window()`

---

### 🧱 Alerts, Popups, and Modals
- Handling alerts
  - `switch_to.alert`
  - `accept()`
  - `dismiss()`
  - `send_keys()`

---

### 🔧 Browser Configuration
- Headless mode
- Browser options
  - Window size
  - Incognito mode
  - Disabling extensions
- Setting download directories

---

### 🖼 Screenshots and Page Data
- `save_screenshot()`
- `get_screenshot_as_file()`
- `get_screenshot_as_base64()`
- `page_source`

---

### 📄 Form Handling
- Input fields
- Checkboxes
- Radio buttons
- Dropdowns
  - Using `Select` class
- Submit buttons

---

### 📊 Handling Web Tables
- Accessing rows and cells
- Iterating over table data
- Extracting column values

---

### 📎 File Upload & Download
- Using `send_keys()` for upload
- Configuring download behavior in browser settings

---

### 📁 Cookies and Sessions
- `get_cookies()`
- `add_cookie()`
- `delete_cookie()`
- `delete_all_cookies()`

---

### 🔄 Executing JavaScript
- `execute_script()`
- Scroll events
- Custom script injection

---

### 🧪 Test Framework Integration
- PyTest
- Unittest
- Allure reports
- Behave (BDD)
- Nose2

---

### 🚀 Parallel & Grid Testing
- Selenium Grid
  - Hub and node setup
  - Remote WebDriver
- `concurrent.futures` or `pytest-xdist` for parallelism

---

### 📦 Best Practices
- Element wait strategies
- Page Object Model (POM)
- Test data management
- Locator reusability
- Logging and reporting

---
