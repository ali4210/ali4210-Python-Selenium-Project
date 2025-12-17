I have rebuilt both documents from the ground up.

These are now the **Definitive Editions**. They seamlessly merge your **Core Automation Scripts** (Stealth, Actions, Scraping) with your **Enterprise Infrastructure** (Selenium Grid).

The **Master Guide** is designed as a global textbook—anyone from a junior tester to a senior SDET can follow it to build this system.

---

### 📘 Document 1: MASTER_GUIDE.md

*This is the comprehensive manual. Save this in your root directory.*

```markdown
# Alnafi Selenium & Grid Framework: The Ultimate Automation Guide
**Author:** Saleem Ali
**Architecture:** Hybrid (Local Execution & Distributed Grid)
**Domain:** SDET, Web Scraping, & Bot Development
**Tech Stack:** Python 3.x, Selenium 4, Selenium Grid (Java), BeautifulSoup4

---

## ==>> 1. Introduction & Project Scope
This repository is not just a collection of scripts; it is a complete **Quality Assurance (QA) Framework**. It covers three distinct levels of automation complexity:

1.  **Level 1 (Functional):** Interacting with standard web elements (forms, dropdowns, alerts).
2.  **Level 2 (Stealth):** Advanced algorithms to mimic human behavior and bypass anti-bot security (e.g., Gmail Login).
3.  **Level 3 (Infrastructure):** Distributed execution using **Selenium Grid**, allowing tests to run on remote servers rather than the local machine.

---

## ==>> 2. Environment Setup (Universal)
*Whether you are a beginner or a pro, start here.*

### => Step 1: Install Python Dependencies
The project relies on `selenium` for control and `webdriver-manager` to avoid manual driver downloads.
* **File:** `requirements.txt`
```bash
pip install -r requirements.txt

```

### => Step 2: Install Java (For Grid)

Selenium Grid is a Java application. You must have the **Java Runtime Environment (JRE 11+)** installed to run the `.jar` server files.

* Verify installation: `java -version`

---

## ==>> Module 1: The Core Automation Framework

*Scripts for Local Execution (running directly on your PC).*

### => Driver Management

**Concept:** We do not hardcode paths like `C:\chromedriver.exe`. We use `webdriver_manager` to download the correct driver automatically at runtime.

* **File:** `web_driver_auto_update_browser.py`

```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager

service = Service(ChromeDriverManager().install())
driver = webdriver.Chrome(service=service)

```

### => Advanced Locators & Controls

**Concept:** Handling dynamic elements that standard IDs cannot find.

* **File:** `checkbox.py` (Iterating through lists)
* **File:** `css-sdelectors.py` (Using Attribute Selectors)

```python
# Finding elements by partial attributes
driver.find_element(By.CSS_SELECTOR, "input[type='email']")

```

### => ActionChains (Mouse & Keyboard)

**Concept:** Simulating complex physical actions like Drag-and-Drop, Hover, and Context Clicks.

* **File:** `drag_slider_range.py`
* **File:** `mouse-over-effect.py`
* **File:** `complex-element(Right_Click).py`

```python
from selenium.webdriver import ActionChains
# Drag an element 50 pixels to the left
actions.drag_and_drop_by_offset(element, -50, 0).perform()

```

---

## ==>> Module 2: The "Stealth" Login System

*How to bypass bot detection on high-security sites like Google.*

### => The Human Emulation Algorithm

**File:** `gmail_login-1.py`
Standard automation dumps text instantly (e.g., `send_keys("password")`). This triggers security flags. We solve this by introducing random delays between keystrokes.

```python
import time, random

def human_type(element, text):
    for char in text:
        element.send_keys(char)
        # Sleep for random ms between keystrokes
        time.sleep(random.uniform(0.05, 0.2))

```

### => Removing Automation Flags

Browsers broadcast a flag `navigator.webdriver = true`. We must disable this to appear as a standard user.

```python
options.add_argument("--disable-blink-features=AutomationControlled")
options.add_experimental_option("excludeSwitches", ["enable-automation"])

```

---

## ==>> Module 3: Distributed Infrastructure (Selenium Grid)

*Running tests on a remote network (The Enterprise Standard).*

### => Concept

Instead of the Python script opening a browser window on *your* screen, it sends commands (JSON) to a central **Hub**. The Hub finds an available **Node** (worker machine) to execute the test.

### => Step 1: Start the Hub

The Traffic Controller. Run this in **Terminal 1**.

```bash
java -jar Selenium-Grid/selenium-server-4.38.0.jar hub

```

* **Output:** `Started Selenium Hub 4.38.0` on Port 4444.

### => Step 2: Start the Node

The Worker. Run this in **Terminal 2**.

```bash
java -jar Selenium-Grid/selenium-server-4.38.0.jar node --detect-drivers true

```

* **Output:** `Node has been added`.

### => Step 3: Connect Python to Grid

**File:** `Selenium-Grid/selenium_grid_test.py`
We switch from `webdriver.Chrome()` to `webdriver.Remote()`.

```python
from selenium import webdriver
from selenium.webdriver.chrome.options import Options

# Point to the Hub Address (Localhost for testing)
hub_url = "[http://127.0.0.1:4444/wd/hub](http://127.0.0.1:4444/wd/hub)"

# Use Options (Selenium 4 Requirement)
chrome_options = Options()

# Initialize Remote Connection
driver = webdriver.Remote(
    command_executor=hub_url,
    options=chrome_options
)

driver.get("[https://www.google.com](https://www.google.com)")
print(f"Executed on Grid Node: {driver.title}")
driver.quit()

```

---

## ==>> Module 4: Data & Evidence

### => Static Scraping

**File:** `scraping.py`
Uses `BeautifulSoup` to parse HTML text without rendering the UI. Ideal for fast data extraction.

### => Forensic Screenshots

**File:** `screenshot_full_page.py`
Uses JavaScript injection to calculate the true height of a webpage and resize the window before capturing, ensuring no data is cut off.

---

**Status:** Completed & Validated
**Recommended Path:** Start with Module 1 (Local), move to Module 2 (Stealth), and finalize with Module 3 (Grid).

```

