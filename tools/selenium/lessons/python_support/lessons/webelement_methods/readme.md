## **WebElement Methods – Selenium with Python**

The `WebElement` interface in Selenium represents elements found in a web page. Once located using a method like `find_element()`, a `WebElement` object can be used to perform various actions (like clicking, typing, retrieving data) or to inspect its properties (like text, tag name, or attributes).

---

### **Overview**

- Returned by: `find_element()` or `find_elements()`.
- Used to interact with HTML elements (buttons, inputs, links, etc.).
- All browser commands on elements (click, input, get text) are handled via `WebElement`.

---

### **Common WebElement Methods**

| Method                          | Description |
|----------------------------------|-------------|
| `click()`                        | Clicks the element (e.g., button, link) |
| `send_keys(*value)`              | Types text or keys into the element (e.g., input fields) |
| `clear()`                        | Clears the content of an input or textarea |
| `submit()`                       | Submits a form element |
| `get_attribute(name)`            | Returns the value of a given attribute |
| `get_property(name)`             | Returns the DOM property (JS-based) |
| `text`                           | Returns the visible text of the element |
| `tag_name`                       | Returns the element’s tag name (e.g., `input`) |
| `is_displayed()`                 | Returns `True` if the element is visible |
| `is_enabled()`                   | Returns `True` if the element is enabled |
| `is_selected()`                 | Returns `True` if checkbox/radio is selected |
| `screenshot(filename)`           | Saves a screenshot of the element |
| `value_of_css_property(name)`    | Returns the value of the specified CSS property |
| `location`                       | Returns X and Y coordinates of the element |
| `size`                           | Returns the height and width |
| `rect`                           | Returns a dict with location and size info |
| `accessible_name`                | ARIA-accessible name for assistive tools |
| `aria_role`                      | ARIA role of the element |

---

### **Example Usage**

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()
driver.get("https://example.com")

element = driver.find_element(By.ID, "username")

# Interaction
element.click()
element.send_keys("testuser")
element.clear()

# Attribute inspection
print(element.text)
print(element.get_attribute("placeholder"))
print(element.is_displayed())
print(element.tag_name)

driver.quit()
```

---

### **send_keys() Special Keys**

Use from `selenium.webdriver.common.keys`:

```python
from selenium.webdriver.common.keys import Keys

element.send_keys(Keys.ENTER)
element.send_keys(Keys.TAB)
element.send_keys(Keys.CONTROL, "a")  # Ctrl + A
```

---

### **CSS & Layout Properties**

| Property             | Method                         |
|----------------------|--------------------------------|
| Element text color   | `value_of_css_property('color')` |
| Background color     | `value_of_css_property('background-color')` |
| Font family          | `value_of_css_property('font-family')` |
| Element size         | `element.size` or `element.rect` |
| Element position     | `element.location`             |

---

### **Element Screenshot**

```python
element = driver.find_element(By.ID, "logo")
element.screenshot("logo.png")
```

---

### **Best Practices**

- Always re-locate the element after a page reload or DOM change.
- Use `is_displayed()` before interacting to ensure visibility.
- Prefer `get_attribute()` for form inputs and dynamic values.
- Avoid using `submit()` on non-form elements (use `click()` instead).

---
