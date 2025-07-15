## **Working with Forms and Inputs – Selenium with Python**

Forms and input fields are key components of web interaction. Selenium provides comprehensive tools to locate, fill out, clear, and submit forms and their associated input fields such as text boxes, checkboxes, radio buttons, and dropdowns.

---

### **Overview**

- Form elements include text fields, password fields, textareas, checkboxes, radio buttons, buttons, and select dropdowns.
- Interactions are done using `WebElement` methods like `send_keys()`, `click()`, `clear()`, and `submit()`.

---

### **Text Inputs (Text Fields, Textareas, Password Fields)**

| Method                     | Description |
|----------------------------|-------------|
| `send_keys("text")`        | Enters text into the input field |
| `clear()`                  | Clears existing text from the field |
| `get_attribute("value")`   | Gets current text/value from the field |

```python
username = driver.find_element(By.NAME, "username")
username.clear()
username.send_keys("testuser")
```

---

### **Radio Buttons and Checkboxes**

| Operation           | Method Example |
|---------------------|----------------|
| Select an option    | `element.click()` |
| Check selection     | `element.is_selected()` |
| Conditional select  | `if not element.is_selected(): element.click()` |

```python
# Select a checkbox if not already selected
checkbox = driver.find_element(By.ID, "remember")
if not checkbox.is_selected():
    checkbox.click()
```

---

### **Dropdowns (Select Elements)**

Use `Select` class from `selenium.webdriver.support.ui`.

```python
from selenium.webdriver.support.ui import Select

dropdown = Select(driver.find_element(By.ID, "country"))

dropdown.select_by_visible_text("India")
dropdown.select_by_value("IN")
dropdown.select_by_index(2)

# Get selected option
print(dropdown.first_selected_option.text)

# List all options
for option in dropdown.options:
    print(option.text)
```

---

### **Form Submission**

| Method     | Description |
|------------|-------------|
| `submit()` | Submits the form containing the element |

```python
input_field = driver.find_element(By.ID, "email")
input_field.send_keys("test@example.com")
input_field.submit()  # Submits the parent <form>
```

*Alternative:* Use the submit button's `.click()` method.

---

### **File Upload Input**

```python
upload = driver.find_element(By.NAME, "file")
upload.send_keys("/path/to/file.txt")
```

*Only works with `<input type="file">`.*

---

### **Buttons**

| Type         | Interaction |
|--------------|-------------|
| `<button>`   | `click()`   |
| `<input type="submit">` | `click()` |

```python
submit_btn = driver.find_element(By.ID, "submit-btn")
submit_btn.click()
```

---

### **Form Validations and Alerts**

- JavaScript validation errors may prevent submission.
- Check for alert or inline error messages after `submit()`.

```python
error = driver.find_element(By.CLASS_NAME, "error-message")
print(error.text)
```

---

### **Common Attributes to Extract**

| Attribute       | Purpose |
|------------------|---------|
| `value`          | Current content of input |
| `name`           | Often used in form submissions |
| `placeholder`    | Hint shown inside input |
| `type`           | Input type (`text`, `password`, `email`, etc.) |
| `required`       | Whether field is mandatory |

```python
email = driver.find_element(By.ID, "email")
print(email.get_attribute("placeholder"))
```

---

### **Best Practices**

- Use `clear()` before `send_keys()` for predictable behavior.
- Wait for input fields to be visible and enabled.
- Use `Select` only for `<select>` elements.
- Use `is_selected()` before clicking radio/checkbox.
- Handle alerts and validation errors after form submission.

---
