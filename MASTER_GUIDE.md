# 🎓 SELENIUM AUTOMATION & GRID MASTERY GUIDE
### Complete Learning Resource: Zero to DevOps Hero
### Author: Saleem Ali | AIOps Engineer

---

## 📖 TABLE OF CONTENTS

### PART 1: FOUNDATION (Chapters 1-4)
1. Introduction to Selenium
2. Environment Setup & Installation
3. WebDriver Basics & Browser Control
4. Locator Strategies (ID, Name, CSS, XPath)

### PART 2: INTERMEDIATE AUTOMATION (Chapters 5-8)
5. Web Element Interactions
6. Form Handling (Dropdowns, Checkboxes)
7. Browser Options & Configurations
8. Synchronization Strategies

### PART 3: ADVANCED TECHNIQUES (Chapters 9-15)
9. Complex User Interactions (Mouse, Keyboard)
10. Alert & Popup Handling
11. Iframe Navigation
12. Window & Tab Management
13. Screenshot Capabilities
14. Web Scraping Integration
15. Error Handling & Element Validation

### PART 4: SELENIUM GRID - DEVOPS LEVEL (Chapters 16-19)
16. Grid Architecture & Components
17. Hub-Node Setup & Configuration
18. Distributed Testing Implementation
19. Grid Best Practices & Scaling

### PART 5: PROFESSIONAL PRACTICES (Chapters 20-23)
20. Project Organization & Structure
21. Security Best Practices
22. CI/CD Integration
23. Real-World DevOps Applications

---

# PART 1: FOUNDATION

## Chapter 1: Introduction to Selenium

### 1.1 What is Selenium?

Selenium is the **industry-standard** open-source framework for automating web browsers. Used by millions of developers worldwide for testing, monitoring, and automation.

**Key Statistics:**
- 📊 30+ million downloads monthly
- 🏢 Used by Google, Amazon, Netflix, Facebook
- 💼 #1 skill for QA & DevOps engineers
- 🌍 Supports 10+ programming languages

### 1.2 Selenium Ecosystem

```
┌─────────────────────────────────────────┐
│         SELENIUM ECOSYSTEM              │
├─────────────────────────────────────────┤
│ 1. SELENIUM WEBDRIVER (Core)           │
│    ├── Browser automation engine        │
│    ├── Direct browser control           │
│    └── Language bindings (Python, Java)│
│                                         │
│ 2. SELENIUM GRID (Distribution) ⭐      │
│    ├── Parallel execution               │
│    ├── Multi-browser testing            │
│    ├── Hub-Node architecture            │
│    └── Scalable infrastructure          │
│                                         │
│ 3. SELENIUM IDE (Recording)             │
│    ├── Browser extension                │
│    └── Quick record & playback          │
└─────────────────────────────────────────┘
```

### 1.3 Why Learn Selenium + Grid?

**Career Impact:**
✅ **DevOps Engineer:** CI/CD pipeline testing
✅ **QA Engineer:** Automated regression testing
✅ **AIOps Engineer:** Monitoring & validation
✅ **Data Engineer:** Web scraping at scale

**Grid Advantage (Your Edge!):**
```
Without Grid:           With Grid (Your Skill!):
├── 1 browser           ├── 10+ browsers parallel
├── 1 test at a time    ├── 100+ tests simultaneously
├── 2 hours runtime     ├── 10 minutes runtime
└── Limited scaling     └── Infinite scaling
```

---

## Chapter 2: Environment Setup

### 2.1 Complete Installation

**Step 1: Install Python Dependencies**
```bash
# Install all required packages
pip install -r requirements.txt
```

**Step 2: Verify Installation**
```bash
python -c "import selenium; print(selenium.__version__)"
# Expected output: 4.38.0
```

**Step 3: Download Selenium Grid JAR**
```bash
# Grid Server (for distributed testing)
# Download from: https://github.com/SeleniumHQ/selenium/releases
# File: selenium-server-4.38.0.jar
```

### 2.2 Requirements.txt Deep Dive

```txt
# Core Selenium
selenium==4.38.0

# WebDriver Management (Auto-updates drivers)
webdriver-manager==4.0.1

# Web Scraping
beautifulsoup4==4.12.2
requests==2.31.0

# Security & Environment
python-dotenv==1.0.0
```

**Why Each Package?**

```python
selenium==4.38.0
```
- **Purpose:** Core browser automation
- **Features:** WebDriver API, Grid support
- **Why 4.38.0:** Latest stable with Grid 4

```python
webdriver-manager==4.0.1
```
- **Purpose:** Auto-download browser drivers
- **Benefit:** No manual driver maintenance
- **How:** Detects browser version → Downloads matching driver

```python
beautifulsoup4==4.12.2
```
- **Purpose:** HTML parsing for scraping
- **Use with Selenium:** Extract structured data
- **Example:** Parse tables, lists, dynamic content

```python
python-dotenv==1.0.0
```
- **Purpose:** Environment variable management
- **Security:** Keep credentials out of code
- **Usage:**
  ```python
  from dotenv import load_dotenv
  import os
  
  load_dotenv()
  password = os.getenv('PASSWORD')  # Secure!
  ```

### 2.3 Project Structure

```
selenium-automation-grid/
├── drivers/                 # Browser drivers (auto-managed)
│   ├── chromedriver.exe
│   ├── geckodriver.exe
│   └── msedgedriver.exe
├── screenshots/            # Captured screenshots
│   └── myfile
├── tests/                  # Test automation scripts
│   ├── Alert_handeling.py
│   ├── checkbox.py
│   ├── iframe.py
│   └── ...
├── grid/                   # Selenium Grid setup
│   ├── selenium-server-4.38.0.jar
│   └── selenium_grid_test.py
├── requirements.txt        # Python dependencies
├── .gitignore             # Security exclusions
├── .env                   # Environment variables (secure)
└── README.md              # Project documentation
```

---

## Chapter 3: WebDriver Basics

### 3.1 Chrome WebDriver (Manual Path)

**FILE: chrome_script.py**
```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service

path = Service(r"C:\Users\User\PycharmProjects\pythonProject3\Alnafi Selenium\Drivers\chromedriver.exe")
driver = webdriver.Chrome(service=path)
driver.get("https://www.alnafi.com")
```

**📝 LINE-BY-LINE:**

```python
from selenium import webdriver
```
- Imports core WebDriver module
- Provides browser classes (Chrome, Firefox, Edge)

```python
from selenium.webdriver.chrome.service import Service
```
- **Selenium 4 requirement:** Must use Service class
- Replaces deprecated `executable_path` parameter

```python
path = Service(r"C:\...\chromedriver.exe")
```
- **r prefix:** Raw string (handles Windows backslashes)
- **Why Service?** Encapsulates driver configuration
- **Manual path:** You download driver yourself

```python
driver = webdriver.Chrome(service=path)
```
- Creates Chrome browser instance
- Returns WebDriver object for control

```python
driver.get("https://www.alnafi.com")
```
- Navigates to URL
- Waits for page load (default behavior)

### 3.2 Auto-Update WebDriver (Production Ready)

**FILE: web_driver_auto_update_browser.py**
```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager

path = Service(ChromeDriverManager().install())
driver = webdriver.Chrome(service=path)
driver.get("https://www.alnafi.com")
driver.maximize_window()

web_title = driver.title
if web_title == "Al Nafi | Online Courses, Certificates, and Diplomas in Emerging Technologies":
    print(f"Yes, Title is Verified: {web_title}")
else:
    print(f"No, Title is Not Verified: {web_title}")

driver.quit()
```

**🔍 WHAT HAPPENS BEHIND THE SCENES:**

```python
ChromeDriverManager().install()
```

**First Run:**
```
1. Detect Chrome version: 120.0.6099.129
2. Download matching chromedriver from official source
3. Cache: ~/.wdm/drivers/chromedriver/120.0/chromedriver.exe
4. Return cached path
   Time: ~5 seconds
```

**Subsequent Runs:**
```
1. Check cache for Chrome 120.0
2. Found! Return cached path
   Time: ~0.1 seconds (instant!)
```

```python
driver.maximize_window()
```
- **Why critical:**
  - Consistent element positions
  - All content visible (no hidden elements)
  - Better for screenshots
  - Prevents responsive layout shifts

```python
web_title = driver.title
```
- Returns page `<title>` tag content
- Use case: Verify correct page loaded

```python
driver.quit()
```
- **quit() vs close():**
  ```python
  driver.close()  # Closes current window only
  driver.quit()   # Closes ALL windows + ends session
  ```

### 3.3 Multi-Browser Support

**Firefox:**
```python
from selenium import webdriver
from webdriver_manager.firefox import GeckoDriverManager
from selenium.webdriver.firefox.service import Service

service = Service(GeckoDriverManager().install())
driver = webdriver.Firefox(service=service)
```

**Edge:**
```python
from selenium import webdriver
from webdriver_manager.microsoft import EdgeChromiumDriverManager
from selenium.webdriver.edge.service import Service

service = Service(EdgeChromiumDriverManager().install())
driver = webdriver.Edge(service=service)
```

**Browser Comparison:**
```
┌─────────────┬──────────┬─────────────┬───────────────┐
│   Browser   │  Speed   │  Stability  │  Use Case     │
├─────────────┼──────────┼─────────────┼───────────────┤
│ Chrome      │ ⚡⚡⚡⚡⚡   │ Excellent   │ Primary       │
│ Firefox     │ ⚡⚡⚡⚡     │ Good        │ Cross-browser │
│ Edge        │ ⚡⚡⚡⚡⚡   │ Excellent   │ Windows focus │
└─────────────┴──────────┴─────────────┴───────────────┘
```

---

## Chapter 4: Locator Strategies

### 4.1 The 8 Locators

```python
from selenium.webdriver.common.by import By

# 1. ID (Fastest)
driver.find_element(By.ID, "username")

# 2. NAME
driver.find_element(By.NAME, "email")

# 3. CLASS_NAME
driver.find_element(By.CLASS_NAME, "btn-primary")

# 4. TAG_NAME
driver.find_element(By.TAG_NAME, "input")

# 5. LINK_TEXT (Exact match)
driver.find_element(By.LINK_TEXT, "Sign Up")

# 6. PARTIAL_LINK_TEXT
driver.find_element(By.PARTIAL_LINK_TEXT, "Sign")

# 7. CSS_SELECTOR
driver.find_element(By.CSS_SELECTOR, "input[name='email']")

# 8. XPATH (Most powerful)
driver.find_element(By.XPATH, "//input[@name='email']")
```

### 4.2 CSS Selectors Mastery

**Basic Syntax:**
```css
#id                  /* By ID */
.class               /* By class */
element              /* By tag */
[attribute='value']  /* By attribute */
```

**Combined Selectors:**
```css
input#username           /* Tag + ID */
input.form-control       /* Tag + class */
input[type='email']      /* Tag + attribute */
div > input              /* Direct child */
div input                /* Descendant */
```

**Example:**
```python
# Multiple ways to find same element
driver.find_element(By.CSS_SELECTOR, "#identifierId")
driver.find_element(By.CSS_SELECTOR, "input#identifierId")
driver.find_element(By.CSS_SELECTOR, "input[id='identifierId']")
driver.find_element(By.CSS_SELECTOR, "input[type='email']#identifierId")
```

### 4.3 XPath Complete Guide

**Basic XPath:**
```xpath
//tag[@attribute='value']
//input[@id='username']
//button[@type='submit']
```

**Advanced XPath:**
```xpath
# Text content
//button[text()='Login']
//button[contains(text(), 'Log')]

# Multiple conditions
//input[@id='email' and @type='text']

# Hierarchy
//form[@id='login']/div/input[1]
//div[@class='form']//input

# Axes
//input[@id='email']/parent::div
//input[@id='email']/following-sibling::input
//div[@class='container']//descendant::input
```

**XPath vs CSS:**
```
CSS Selectors:
✅ Faster (20-30% performance gain)
✅ Simpler syntax
✅ Better readability
❌ Cannot traverse up (parent)
❌ Limited text matching

XPath:
✅ Can navigate parent/sibling
✅ Powerful text matching
✅ More flexible
❌ Slower performance
❌ Complex syntax
```

---

# PART 2: INTERMEDIATE AUTOMATION

## Chapter 5: Form Handling

### 5.1 Dropdown Handling

**FILE: drop-down-2.py**
```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.select import Select
from webdriver_manager.firefox import GeckoDriverManager
from selenium.webdriver.firefox.service import Service
import time

service = Service(GeckoDriverManager().install())
driver = webdriver.Firefox(service=service)
driver.get("https://www.wikipedia.org/")
driver.maximize_window()

my_select = driver.find_element(By.ID, "searchLanguage")
sel = Select(my_select)

# Three ways to select
sel.select_by_value("af")              # By value attribute
sel.select_by_visible_text('Latina')  # By visible text
sel.select_by_index(2)                 # By index (0-based)

time.sleep(5)
driver.quit()
```

**📝 Select Class Explained:**

```python
from selenium.webdriver.support.select import Select
```
- Special class for `<select>` dropdowns
- Simplifies dropdown interaction
- Three selection methods

```python
my_select = driver.find_element(By.ID, "searchLanguage")
sel = Select(my_select)
```
**Why two steps?**
1. Find the `<select>` element
2. Wrap in Select() for dropdown methods

**Selection Methods:**
```python
# Method 1: By value attribute
sel.select_by_value("af")
# Selects: <option value="af">Afrikaans</option>

# Method 2: By visible text (Most common)
sel.select_by_visible_text('Latina')
# Selects: <option value="la">Latina</option>

# Method 3: By index
sel.select_by_index(2)
# Selects: 3rd option (0-based index)
```

**When to use each:**
```
select_by_value()        → When value is stable/known
select_by_visible_text() → Most readable (recommended)
select_by_index()        → Rarely used (fragile)
```

**Additional Select Methods:**
```python
# Get selected option
selected = sel.first_selected_option
print(selected.text)

# Get all options
all_options = sel.options
for option in all_options:
    print(option.text)

# Deselect (multi-select only)
sel.deselect_by_index(0)
sel.deselect_all()
```

### 5.2 Checkbox Handling

**FILE: checkbox.py**
```python
import time
from selenium import webdriver
from selenium.webdriver.firefox.service import Service
from webdriver_manager.firefox import GeckoDriverManager
from selenium.webdriver.common.by import By

driver = webdriver.Firefox(service=Service(GeckoDriverManager().install()))
driver.get("https://admin-demo.nopcommerce.com/Admin/Order/List")
driver.maximize_window()

# Login first
my_email = driver.find_element(By.ID, "Email")
my_email.clear()
time.sleep(2)
my_email.send_keys('admin@yourstore.com')

my_password = driver.find_element(By.ID, "Password")
my_password.clear()
time.sleep(2)
my_password.send_keys('admin')

time.sleep(2)
driver.find_element(By.ID, 'RememberMe').click()

time.sleep(3)
driver.find_element(By.XPATH, '/html/body/div[6]/main/div/section/div/div[2]/div[1]/div/form/div[3]/button').click()

time.sleep(3)

def is_element_present(att, abd):
    if len(driver.find_elements(by=att, value=abd)) == 0:
        return False
    else:
        return True

# Method 1: Dynamic checkbox selection (loop)
i = 1
while is_element_present(By.XPATH, '/html/body/div[3]/div[1]/form[1]/section/div/div/div/div[2]/div/div[2]/div[1]/div/div/div[3]/table/tbody/tr['+str(i)+']/td[1]/input'):
    driver.find_element(By.XPATH, '/html/body/div[3]/div[1]/form[1]/section/div/div/div/div[2]/div/div[2]/div[1]/div/div/div[3]/table/tbody/tr['+str(i)+']/td[1]/input').click()
    time.sleep(2)
    i = i + 1
print("Total checkbox value is:", len(driver.find_elements(By.CLASS_NAME, 'checkboxGroups')))

# Method 2: Select all checkboxes by name
time.sleep(2)
driver.find_element(By.XPATH, '/html/body/div[3]/aside/div/nav/ul/li[4]/a').click()
driver.find_element(By.XPATH, '/html/body/div[3]/aside/div/nav/ul/li[4]/ul/li[1]/a/p').click()
time.sleep(2)

my_checkboxes = driver.find_elements(By.NAME, 'checkbox_customers')
for checkbox in my_checkboxes:
    checkbox.click()
    time.sleep(2)
print("Total checkbox value is:", len(driver.find_elements(By.NAME, 'checkbox_customers')))

driver.quit()
```

**🔍 KEY CONCEPTS:**

```python
my_email.clear()
```
- **Purpose:** Clear existing text in input field
- **When needed:** Pre-filled forms, previous test data
- **Best practice:** Always clear before typing

```python
def is_element_present(att, abd):
    if len(driver.find_elements(by=att, value=abd)) == 0:
        return False
    else:
        return True
```

**Why `find_elements` (plural)?**
```python
# find_element() - Throws exception if not found
element = driver.find_element(By.ID, "missing")  # ❌ Error!

# find_elements() - Returns empty list if not found
elements = driver.find_elements(By.ID, "missing")  # ✅ Returns []
```

**Dynamic XPath Pattern:**
```python
i = 1
while is_element_present(By.XPATH, '...tr['+str(i)+']/td[1]/input'):
    driver.find_element(By.XPATH, '...tr['+str(i)+']/td[1]/input').click()
    i = i + 1
```

**Breaking it down:**
```
Iteration 1: ...tr[1]/td[1]/input  → First checkbox
Iteration 2: ...tr[2]/td[1]/input  → Second checkbox
Iteration 3: ...tr[3]/td[1]/input  → Third checkbox
...until no more elements found
```

**Method 2: Bulk Selection**
```python
my_checkboxes = driver.find_elements(By.NAME, 'checkbox_customers')
for checkbox in my_checkboxes:
    checkbox.click()
```

**When to use:**
- **Method 1 (Loop):** Unknown number of elements
- **Method 2 (Bulk):** All elements share common attribute

---

## Chapter 6: Synchronization Strategies

### 6.1 Why Synchronization?

**The Problem:**
```python
driver.get("https://example.com")
driver.find_element(By.ID, "button").click()  # ❌ May fail!
```

**Why it fails:**
- Page not fully loaded
- JavaScript still executing
- Element not yet rendered
- AJAX request pending

### 6.2 Three Wait Strategies

**1. Implicit Wait (Global):**
```python
driver.implicitly_wait(10)  # Wait up to 10 seconds for ANY element
```

**2. Explicit Wait (Specific):**
```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

wait = WebDriverWait(driver, 10)
element = wait.until(EC.element_to_be_clickable((By.ID, "button")))
element.click()
```

**3. Sleep (Last Resort):**
```python
import time
time.sleep(3)  # Hard wait (not recommended for production)
```

### 6.3 Real Implementation

**FILE: gmail-login-sync.py**
```python
from selenium import webdriver
from selenium.webdriver.support import expected_conditions
from selenium.webdriver.support.wait import WebDriverWait
from webdriver_manager.firefox import GeckoDriverManager
from selenium.webdriver.firefox.service import Service
from selenium.webdriver.common.by import By

service = Service(GeckoDriverManager().install())
driver = webdriver.Firefox(service=service)

driver.implicitly_wait(20)
wait = WebDriverWait(driver, 10)

driver.get("https://workspace.google.com/intl/en-US/gmail/")
driver.maximize_window()

driver.find_element(By.PARTIAL_LINK_TEXT, 'Sign in').click()
driver.find_element(By.ID, 'identifierId').send_keys('saleemali.mohammad')
driver.find_element(By.XPATH, '//*[@id="identifierNext"]/div/button/span').click()

action = wait.until(expected_conditions.element_to_be_clickable((By.NAME, 'Passwd')))
action.send_keys('Alisaleem01627609670')

login = wait.until(expected_conditions.element_to_be_clickable((By.XPATH, '//*[@id="identifierNext"]/div/button/span')))
login.click()

print("Login Success")
driver.quit()
```

**📝 BREAKDOWN:**

```python
driver.implicitly_wait(20)
```
- **Scope:** Global (all find_element calls)
- **Behavior:** Polls DOM for up to 20 seconds
- **When stops:** Element found OR 20 seconds passed

```python
wait = WebDriverWait(driver, 10)
```
- **Scope:** Specific conditions
- **Behavior:** More intelligent than implicit
- **Timeout:** 10 seconds

```python
action = wait.until(expected_conditions.element_to_be_clickable((By.NAME, 'Passwd')))
```

**What happens:**
```
1. Start timer (10 seconds)
2. Check: Is element present?
3. Check: Is element visible?
4. Check: Is element enabled?
5. Check: Is element clickable?
6. If any check fails → Wait 500ms → Repeat
7. If all pass → Return element
8. If timeout → Throw TimeoutException
```

**Common Expected Conditions:**
```python
from selenium.webdriver.support import expected_conditions as EC

# Element checks
EC.presence_of_element_located((By.ID, "id"))
EC.visibility_of_element_located((By.ID, "id"))
EC.element_to_be_clickable((By.ID, "id"))

# State checks
EC.title_is("Expected Title")
EC.title_contains("Partial Title")
EC.url_contains("example.com")

# Alert checks
EC.alert_is_present()

# Custom conditions
EC.text_to_be_present_in_element((By.ID, "id"), "text")
```

---

# PART 3: ADVANCED TECHNIQUES

## Chapter 7: Complex User Interactions

### 7.1 ActionChains Introduction

**What is ActionChains?**
- Advanced user interaction API
- Simulates complex mouse/keyboard actions
- Builds action sequences

### 7.2 Mouse Actions

**Right Click:**
**FILE: complex-element(Right_Click).py**
```python
from selenium import webdriver
from selenium.webdriver import ActionChains
from selenium.webdriver.common.by import By
from selenium.webdriver.firefox.service import Service
from webdriver_manager.firefox import GeckoDriverManager
import time

driver = webdriver.Firefox(service=Service(GeckoDriverManager().install()))
driver.get('https://alnafi.com/courses')
driver.maximize_window()
driver.implicitly_wait(5)

my_path = driver.find_element(By.XPATH, '/html/body/div[1]/div/div[4]/div/div[2]/div[2]/div[2]/div/div[1]/div/a/div/div/div[2]/div/div[1]/div[2]')

actions = ActionChains(driver)
actions.context_click(my_path).perform()

time.sleep(5)
driver.quit()
```

**Double Click:**
```python
actions.double_click(my_path).perform()
```

**📝 ACTIONCHAINS EXPLAINED:**

```python
actions = ActionChains(driver)
```
- Creates action builder
- Stores action sequence
- Executes on `.perform()`

```python
actions.context_click(my_path).perform()
```
**Step-by-step:**
```
1. Move mouse to element
2. Perform right-click
3. Trigger context menu
```

**ActionChains Methods:**
```python
# Mouse actions
actions.click(element)                    # Left click
actions.context_click(element)            # Right click
actions.double_click(element)             # Double click
actions.click_and_hold(element)           # Press and hold
actions.release(element)                  # Release held button

# Mouse movement
actions.move_to_element(element)          # Hover
actions.move_by_offset(x, y)              # Move cursor
actions.drag_and_drop(source, target)     # Drag & drop

# Chaining actions
actions.click(element1).pause(1).click(element2).perform()
```

### 7.3 Drag and Drop

**FILE: drag_slider_range.py**
```python
from selenium import webdriver
from selenium.webdriver import ActionChains
from selenium.webdriver.common.by import By
from selenium.webdriver.firefox.service import Service
from webdriver_manager.firefox import GeckoDriverManager
import time

driver = webdriver.Firefox(service=Service(GeckoDriverManager().install()))
driver.get("https://www.flipkart.com/clothing-and-accessories/pr?sid=clo&otracker=categorytree&p%5B%5D=facets.ideal_for%255B%255D%3DMen&otracker=nmenu_sub_Men_0_Clothing")
driver.maximize_window()
driver.implicitly_wait(5)

time.sleep(3)

actions = ActionChains(driver)
slider_bar = driver.find_element(By.XPATH, '/html/body/div/div/div[3]')
actions.drag_and_drop_by_offset(slider_bar, -50, 0).perform()

time.sleep(5)
driver.quit()
```

**drag_and_drop_by_offset():**
```python
actions.drag_and_drop_by_offset(element, x_offset, y_offset)
```
- **element:** Source element to drag
- **x_offset:** Horizontal movement (pixels)
  - Positive = right
  - Negative = left
- **y_offset:** Vertical movement (pixels)
  - Positive = down
  - Negative = up

**Example:**
```python
# Move slider 50 pixels left
actions.drag_and_drop_by_offset(slider, -50, 0).perform()

# Move element 100 pixels right, 50 down
actions.drag_and_drop_by_offset(element, 100, 50).perform()
```

### 7.4 Mouse Hover Effects

**FILE: mouse-over-effect.py**
```python
from selenium import webdriver
from selenium.webdriver import ActionChains
from selenium.webdriver.common.by import By
from selenium.webdriver.firefox.service import Service
from webdriver_manager.firefox import GeckoDriverManager
import time

driver = webdriver.Firefox(service=Service(GeckoDriverManager().install()))
driver.get('https://www.shwapno.com/?srsltid=AfmBOoqkFd6tXqsEy4Pn35wwyik70EH0KSdbqxAJHUthwvUhi_DTC9uU&msid=mhqf1wdoixs5qs6')
driver.maximize_window()
driver.implicitly_wait(5)

time.sleep(3)

menu_bar = driver.find_element(By.XPATH, '/html/body/header/div[2]/div/div[1]/div[2]/ul/li[7]/a')
actions = ActionChains(driver)
actions.move_to_element(menu_bar).perform()

time.sleep(2)

pop_menu = driver.find_element(By.XPATH, '/html/body/header/div[2]/div/div[1]/div[2]/ul/li[7]/ul/li[3]/a')
driver.execute_script("arguments[0].click();", pop_menu)

time.sleep(5)
driver.quit()
```

**Pattern:**
```python
# Step 1: Hover over parent menu
actions.move_to_element(menu_bar).perform()

# Step 2: Wait for dropdown to appear
time.sleep(2)

# Step 3: Click dropdown item
pop_menu = driver.find_element(...)
driver.execute_script("arguments[0].click();", pop_menu)
```

**Why JavaScript click?**
```python
# Regular click may fail if element moves
pop_menu.click()  # May throw ElementNotInteractableException

# JavaScript click bypasses visibility checks
driver.execute_script("arguments[0].click();", pop_menu)  # Always works
```

---

## Chapter 8: Alerts, Iframes, Windows

### 8.1 Alert Handling

**FILE: Alert_handeling.py**
```python
import time
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.firefox.service import Service
from selenium.webdriver.common.alert import Alert
from webdriver_manager.firefox import GeckoDriverManager

driver = webdriver.Firefox(service=Service(GeckoDriverManager().install()))

driver.get('https://mail.rediff.com/cgi-bin/login.cgi')
driver.maximize_window()
driver.implicitly_wait(10)

driver.find_element(By.XPATH, '/html/body/div[2]/div[1]/div/div[2]/div[2]/form/button').click()
alert_handle = Alert(driver)

print(alert_handle.text)
time.sleep(5)
alert_handle.accept()
time.sleep(5)
driver.quit()
```

**📝 ALERT HANDLING EXPLAINED:**

```python
from selenium.webdriver.common.alert import Alert
```
- **Purpose:** Import Alert class for popup handling
- **Why needed:** JavaScript alerts require special handling
- **Types handled:** alert(), confirm(), prompt()

```python
driver.find_element(By.XPATH, '...').click()
```
- Triggers JavaScript alert by clicking login without credentials

```python
alert_handle = Alert(driver)
```
- **Creates Alert object** to interact with popup
- **Must do this** before accessing alert properties

```python
print(alert_handle.text)
```
- **Gets alert message text**
- Output: "Please enter a valid user name"

```python
alert_handle.accept()
```
- **Clicks OK button** on alert
- Equivalent to user clicking OK

**Alert Methods:**
```python
# Get alert text
alert_text = alert_handle.text

# Accept alert (OK button)
alert_handle.accept()

# Dismiss alert (Cancel button)
alert_handle.dismiss()

# Send text to prompt
alert_handle.send_keys("My input text")
```

**Three Types of JavaScript Popups:**

**1. Alert (Information):**
```javascript
alert("This is a message");
```
```python
alert = Alert(driver)
print(alert.text)
alert.accept()  # Only option
```

**2. Confirm (Yes/No):**
```javascript
confirm("Are you sure?");
```
```python
alert = Alert(driver)
alert.accept()   # Click OK
# OR
alert.dismiss()  # Click Cancel
```

**3. Prompt (Input):**
```javascript
prompt("Enter your name:");
```
```python
alert = Alert(driver)
alert.send_keys("John Doe")
alert.accept()
```

---

### 8.2 Iframe Handling

**FILE: iframe.py**
```python
import time
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.firefox.service import Service
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from webdriver_manager.firefox import GeckoDriverManager

driver = webdriver.Firefox(service=Service(GeckoDriverManager().install()))

driver.get('https://www.rediff.com/')
driver.maximize_window()
driver.implicitly_wait(10)

driver.switch_to.frame("moneyiframe")
my_nse = driver.find_element(By.XPATH, '//*[@id="nseindex"]')
print(my_nse.text)

time.sleep(2)
driver.quit()
```

**📝 IFRAME DEEP DIVE:**

**What are Iframes?**
- **iframe** = "inline frame"
- Embeds another HTML page within current page
- Separate DOM (Document Object Model)
- Cannot access directly without switching

**HTML Structure:**
```html
<html>
  <body>
    <div>Main Page Content</div>
    
    <iframe id="moneyiframe" src="money.html">
      <!-- This content is in separate document -->
      <div id="nseindex">NSE: 18,500</div>
    </iframe>
  </body>
</html>
```

```python
driver.switch_to.frame("moneyiframe")
```
**What happens:**
1. Selenium context switches to iframe
2. Now you're "inside" the iframe's DOM
3. Can access iframe elements
4. Cannot access main page elements (until switch back)

**Three Ways to Switch to Iframe:**

```python
# Method 1: By index (position on page)
driver.switch_to.frame(0)  # First iframe
driver.switch_to.frame(1)  # Second iframe

# Method 2: By name or ID
driver.switch_to.frame("moneyiframe")
driver.switch_to.frame("frameId")

# Method 3: By WebElement
iframe_element = driver.find_element(By.ID, "moneyiframe")
driver.switch_to.frame(iframe_element)
```

```python
driver.switch_to.default_content()
```
- **Switch back to main page**
- Must do this to access main page elements again

**Complete Iframe Workflow:**
```python
# Start on main page
main_element = driver.find_element(By.ID, "main-content")

# Switch to iframe
driver.switch_to.frame("myframe")

# Access iframe elements
iframe_element = driver.find_element(By.ID, "iframe-content")

# Switch back to main page
driver.switch_to.default_content()

# Can access main page again
main_element2 = driver.find_element(By.ID, "footer")
```

**Nested Iframes:**
```python
# Switch to parent iframe
driver.switch_to.frame("parent-frame")

# Switch to child iframe (inside parent)
driver.switch_to.frame("child-frame")

# Go back one level
driver.switch_to.parent_frame()  # Now in parent-frame

# Go to main page
driver.switch_to.default_content()  # Now in main page
```

---

### 8.3 Window & Tab Management

**FILE: tab_handling.py**
```python
import time
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.firefox.service import Service
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from webdriver_manager.firefox import GeckoDriverManager

driver = webdriver.Firefox(service=Service(GeckoDriverManager().install()))

driver.get('https://alnafi.com/')
driver.maximize_window()

wait = WebDriverWait(driver, 10)

linkedin_link = wait.until(EC.element_to_be_clickable(
    (By.XPATH, "/html/body/div[1]/div/div[5]/div/div[3]/div[2]/a[4]")))
linkedin_link.click()

time.sleep(2)

wins = driver.window_handles
print(f"Total windows: {len(wins)}")
print(f"Window 0 (alnafi.com): {wins[0]}")
print(f"Window 1 (linkedin.com): {wins[1]}")
time.sleep(3)

# Switch to alnafi
driver.switch_to.window(wins[0])
print(f"Tab 0 Title: {driver.title}")
time.sleep(2)

# Switch to LinkedIn
driver.switch_to.window(wins[1])
print(f"Tab 1 Title: {driver.title}")

time.sleep(5)
driver.quit()
```

**📝 WINDOW MANAGEMENT EXPLAINED:**

**Window vs Tab:**
- In Selenium, **windows and tabs are the same thing**
- Both called "window handles"
- API doesn't distinguish between them

```python
wins = driver.window_handles
```
- **Returns list of all open windows/tabs**
- Each window has unique handle (ID)
- Format: List of strings

**Example output:**
```python
['CDwindow-E4F3A5B2C1D6F7A8', 'CDwindow-B8D2E9F1A3C5D7E9']
```

```python
print(f"Total windows: {len(wins)}")
```
- Counts number of open windows/tabs

```python
driver.switch_to.window(wins[0])
```
- **Switch to specific window by handle**
- wins[0] = First window (original)
- wins[1] = Second window (newly opened)

```python
print(f"Tab 0 Title: {driver.title}")
```
- **Gets title of CURRENT window**
- Must switch to window first

**Complete Window Workflow:**

```python
# Open first page
driver.get("https://alnafi.com")
print(f"Windows open: {len(driver.window_handles)}")  # 1

# Click link that opens new tab
driver.find_element(By.LINK_TEXT, "LinkedIn").click()
time.sleep(2)
print(f"Windows open: {len(driver.window_handles)}")  # 2

# Get all window handles
windows = driver.window_handles
original_window = windows[0]
new_window = windows[1]

# Switch to new window
driver.switch_to.window(new_window)
print(f"Current title: {driver.title}")  # LinkedIn title

# Switch back to original
driver.switch_to.window(original_window)
print(f"Current title: {driver.title}")  # Alnafi title

# Close current window only
driver.close()

# Close all windows
driver.quit()
```

**Open New Tab Programmatically:**
```python
# Method 1: JavaScript
driver.execute_script("window.open('');")

# Method 2: Open with URL
driver.execute_script("window.open('https://google.com', '_blank');")

# Switch to new tab
driver.switch_to.window(driver.window_handles[-1])
```

**Close vs Quit:**
```python
driver.close()  # Closes CURRENT window only
driver.quit()   # Closes ALL windows + ends session
```

---

## Chapter 9: Screenshot Capabilities

### 9.1 Basic Screenshots

**FILE: screenshot.py**
```python
import time
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.firefox.service import Service
from webdriver_manager.firefox import GeckoDriverManager

driver = webdriver.Firefox(service=Service(GeckoDriverManager().install()))

driver.get("https://www.alnafi.com/")
driver.maximize_window()
driver.implicitly_wait(5)

time.sleep(0.4)

# Method 1: save_screenshot()
driver.save_screenshot("mylogin.png")

# Method 2: get_screenshot_as_file()
driver.get_screenshot_as_file('./screenshot/mylogin3.png')

# Method 3: Element screenshot
my_section = driver.find_element(By.XPATH, '/html/body/div[1]/div/div[4]/div[10]/div/img')
my_section.screenshot('visa5.png')

time.sleep(2)
driver.quit()
```

**📝 SCREENSHOT METHODS:**

**1. save_screenshot():**
```python
driver.save_screenshot("page.png")
```
- Saves in current working directory
- Simple and direct
- Returns True/False

**2. get_screenshot_as_file():**
```python
driver.get_screenshot_as_file('./screenshots/page.png')
```
- Can specify path
- Better for organized structure
- Returns True/False

**3. get_screenshot_as_png():**
```python
png_bytes = driver.get_screenshot_as_png()
```
- Returns binary data
- Useful for in-memory processing
- Can save manually

**4. Element screenshot:**
```python
element = driver.find_element(By.ID, "logo")
element.screenshot("logo.png")
```
- Captures specific element only
- Introduced in Selenium 4
- Useful for focused captures

---

### 9.2 Dynamic Screenshot Naming

**FILE: screenshot-2.py**
```python
import time as t
from datetime import *
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.firefox.service import Service
from webdriver_manager.firefox import GeckoDriverManager

driver = webdriver.Firefox(service=Service(GeckoDriverManager().install()))

driver.get("https://alnafi.com/auth/sign-in")
driver.maximize_window()
driver.implicitly_wait(5)

t.sleep(0.4)
day = date.today()
date_time = datetime.now()
date_format = day.strftime("%B_%d_%Y")
time_format = date_time.strftime("%I_%M_%p")
myfile = "Screenshot__" + date_format + "_" + time_format + ".png"

my_email = driver.find_element(By.XPATH, "/html/body/div[1]/div/div[2]/div[1]/div/form/div[1]/div/div/input")
my_pass = driver.find_element(By.XPATH, "/html/body/div[1]/div/div[2]/div[1]/div/form/div[2]/div/div/input")

driver.execute_script("arguments[0].setAttribute('style','background: yellow; border:2px solid red;');", my_email)
driver.execute_script("arguments[0].setAttribute('style','background: yellow; border:2px solid red;');", my_pass)

# Save with dynamic name
driver.get_screenshot_as_file('./screenshot//' + myfile)
driver.get_screenshot_as_file(r"C:\Users\User\Desktop\\" + myfile)

driver.close()
driver.quit()
```

**📝 ADVANCED SCREENSHOT TECHNIQUES:**

**Dynamic Naming:**
```python
from datetime import datetime

date_format = day.strftime("%B_%d_%Y")       # December_22_2025
time_format = date_time.strftime("%I_%M_%p") # 02_30_PM
myfile = f"Screenshot__{date_format}_{time_format}.png"
```

**Why dynamic naming?**
- Unique filenames (no overwriting)
- Timestamp tracking
- Better organization
- Debugging made easier

**Element Highlighting:**
```python
driver.execute_script(
    "arguments[0].setAttribute('style','background: yellow; border:2px solid red;');",
    my_email
)
```

**What this does:**
1. Uses JavaScript to modify element style
2. Adds yellow background
3. Adds red border (2px solid)
4. Makes element visible in screenshot
5. Great for debugging and reports

---

### 9.3 Function-Based Screenshots

**FILE: screenshot-3.py**
```python
import time as t
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.firefox.service import Service
from webdriver_manager.firefox import GeckoDriverManager

driver = webdriver.Firefox(service=Service(GeckoDriverManager().install()))

driver.get("https://alnafi.com/auth/sign-in")
driver.maximize_window()
driver.implicitly_wait(5)

def my_file_sc(driver):
    file_name = t.asctime().replace(":", "_") + ".png"
    driver.save_screenshot(file_name)

t.sleep(5)
my_email = driver.find_element(By.XPATH, "/html/body/div[1]/div/div[2]/div[1]/div/form/div[1]/div/div/input")
my_pass = driver.find_element(By.XPATH, "/html/body/div[1]/div/div[2]/div[1]/div/form/div[2]/div/div/input")

driver.execute_script("arguments[0].setAttribute('style','background: yellow; border:2px solid red;');", my_email)
driver.execute_script("arguments[0].setAttribute('style','background: yellow; border:2px solid red;');", my_pass)

my_file_sc(driver)

driver.close()
driver.quit()
```

**📝 REUSABLE SCREENSHOT FUNCTION:**

```python
def my_file_sc(driver):
    file_name = t.asctime().replace(":", "_") + ".png"
    driver.save_screenshot(file_name)
```

**Breakdown:**
```python
t.asctime()  # Returns: 'Mon Dec 22 14:30:45 2025'
.replace(":", "_")  # Replace colons (invalid in Windows filenames)
# Result: 'Mon Dec 22 14_30_45 2025.png'
```

**Why functions?**
- Reusable code
- Consistent naming
- Easy to maintain
- Can add error handling

**Enhanced version:**
```python
import os
import time as t

def my_file_sc(driver, folder="screenshots"):
    # Create folder if doesn't exist
    os.makedirs(folder, exist_ok=True)
    
    # Generate filename
    file_name = t.asctime().replace(":", "_") + ".png"
    file_path = os.path.join(folder, file_name)
    
    # Take screenshot
    driver.save_screenshot(file_path)
    print(f"Screenshot saved: {file_path}")
    return file_path
```

---

### 9.4 Full-Page Screenshots

**FILE: screenshot_full_page.py**
```python
import os
import time as t
from selenium import webdriver
from selenium.webdriver.firefox.service import Service
from webdriver_manager.firefox import GeckoDriverManager

driver = webdriver.Firefox(service=Service(GeckoDriverManager().install()))

driver.get("https://alnafi.com/")
driver.maximize_window()
driver.implicitly_wait(5)

def my_file_sc(driver):
    my_path = os.getcwd() + "\\"
    file_name = my_path + t.asctime().replace(":", "_") + ".png"
    driver.save_screenshot(file_name)

t.sleep(5)

# Get full page dimensions
total_width = driver.execute_script("return document.body.scrollWidth")
total_height = driver.execute_script("return document.body.scrollHeight")
print(total_width, total_height)

# Resize window to full page size
driver.set_window_size(total_width, total_height)

t.sleep(0.5)
my_file_sc(driver)

driver.close()
driver.quit()
```

**📝 FULL-PAGE SCREENSHOT TECHNIQUE:**

**The Problem:**
- Normal screenshots only capture visible viewport
- Long pages get cut off
- Scrollable content missed

**The Solution:**
```python
total_width = driver.execute_script("return document.body.scrollWidth")
total_height = driver.execute_script("return document.body.scrollHeight")
```

**What this does:**
- `scrollWidth`: Total page width (including overflow)
- `scrollHeight`: Total page height (including scrolled content)

```python
driver.set_window_size(total_width, total_height)
```
- Resizes browser to exact page dimensions
- Now viewport = entire page
- Screenshot captures everything

**Current Working Directory:**
```python
my_path = os.getcwd() + "\\"
```
- `getcwd()`: Get Current Working Directory
- Adds backslash for Windows path
- Ensures screenshot saves in project folder

---

## Chapter 10: Element Validation

### 10.1 Check Element Existence

**FILE: is_elements.py**
```python
import time
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.firefox.service import Service
from webdriver_manager.firefox import GeckoDriverManager

def is_element_present(tag_name):
    try:
        driver = webdriver.Firefox(service=Service(GeckoDriverManager().install()))
        driver.get("https://www.alnafi.com/")
        driver.maximize_window()
        
        a_tag = driver.find_element(By.TAG_NAME, tag_name)
        return True
    except:
        return False

print(is_element_present('a'))  # True - Links exist
```

**📝 ELEMENT VALIDATION:**

**Why check if element exists?**
- Prevent NoSuchElementException
- Conditional logic in tests
- Dynamic page content
- Better error handling

**Method 1: Try-Except:**
```python
def is_element_present(locator_type, locator_value):
    try:
        driver.find_element(locator_type, locator_value)
        return True
    except:
        return False
```

**Method 2: find_elements (Better!):**

**FILE: is_elements-2.py**
```python
def is_element_present(att, abd):
    if len(driver.find_elements(by=att, value=abd)) == 0:
        return False
    else:
        return True

print(is_element_present(By.XPATH, 'saleemali'))  # False
print(is_element_present(By.TAG_NAME, 'a'))       # True
print(is_element_present(By.TAG_NAME, 'div'))     # True
```

**Why find_elements() is better:**
```python
# find_element() - Throws exception
element = driver.find_element(By.ID, "nonexistent")  # ❌ Error!

# find_elements() - Returns empty list
elements = driver.find_elements(By.ID, "nonexistent")  # ✅ Returns []
if len(elements) > 0:
    # Element exists
else:
    # Element doesn't exist
```

**Production-Ready Version:**
```python
def is_element_present(driver, locator_type, locator_value, timeout=0):
    """
    Check if element exists on page
    
    Args:
        driver: WebDriver instance
        locator_type: By.ID, By.XPATH, etc.
        locator_value: Locator string
        timeout: Optional wait time
    
    Returns:
        bool: True if element found, False otherwise
    """
    if timeout > 0:
        driver.implicitly_wait(timeout)
    
    elements = driver.find_elements(locator_type, locator_value)
    
    # Reset implicit wait
    driver.implicitly_wait(0)
    
    return len(elements) > 0
```

---

## Chapter 11: Browser Options & Configuration

### 11.1 Headless Mode

**FILE: options.py (Firefox)**
```python
import time
from selenium import webdriver
from selenium.webdriver.firefox.options import Options
from selenium.webdriver.firefox.service import Service
from webdriver_manager.firefox import GeckoDriverManager

firefox_options = Options()
firefox_options.headless = True

driver = webdriver.Firefox(service=Service(GeckoDriverManager().install()), options=firefox_options)

driver.get("https://www.alnafi.com")
driver.maximize_window()
driver.implicitly_wait(5)
print(driver.title)

time.sleep(2)
driver.quit()
```

**FILE: options-2.py (Chrome)**
```python
from selenium.webdriver.chrome.options import Options

chrome_options = Options()
chrome_options.add_argument("--headless")

driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()), options=chrome_options)
```

**📝 HEADLESS MODE EXPLAINED:**

**What is Headless?**
- Browser runs without GUI
- No visible window
- Background execution
- Perfect for servers/CI/CD

**Why use headless?**
✅ Faster execution (no rendering)
✅ Less resource usage
✅ CI/CD compatible
✅ Server environments (no display)
✅ Parallel execution (more instances)

**Firefox Headless:**
```python
firefox_options = Options()
firefox_options.headless = True
```

**Chrome Headless:**
```python
chrome_options = Options()
chrome_options.add_argument("--headless")
chrome_options.add_argument("--no-sandbox")
chrome_options.add_argument("--disable-dev-shm-usage")
```

**Common Options:**

**Chrome:**
```python
options = Options()
options.add_argument("--start-maximized")
options.add_argument("--incognito")
options.add_argument("--disable-extensions")
options.add_argument("--disable-gpu")
options.add_argument("--no-sandbox")
options.add_argument("--disable-dev-shm-usage")
options.add_argument("user-agent=Mozilla/5.0...")

# Disable images (faster loading)
prefs = {"profile.managed_default_content_settings.images": 2}
options.add_experimental_option("prefs", prefs)
```

**Firefox:**
```python
options = Options()
options.headless = True
options.add_argument("--width=1920")
options.add_argument("--height=1080")

# Set preferences
options.set_preference("browser.download.folderList", 2)
options.set_preference("browser.download.dir", "/downloads")
```

---

## Chapter 12: Web Scraping Integration

**FILE: scraping.py**
```python
import requests
from bs4 import BeautifulSoup

# Send GET request
response = requests.get("https://example.com")
print(response.status_code)  # 200 = success

# Parse HTML
soup = BeautifulSoup(response.text, 'html.parser')
print(soup.prettify())

# Extract title
title = soup.title.string
print("Page Title:", title)

# Find all links
links = soup.find_all('a')
for link in links:
    print(link.get('href'))
```

**📝 SELENIUM + BEAUTIFULSOUP:**

**Why combine them?**
- **Selenium:** Handles JavaScript, dynamic content
- **BeautifulSoup:** Faster HTML parsing
- **Together:** Best of both worlds

**Complete Workflow:**
```python
from selenium import webdriver
from bs4 import BeautifulSoup

# Use Selenium to load dynamic page
driver = webdriver.Chrome(service=service)
driver.get("https://dynamic-website.com")
driver.implicitly_wait(5)

# Get page source after JavaScript execution
page_source = driver.page_source

# Parse with BeautifulSoup
soup = BeautifulSoup(page_source, 'html.parser')

# Extract data
products = soup.find_all('div', class_='product')
for product in products:
    name = product.find('h2').text
    price = product.find('span', class_='price').text
    print(f"{name}: {price}")

driver.quit()
```

**Real-World Example: Task.py**
```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.firefox.service import Service
from webdriver_manager.firefox import GeckoDriverManager
import time

driver = webdriver.Firefox(service=Service(GeckoDriverManager().install()))

driver.get("https://www.wikipedia.org/")
driver.maximize_window()

# Find all language options
options_tag = driver.find_elements(By.TAG_NAME, "option")

for i in options_tag:
    print("Text is", i.text, "The language is", i.get_attribute("lang"))

print(f"Total languages: {len(options_tag)}")

driver.quit()
```

**Scraping Best Practices:**
```python
# 1. Respectful scraping
import time
time.sleep(1)  # Delay between requests

# 2. User agent
options.add_argument("user-agent=Mozilla/5.0 (Windows NT 10.0; Win64; x64)")

# 3. Error handling
try:
    element = driver.find_element(By.ID, "content")
except:
    print("Element not found")

# 4. Robots.txt compliance
# Check: https://website.com/robots.txt
```

---

# PART 4: SELENIUM GRID - DEVOPS LEVEL

## Chapter 13: Selenium Grid Architecture

### 13.1 What is Selenium Grid?

**Selenium Grid** is a distributed testing infrastructure that allows you to run tests on multiple machines and browsers simultaneously.

**Grid 4 Architecture:**
```
                    ┌─────────────────────┐
                    │   TEST SCRIPTS      │
                    │  (Your Code)        │
                    └──────────┬──────────┘
                               │
                    ┌──────────▼──────────┐
                    │     GRID HUB        │
                    │  (Coordinator)      │
                    │  Port: 4444         │
                    │                     │
                    │  ├─ Session Mgmt    │
                    │  ├─ Load Balancing  │
                    │  └─ Node Registry   │
                    └──┬─────────┬────────┘
                       │         │
         ┌─────────────┴──┐   ┌──┴─────────────┐
         │                │   │                │
    ┌────▼─────┐   ┌─────▼────┐   ┌──────────▼───┐
    │  NODE 1  │   │  NODE 2  │   │    NODE 3    │
    │ (Chrome) │   │(Firefox) │   │   (Edge)     │
    │          │   │          │   │              │
    │  Port:   │   │  Port:   │   │   Port:      │
    │  5555    │   │  5556    │   │   5557       │
    └──────────┘   └──────────┘   └──────────────┘
```

### 13.2 Hub-Node Model

**HUB (Router/Session Map):**
- Central coordinator
- Receives test requests
- Routes to available nodes
- Manages session queues
- Load balancing
- **Port:** 4444 (default)

**NODE (Browser Executor):**
- Executes tests on browsers
- Registers with Hub
- Reports capabilities
- Runs browser instances
- **Port:** 5555+ (dynamic)

**Communication Flow:**
```
1. Test script → Hub: "Need Chrome browser"
2. Hub → Checks available nodes with Chrome
3. Hub → Assigns Node 1
4. Hub → Test script: "Use Node 1"
5. Test script ↔ Node 1: Execute tests
6. Node 1 → Hub: "Session complete"
7. Hub: Mark Node 1 as available
```

### 13.3 Grid 4 Components

**1. Router:**
- Entry point for all requests
- Routes to appropriate component
- Port 4444

**2. Distributor:**
- Manages node registration
- Creates new sessions
- Load balancing

**3. Session Map:**
- Tracks active sessions
- Maps session ID to node

**4. Session Queue:**
- Queues requests when nodes busy
- FIFO (First In First Out)

**5. Event Bus:**
- Internal communication
- Pub/sub messaging
- Default ports: 4442, 4443

---

## Chapter 14: Grid Setup & Configuration

### 14.1 Prerequisites

**Required Software:**
```
1. Java 11 or higher
   Download: https://www.oracle.com/java/technologies/downloads/

2. Selenium Server JAR (Grid)
   File: selenium-server-4.38.0.jar
   Download: https://github.com/SeleniumHQ/selenium/releases

3. Browser Drivers (auto-detected or manual)
   - chromedriver.exe
   - geckodriver.exe
   - msedgedriver.exe
```

**Verify Java:**
```bash
java -version
# Output: java version "11.0.x" or higher
```

### 14.2 Start Selenium Grid Hub

**Command:**
```bash
java -jar selenium-server-4.38.0.jar hub
```

**Expected Output:**
```
INFO [Standalone.execute] - Started Selenium Standalone
INFO [Hub.execute] - Started Hub
INFO [Hub.execute] - Selenium Grid hub is up and running on http://localhost:4444
```

**Access Grid Console:**
```
http://localhost:4444/ui
```

**What you'll see:**
- Grid status (active/inactive)
- Connected nodes (0 initially)
- Session queue
- Grid capabilities

### 14.3 Start Selenium Grid Node

**Open NEW terminal** (keep Hub running in first terminal)

**Command (Auto-detect drivers):**
```bash
java -jar selenium-server-4.38.0.jar node --detect-drivers true --publish-events tcp://localhost:4442 --subscribe-events tcp://localhost:4443
```

**Expected Output:**
```
INFO [NodeServer.execute] - Started Selenium Node
INFO [Node.execute] - Detected browsers: Chrome, Firefox, Edge
INFO [Node.execute] - Announcing node to http://localhost:4444
INFO [Node.execute] - Node registration successful
```

**For Remote Machine (Different IP):**
```bash
java -jar selenium-server-4.38.0.jar node --detect-drivers true --publish-events tcp://10.0.2.1:4442 --subscribe-events tcp://10.0.2.1:4443 --hub http://10.0.2.1:4444
```

**Your IP = 10.0.2.1** (from your code)

### 14.4 Command Breakdown

```bash
java -jar selenium-server-4.38.0.jar node
```
- Starts Grid in Node mode

```bash
--detect-drivers true
```
- Auto-detects chromedriver, geckodriver, msedgedriver
- Scans PATH environment variable
- No manual driver configuration needed

```bash
--publish-events tcp://localhost:4442
```
- Node publishes events to Hub
- Port 4442 = Event Bus publish port

```bash
--subscribe-events tcp://localhost:4443
```
- Node subscribes to Hub events
- Port 4443 = Event Bus subscribe port

```bash
--hub http://10.0.2.1:4444
```
- Specify Hub URL (for remote nodes)
- Default: http://localhost:4444

**Additional Useful Flags:**
```bash
--max-sessions 10          # Max concurrent sessions per node
--session-timeout 300      # Session timeout (seconds)
--port 5555               # Custom node port
--log-level INFO          # Logging level
--enable-managed-downloads true  # Download file handling
```

---

## Chapter 15: Grid Test Implementation

### 15.1 Remote WebDriver Test

**FILE: selenium_grid_test.py**
```python
import time
from selenium import webdriver
from selenium.webdriver.chrome.options import Options as ChromeOptions

hub_url = "http://10.0.2.1:4444/wd/hub"

# Define browser options
chrome_options = ChromeOptions()

# Create Remote driver
driver = webdriver.Remote(
    command_executor=hub_url,
    options=chrome_options
)

driver.get("https://google.com")
driver.maximize_window()
driver.implicitly_wait(5)
print(driver.title)

time.sleep(5)
driver.quit()
```

**📝 LINE-BY-LINE BREAKDOWN:**

```python
hub_url = "http://10.0.2.1:4444/wd/hub"
```
- **Hub endpoint** for WebDriver requests
- **10.0.2.1** = Your Hub machine IP
- **4444** = Default Hub port
- **/wd/hub** = WebDriver endpoint path

```python
chrome_options = ChromeOptions()
```
- Creates Chrome-specific options
- Can add arguments, preferences
- Defines browser capabilities

```python
driver = webdriver.Remote(
    command_executor=hub_url,
    options=chrome_options
)
```
**This is the KEY difference!**
- **webdriver.Remote()** instead of webdriver.Chrome()
- Connects to Hub, not local browser
- Hub assigns available Chrome node
- Returns remote driver instance

**What happens behind the scenes:**
```
1. Test creates Remote WebDriver
2. Sends request to Hub: "Need Chrome"
3. Hub checks registered nodes
4. Hub finds Node with Chrome
5. Hub creates session on that Node
6. Hub returns session ID to test
7. Test controls remote browser via Hub
```

### 15.2 Multi-Browser Grid Testing

```python
import time
from selenium import webdriver
from selenium.webdriver.chrome.options import Options as ChromeOptions
from selenium.webdriver.firefox.options import Options as FirefoxOptions
from selenium.webdriver.edge.options import Options as EdgeOptions

hub_url = "http://localhost:4444/wd/hub"

def test_chrome():
    chrome_options = ChromeOptions()
    driver = webdriver.Remote(
        command_executor=hub_url,
        options=chrome_options
    )
    driver.get("https://google.com")
    print(f"Chrome - Title: {driver.title}")
    driver.quit()

def test_firefox():
    firefox_options = FirefoxOptions()
    driver = webdriver.Remote(
        command_executor=hub_url,
        options=firefox_options
    )
    driver.get("https://google.com")
    print(f"Firefox - Title: {driver.title}")
    driver.quit()

def test_edge():
    edge_options = EdgeOptions()
    driver = webdriver.Remote(
        command_executor=hub_url,
        options=edge_options
    )
    driver.get("https://google.com")
    print(f"Edge - Title: {driver.title}")
    driver.quit()

# Run all tests
test_chrome()
test_firefox()
test_edge()
```

### 15.3 Parallel Grid Execution

```python
from concurrent.futures import ThreadPoolExecutor
from selenium import webdriver
from selenium.webdriver.chrome.options import Options as ChromeOptions

hub_url = "http://localhost:4444/wd/hub"

def run_test(test_id):
    chrome_options = ChromeOptions()
    driver = webdriver.Remote(
        command_executor=hub_url,
        options=chrome_options
    )
    
    driver.get("https://google.com")
    print(f"Test {test_id} - Title: {driver.title}")
    
    driver.quit()
    return f"Test {test_id} completed"

# Run 10 tests in parallel
with ThreadPoolExecutor(max_workers=10) as executor:
    futures = [executor.submit(run_test, i) for i in range(1, 11)]
    
    for future in futures:
        print(future.result())
```

**This is THE POWER of Grid:**
- 10 tests running simultaneously
- 10 different browsers (or same browser, different instances)
- 10x faster than sequential execution
- Scales horizontally (add more nodes = more parallel tests)

---

## Chapter 16: Grid Best Practices

### 16.1 Production Configuration

**1. Dedicated Hub Machine:**
```
Hub Server (Minimum):
├── 2 CPU cores
├── 4 GB RAM
├── Java 11+
└── Stable network
```

**2. Multiple Node Machines:**
```
Node Server (Recommended per node):
├── 4 CPU cores
├── 8 GB RAM
├── 2-3 concurrent sessions max
├── Browser + driver installed
└── Low latency to Hub
```

**3. Network Configuration:**
```bash
# Hub firewall rules
Allow incoming: 4444 (WebDriver requests)
Allow incoming: 4442 (Event Bus publish)
Allow incoming: 4443 (Event Bus subscribe)

# Node firewall rules
Allow outgoing: 4444, 4442, 4443
```

### 16.2 Grid Monitoring

**1. Grid Console:**
```
http://localhost:4444/ui
```
- Real-time node status
- Active sessions
- Queue length
- Browser capabilities

**2. Grid Status API:**
```bash
curl http://localhost:4444/status
```

**Response:**
```json
{
  "ready": true,
  "message": "Selenium Grid ready",
  "nodes": [
    {
      "id": "node-1",
      "status": "UP",
      "maxSessions": 5,
      "sessions": [...]
    }
  ]
}
```

### 16.3 Error Handling in Grid

```python
from selenium import webdriver
from selenium.common.exceptions import WebDriverException
import time

hub_url = "http://localhost:4444/wd/hub"
max_retries = 3

def create_driver_with_retry():
    for attempt in range(max_retries):
        try:
            chrome_options = ChromeOptions()
            driver = webdriver.Remote(
                command_executor=hub_url,
                options=chrome_options
            )
            print(f"✓ Connected to Grid (attempt {attempt + 1})")
            return driver
        except WebDriverException as e:
            print(f"✗ Attempt {attempt + 1} failed: {e}")
            if attempt < max_retries - 1:
                time.sleep(5)  # Wait before retry
            else:
                raise Exception("Failed to connect to Grid after retries")

# Use it
driver = create_driver_with_retry()
driver.get("https://example.com")
driver.quit()
```

### 16.4 Grid Scaling Strategies

**Horizontal Scaling (Add More Nodes):**
```bash
# Start multiple nodes on same machine
java -jar selenium-server-4.38.0.jar node --port 5555 &
java -jar selenium-server-4.38.0.jar node --port 5556 &
java -jar selenium-server-4.38.0.jar node --port 5557 &
```

**Vertical Scaling (More Sessions per Node):**
```bash
java -jar selenium-server-4.38.0.jar node --max-sessions 10
```

**Cloud Grid (Docker):**
```yaml
# docker-compose.yml
version: "3"
services:
  selenium-hub:
    image: selenium/hub:4.38.0
    ports:
      - "4444:4444"
  
  chrome:
    image: selenium/node-chrome:4.38.0
    depends_on:
      - selenium-hub
    environment:
      - SE_EVENT_BUS_HOST=selenium-hub
      - SE_EVENT_BUS_PUBLISH_PORT=4442
      - SE_EVENT_BUS_SUBSCRIBE_PORT=4443
  
  firefox:
    image: selenium/node-firefox:4.38.0
    depends_on:
      - selenium-hub
    environment:
      - SE_EVENT_BUS_HOST=selenium-hub
      - SE_EVENT_BUS_PUBLISH_PORT=4442
      - SE_EVENT_BUS_SUBSCRIBE_PORT=4443
```

```bash
docker-compose up -d
```

---

## Chapter 17: Security Best Practices

### 17.1 Credential Management

**NEVER do this:**
```python
# ❌ CRITICAL SECURITY VIOLATION
username = "admin@example.com"
password = "MyPassword123"
driver.find_element(By.ID, "password").send_keys(password)
```

**ALWAYS do this:**
```python
# ✅ SECURE APPROACH
from dotenv import load_dotenv
import os

load_dotenv()
username = os.getenv('USERNAME')
password = os.getenv('PASSWORD')

driver.find_element(By.ID, "username").send_keys(username)
driver.find_element(By.ID, "password").send_keys(password)
```

**.env file:**
```
USERNAME=admin@example.com
PASSWORD=MySecurePassword123!
API_KEY=your_api_key_here
```

**.gitignore (CRITICAL):**
```
.env
*password*
*credentials*
secrets.json
config_prod.py
```

### 17.2 Screenshot Security

```python
# ❌ Screenshots may contain sensitive data
driver.save_screenshot("login_page.png")  # Contains password field!

# ✅ Mask sensitive fields before screenshot
password_field = driver.find_element(By.ID, "password")
driver.execute_script(
    "arguments[0].value = '********';", 
    password_field
)
driver.save_screenshot("login_page.png")
```

### 17.3 Grid Security

**1. Authentication:**
```bash
# Basic auth for Grid Hub
java -jar selenium-server-4.38.0.jar hub \
  --username admin \
  --password securepassword
```

**2. HTTPS:**
```bash
# Use HTTPS for production
hub_url = "https://grid.yourdomain.com:4444/wd/hub"
```

**3. Network Security:**
- Run Grid on private network
- Use VPN for remote nodes
- Firewall rules (restrict ports)
- No public Grid exposure

---

## Chapter 18: CI/CD Integration

### 18.1 Jenkins Integration

**Jenkinsfile:**
```groovy
pipeline {
    agent any
    
    stages {
        stage('Setup') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        
        stage('Start Grid') {
            steps {
                sh 'java -jar selenium-server-4.38.0.jar hub &'
                sh 'java -jar selenium-server-4.38.0.jar node --detect-drivers true &'
                sleep 10  // Wait for Grid to start
            }
        }
        
        stage('Run Tests') {
            steps {
                sh 'python selenium_grid_test.py'
            }
        }
        
        stage('Stop Grid') {
            steps {
                sh 'pkill -f selenium-server'
            }
        }
    }
    
    post {
        always {
            archiveArtifacts artifacts: 'screenshots/**/*.png'
            junit 'test-results/*.xml'
        }
    }
}
```

### 18.2 GitHub Actions

**.github/workflows/selenium-tests.yml:**
```yaml
name: Selenium Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v2
    
    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: 3.9
    
    - name: Install dependencies
      run: |
        pip install -r requirements.txt
    
    - name: Start Selenium Grid
      run: |
        java -jar selenium-server-4.38.0.jar hub &
        java -jar selenium-server-4.38.0.jar node --detect-drivers true &
        sleep 10
    
    - name: Run tests
      run: |
        python selenium_grid_test.py
    
    - name: Upload screenshots
      if: always()
      uses: actions/upload-artifact@v2
      with:
        name: screenshots
        path: screenshots/
```

---

## Chapter 19: Real-World DevOps Applications

### 19.1 Automated Regression Testing

```python
import pytest
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.options import Options

@pytest.fixture
def driver():
    hub_url = "http://localhost:4444/wd/hub"
    chrome_options = Options()
    
    driver = webdriver.Remote(
        command_executor=hub_url,
        options=chrome_options
    )
    yield driver
    driver.quit()

def test_login(driver):
    driver.get("https://example.com/login")
    driver.find_element(By.ID, "username").send_keys("testuser")
    driver.find_element(By.ID, "password").send_keys("testpass")
    driver.find_element(By.ID, "submit").click()
    
    assert "Dashboard" in driver.title

def test_navigation(driver):
    driver.get("https://example.com")
    driver.find_element(By.LINK_TEXT, "About").click()
    
    assert "About" in driver.title

# Run with: pytest -v -n 10  # 10 parallel tests
```

### 19.2 Health Check Monitoring

```python
import schedule
import time
from selenium import webdriver
from selenium.webdriver.chrome.options import Options
import smtplib
from email.mime.text import MIMEText

def health_check():
    hub_url = "http://localhost:4444/wd/hub"
    chrome_options = Options()
    chrome_options.add_argument("--headless")
    
    try:
        driver = webdriver.Remote(
            command_executor=hub_url,
            options=chrome_options
        )
        
        driver.get("https://yourapp.com/health")
        status = driver.find_element(By.ID, "status").text
        
        if status != "OK":
            send_alert(f"Health check failed: {status}")
        
        driver.quit()
    except Exception as e:
        send_alert(f"Health check error: {e}")

def send_alert(message):
    msg = MIMEText(message)
    msg['Subject'] = 'Application Health Alert'
    msg['From'] = 'alerts@yourapp.com'
    msg['To'] = 'devops@yourapp.com'
    
    # Send email...

# Schedule every 5 minutes
schedule.every(5).minutes.do(health_check)

while True:
    schedule.run_pending()
    time.sleep(1)
```

### 19.3 Deployment Validation

```python
def validate_deployment(environment_url):
    """
    Validate deployment by running smoke tests
    Returns True if all tests pass
    """
    hub_url = "http://localhost:4444/wd/hub"
    chrome_options = Options()
    
    driver = webdriver.Remote(
        command_executor=hub_url,
        options=chrome_options
    )
    
    try:
        # Test 1: Homepage loads
        driver.get(environment_url)
        assert "Welcome" in driver.title
        
        # Test 2: Login works
        driver.get(f"{environment_url}/login")
        driver.find_element(By.ID, "username").send_keys("test")
        driver.find_element(By.ID, "password").send_keys("test")
        driver.find_element(By.ID, "submit").click()
        assert "Dashboard" in driver.title
        
        # Test 3: Critical API endpoint
        driver.get(f"{environment_url}/api/health")
        page_text = driver.find_element(By.TAG_NAME, "body").text
        assert "healthy" in page_text.lower()
        
        return True
    except Exception as e:
        print(f"Deployment validation failed: {e}")
        return False
    finally:
        driver.quit()

# Use in deployment pipeline
if validate_deployment("https://staging.yourapp.com"):
    print("✓ Deployment validated. Proceeding to production.")
else:
    print("✗ Deployment validation failed. Rollback triggered.")
    # Trigger rollback...
```

---

## Chapter 20: Troubleshooting Guide

### 20.1 Common Issues & Solutions

**Issue 1: Cannot connect to Grid Hub**
```python
WebDriverException: Message: invalid session id
```
**Solution:**
```bash
# Check Hub is running
curl http://localhost:4444/status

# Verify firewall allows port 4444
telnet localhost 4444

# Check Hub logs
java -jar selenium-server-4.38.0.jar hub --log-level FINE
```

**Issue 2: Node not registering**
```
Node failed to register to Hub
```
**Solution:**
```bash
# Check Hub URL is correct
--hub http://CORRECT_HUB_IP:4444

# Verify Event Bus ports
--publish-events tcp://HUB_IP:4442
--subscribe-events tcp://HUB_IP:4443

# Check drivers are detected
java -jar selenium-server-4.38.0.jar node --detect-drivers true --log-level INFO
```

**Issue 3: Element not found**
```python
NoSuchElementException
```
**Solution:**
```python
# Use explicit waits
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

wait = WebDriverWait(driver, 10)
element = wait.until(
    EC.presence_of_element_located((By.ID, "myid"))
)
```

**Issue 4: Stale element reference**
```python
StaleElementReferenceException
```
**Solution:**
```python
# Re-find element
try:
    element.click()
except StaleElementReferenceException:
    element = driver.find_element(By.ID, "myid")
    element.click()
```

**Issue 5: Session timeout**
```
Session is terminated due to timeout
```
**Solution:**
```bash
# Increase timeout on Node
java -jar selenium-server-4.38.0.jar node --session-timeout 600
```

---

## Chapter 21: Performance Optimization

### 21.1 Speed Up Tests

**1. Use Headless Mode:**
```python
chrome_options = Options()
chrome_options.add_argument("--headless")
# 20-30% faster
```

**2. Disable Images:**
```python
prefs = {"profile.managed_default_content_settings.images": 2}
chrome_options.add_experimental_option("prefs", prefs)
# 40% faster page loads
```

**3. Implicit Waits:**
```python
driver.implicitly_wait(10)  # Set once, applies globally
```

**4. Page Load Strategy:**
```python
chrome_options.page_load_strategy = 'eager'  # Don't wait for full load
```

### 21.2 Grid Performance

**1. Optimize Node Configuration:**
```bash
# 2-3 sessions per node (optimal)
java -jar selenium-server-4.38.0.jar node --max-sessions 3

# Session timeout
--session-timeout 300  # 5 minutes
```

**2. Network Latency:**
- Deploy nodes close to Hub (same data center)
- Use gigabit network
- Monitor ping times

**3. Resource Allocation:**
```
Per Browser Instance:
├── 500 MB - 1 GB RAM
├── 0.5 - 1 CPU core
└── 50-100 MB disk
```

---

## Chapter 22: Final Project Structure

### 22.1 Production-Ready Structure

```
selenium-automation-grid/
│
├── 📂 src/
│   ├── 📂 pages/           # Page Object Models
│   │   ├── login_page.py
│   │   ├── home_page.py
│   │   └── base_page.py
│   │
│   ├── 📂 tests/           # Test cases
│   │   ├── test_login.py
│   │   ├── test_navigation.py
│   │   └── conftest.py
│   │
│   └── 📂 utils/           # Utilities
│       ├── driver_factory.py
│       ├── config.py
│       └── helpers.py
│
├── 📂 grid/                # Grid setup
│   ├── selenium-server-4.38.0.jar
│   ├── start_hub.sh
│   └── start_node.sh
│
├── 📂 screenshots/         # Test screenshots
├── 📂 reports/            # Test reports
├── 📂 logs/               # Execution logs
│
├── 📄 requirements.txt    # Dependencies
├── 📄 .env.example        # Env template
├── 📄 .gitignore         # Git exclusions
├── 📄 pytest.ini         # Pytest config
├── 📄 README.md          # Documentation
├── 📄 MASTER_GUIDE.md    # This guide
└── 📄 Jenkinsfile        # CI/CD
