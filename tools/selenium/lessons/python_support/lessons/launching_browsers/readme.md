## **Launching Browsers – Selenium with Python**

This note provides complete coverage on how to launch and configure different web browsers using Selenium WebDriver in Python, including default, customized, and headless modes.

---

### **Default Browser Launch**

Each browser has its own driver class in `selenium.webdriver`.

#### **Chrome**
```python
from selenium import webdriver
driver = webdriver.Chrome()
```

#### **Firefox**
```python
from selenium import webdriver
driver = webdriver.Firefox()
```

#### **Edge**
```python
from selenium import webdriver
driver = webdriver.Edge()
```

#### **Safari**
```python
from selenium import webdriver
driver = webdriver.Safari()
```

> Ensure corresponding browser drivers are installed and available in PATH.

---

### **Custom Browser Launch with Options**

Each browser supports `Options` to modify browser behavior at launch.

#### **ChromeOptions**
```python
from selenium.webdriver.chrome.options import Options

options = Options()
options.add_argument("--start-maximized")       # Open window maximized
options.add_argument("--disable-extensions")    # Disable extensions
options.add_argument("--incognito")             # Private mode

driver = webdriver.Chrome(options=options)
```

#### **FirefoxOptions**
```python
from selenium.webdriver.firefox.options import Options

options = Options()
options.headless = False                        # Run in normal mode
options.add_argument("-private")                # Private browsing

driver = webdriver.Firefox(options=options)
```

#### **EdgeOptions**
```python
from selenium.webdriver.edge.options import Options

options = Options()
options.use_chromium = True                     # Required for Chromium Edge
options.add_argument("--start-maximized")

driver = webdriver.Edge(options=options)
```

---

### **Headless Browser Mode**

Useful for CI pipelines or running without a GUI.

#### **Headless Chrome**
```python
options = Options()
options.add_argument("--headless")
driver = webdriver.Chrome(options=options)
```

#### **Headless Firefox**
```python
options = Options()
options.headless = True
driver = webdriver.Firefox(options=options)
```

> Use `--window-size=1920,1080` for full viewport rendering in headless mode.

---

### **Remote WebDriver Launch (Selenium Grid / Docker)**

Connects to a remote browser session on another machine or Docker.

```python
from selenium import webdriver
from selenium.webdriver.common.desired_capabilities import DesiredCapabilities

driver = webdriver.Remote(
    command_executor="http://<hub_ip>:4444/wd/hub",
    desired_capabilities=DesiredCapabilities.CHROME
)
```

---

### **Specifying Driver Executable Path (if not in PATH)**

```python
driver = webdriver.Chrome(executable_path="C:/drivers/chromedriver.exe")
```

> Prefer using `webdriver-manager` to avoid hardcoded paths.

---

### **Using WebDriver Manager**

Recommended for automatic browser driver management.

```python
from selenium import webdriver
from webdriver_manager.chrome import ChromeDriverManager

driver = webdriver.Chrome(ChromeDriverManager().install())
```

---

### **Opening a Website After Launch**

```python
driver.get("https://www.example.com")
```

---

### **Important Parameters (for all browsers)**

| Parameter           | Description |
|---------------------|-------------|
| `options`           | Accepts browser configuration options |
| `executable_path`   | Full path to browser driver |
| `service`           | Advanced control via `Service` class |
| `desired_capabilities` | Used for remote execution / advanced features |

---
