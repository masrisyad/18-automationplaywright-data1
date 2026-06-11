Here is a comprehensive and easy-to-understand `README.md` for your script.

```markdown
# Automated Login Testing & PDF Reporting

This project is an automated testing script built with Python and **Playwright**. It performs an end-to-end login test on a web application, captures screenshots, generates a comprehensive PDF report (complete with test logs and a success rate chart), and automatically emails the results to designated recipients using the **Mailjet API**.

---

## 🌟 Features

* **Automated UI Testing:** Uses Playwright to simulate user interactions (navigating, typing credentials, and clicking buttons) asynchronously.
* **Visual Evidence:** Automatically captures a screenshot of the browser upon test completion.
* **Dynamic PDF Generation:** Uses `fpdf` and `matplotlib` to create a professional test report containing:
    * A donut chart illustrating the Pass/Fail success rate.
    * A detailed table of step-by-step test logs.
    * Screenshot evidence of the final state.
* **Email Integration:** Automatically sends the generated PDF report as an email attachment via Mailjet.
* **Resilient Error Handling:** Logs timeouts and interaction failures gracefully without crashing the report generation.

---

## 📋 Prerequisites

Before running the script, ensure you have the following installed:

* **Python 3.8+**
* **pip** (Python package installer)

### Required Python Packages

You will need to install the external dependencies used in this script. You can install them via pip:

```bash
pip install playwright matplotlib fpdf2 mailjet_rest

```

*Note: After installing Playwright, you must install the required browser binaries:*

```bash
playwright install chromium

```

---

## ⚙️ Configuration

This script relies on an external `settings.py` file to manage configurations. You must ensure that `settings.py` is present in the same directory and contains the following dataclass definitions: `EmailConfig` and `LoginConfig`.

### 1. Environment Variables

The script interacts with several environment variables for security and customization:

| Variable Name | Description | Default Value |
| --- | --- | --- |
| `WAIT_AFTER_LOGIN_SECONDS` | Time to wait before taking the final screenshot. | `3` |
| `SEND_EMAIL` | Set to `true` to enable email dispatching. | `false` |
| `MAILJET_API_KEY` | Your Mailjet public API key. | *None* (Required if sending email) |
| `MAILJET_API_SECRET` | Your Mailjet secret API key. | *None* (Required if sending email) |

### 2. The `settings.py` file

Make sure your `settings.py` defines the necessary configurations. It should look something like this:

```python
# settings.py example
from dataclasses import dataclass

@dataclass
class LoginConfig:
    login_url: str = "[https://your-website.com/login](https://your-website.com/login)"
    username: str = "your_email@example.com"
    password: str = "your_password"
    timeout_ms: int = 10000
    headless: bool = True

@dataclass
class EmailConfig:
    enabled: bool = True  # Or read from os.getenv("SEND_EMAIL")
    api_key: str = "your_mailjet_api_key"
    api_secret: str = "your_mailjet_secret"
    sender_email: str = "sender@example.com"
    sender_name: str = "QA Bot"
    recipient_email: str = "team@example.com"
    recipient_name: str = "Dev Team"
    subject: str = "Daily Automated Login Test Report"
    body: str = "Please find the attached automated test report."

```

---

## 🚀 Usage

Once your environment is set up and configured, you can run the test script directly from your terminal:

```bash
python main.py

```

*(Assuming you saved the provided script as `main.py`)*

### What happens when you run it?

1. The script launches a Chromium browser instance.
2. It navigates to the login URL and attempts to log in.
3. It listens for the success alert (*"Berhasil Masuk"*).
4. A screenshot (`screenshot1.png`) is saved to the working directory.
5. A PDF report (`test_report.pdf`) is compiled and saved.
6. If email is enabled, the PDF is dispatched via Mailjet.

---

## 📂 Output Files

After a successful (or failed) run, you will find the following files generated in your project directory:

* **`screenshot1.png`**: The visual capture of the page after the login attempt.
* **`test_report.pdf`**: The finalized report containing the pie chart, the tabular step-by-step logs, and the screenshot evidence.

```

```
