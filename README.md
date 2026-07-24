# 🕸️ Selenium in Google Colab: The Ultimate Boilerplate

[🇬🇧 English] | [🇷🇺 Русский] | [🇮🇷 فارسی]

---

## 🇬🇧 English

A plug-and-play boilerplate for running Headless Chrome with Selenium inside Google Colab. This setup automatically manages driver versions and includes essential bypasses for common anti-bot detection systems.

### 🚀 Features
* **Zero Manual Updates:** Uses `webdriver-manager` to automatically fetch the correct ChromeDriver binary. 
* **Colab-Ready:** Pre-configured with the mandatory `--no-sandbox` and `--disable-dev-shm-usage` flags required to run Chrome in Colab's Docker containers.
* **Anti-Bot Evasion:** Masks the automation environment by disabling `AutomationControlled` blink features and spoofing a standard Windows User-Agent.
* **Visual Debugging:** Includes a snippet to render headless screenshots directly inside the Colab notebook.

### 🛠️ Usage

**1. Install Dependencies**
```bash
!pip install selenium webdriver-manager
```
2. The Core Setup
```Python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
import subprocess

try:
    from webdriver_manager.chrome import ChromeDriverManager
except ImportError:
    print("webdriver-manager not found, installing...")
    subprocess.check_call(['pip', 'install', 'webdriver-manager'])
    from webdriver_manager.chrome import ChromeDriverManager

def get_colab_driver():
    options = webdriver.ChromeOptions()
    options.add_argument('--headless=new')
    options.add_argument('--no-sandbox')
    options.add_argument('--disable-dev-shm-usage')
    options.add_argument('--disable-blink-features=AutomationControlled')
    options.add_argument("user-agent=Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36")
    
    service = Service(ChromeDriverManager().install())
    return webdriver.Chrome(service=service, options=options)

driver = get_colab_driver()
driver.get("[https://example.com](https://example.com)")
driver.save_screenshot("visual_check.png")
```
3. View the Result
```Python
from IPython.display import Image, display
display(Image("visual_check.png"))
```
4. Clean Up
```Python
driver.quit()
```
