##  Selenium Cheatsheet (Python)

###  Setup

```bash
pip install selenium
```

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
```

###  Launching Browser

```python
driver = webdriver.Chrome()  # or Firefox(), Edge()
driver.get("https://example.com")
driver.maximize_window()
driver.quit()
```

---

##  WebDriver Interface

| Method                  | Description                        |
|-------------------------|------------------------------------|
| `get(url)`              | Open URL                           |
| `close()`               | Close current window               |
| `quit()`                | Close all windows and end session  |
| `title`                | Get page title                     |
| `current_url`          | Get current URL                    |
| `page_source`          | Get HTML source                    |

---

##  Locating Elements

```python
driver.find_element(By.ID, "id")
driver.find_elements(By.CLASS_NAME, "class")
driver.find_element(By.NAME, "name")
driver.find_element(By.XPATH, "//tag[@attr='value']")
driver.find_element(By.CSS_SELECTOR, "tag[attr='value']")
```

---

##  WebElement Methods

| Method           | Description                        |
|------------------|------------------------------------|
| `.click()`       | Click element                      |
| `.send_keys()`   | Input text                         |
| `.text`          | Get element text                   |
| `.get_attribute()` | Get HTML attribute                |
| `.is_displayed()` | Visibility check                  |
| `.clear()`       | Clear text from input              |

---

##  Forms & Inputs

```python
input_box = driver.find_element(By.ID, "search")
input_box.send_keys("Query")
input_box.submit()
```

---

##  Navigation

```python
driver.back()
driver.forward()
driver.refresh()
```

---

##  Waits

### Implicit Wait
```python
driver.implicitly_wait(10)  # seconds
```

###  Explicit Wait
```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

WebDriverWait(driver, 10).until(EC.presence_of_element_located((By.ID, "id")))
```

###  Fluent Wait
```python
wait = WebDriverWait(driver, 10, poll_frequency=1, ignored_exceptions=[Exception])
```

---

##  Windows and Tabs

```python
driver.window_handles  # List of all handles
driver.switch_to.window(driver.window_handles[1])
```

---

##  Frames and iFrames

```python
driver.switch_to.frame("frame_id")
driver.switch_to.default_content()
```

---

##  Alerts and Popups

```python
alert = driver.switch_to.alert
alert.accept()
alert.dismiss()
alert.send_keys("text")
```

---

##  Action Chains

```python
from selenium.webdriver import ActionChains

actions = ActionChains(driver)
actions.move_to_element(el).click().perform()
```

---

##  Screenshots

```python
driver.save_screenshot("screen.png")
```

---

##  Cookies

```python
driver.get_cookies()
driver.add_cookie({"name": "token", "value": "123"})
driver.delete_all_cookies()
```

---

##  Page Scrolling

```python
driver.execute_script("window.scrollTo(0, document.body.scrollHeight);")
```

---

##  JavaScript Execution

```python
driver.execute_script("arguments[0].click();", element)
```

---

##  Exception Handling

```python
from selenium.common.exceptions import NoSuchElementException

try:
    driver.find_element(By.ID, "nonexistent")
except NoSuchElementException:
    print("Element not found")
```

---

##  Headless Testing

```python
from selenium.webdriver.chrome.options import Options

options = Options()
options.add_argument("--headless")
driver = webdriver.Chrome(options=options)
```

---

##  Selenium Grid

- **Hub**: `java -jar selenium-server.jar hub`
- **Node**: `java -jar selenium-server.jar node -hub http://localhost:4444/grid/register`
- **Remote Driver**:
  ```python
  from selenium import webdriver
  driver = webdriver.Remote(command_executor="http://localhost:4444/wd/hub",
                            desired_capabilities={"browserName": "chrome"})
  ```

---

##  Test Framework Integration

###  unittest
```python
import unittest

class TestExample(unittest.TestCase):
    def setUp(self):
        self.driver = webdriver.Chrome()
    def test_title(self):
        self.driver.get("https://example.com")
        self.assertIn("Example", self.driver.title)
    def tearDown(self):
        self.driver.quit()
```

###  pytest
```python
def test_title():
    driver = webdriver.Chrome()
    driver.get("https://example.com")
    assert "Example" in driver.title
    driver.quit()
```

###  nose2, behave (BDD)
- `nose2`: drop-in for unittest
- `behave`: uses `@given`, `@when`, `@then` steps in `.feature` files

---

##  Best Practices

- Use **explicit waits** over `sleep()`
- Follow **Page Object Model (POM)**
- **Separate** test logic and driver logic
- Use **reusable locators/functions**
- Implement **exception handling**
- Add **logging** and **screenshots** for debugging

---
