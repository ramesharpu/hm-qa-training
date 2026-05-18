# DevOps Training Content

# Module 7: Advanced Robot Framework Concepts

---

# 1. Page Object Model (POM) in Robot Framework

## What is POM?

Page Object Model (POM) is a design pattern used in test automation where each web page is represented as a separate object (file/class) containing:

* Locators
* Keywords (actions)

This improves:

* Maintainability
* Reusability
* Scalability

---

## Why POM is Important?

Without POM:

* Test cases become repetitive
* Locators are duplicated
* Maintenance becomes difficult

With POM:

* UI changes are handled in one place
* Tests become cleaner and readable

---

## POM Architecture

```text id="p1p7qa"
Test Cases → Page Objects → SeleniumLibrary → Application
```

---

## POM Folder Structure

```text id="p2k9vm"
project/
│
├── tests/
├── pages/
│   ├── login_page.robot
│   ├── dashboard_page.robot
│
├── resources/
└── keywords/
```

---

## Example: Login Page Object

```robot id="p3x8ql"
*** Settings ***
Library    SeleniumLibrary

*** Variables ***
${USERNAME}    id=username
${PASSWORD}    id=password
${LOGIN_BTN}   id=login
```

---

## Login Keywords (POM Style)

```robot id="p4m2tn"
*** Keywords ***
Open Login Page
    Go To    https://example.com/login

Enter Username
    [Arguments]    ${user}
    Input Text    ${USERNAME}    ${user}

Enter Password
    [Arguments]    ${pass}
    Input Password    ${PASSWORD}    ${pass}

Click Login
    Click Button    ${LOGIN_BTN}
```

---

## Using POM in Test Case

```robot id="p5v7qp"
*** Test Cases ***
Valid Login Test
    Open Login Page
    Enter Username    admin
    Enter Password    admin123
    Click Login
```

---

## Benefits of POM in Robot Framework

* Reduces duplication
* Centralizes locators
* Easier maintenance
* Better scalability
* Improves readability

---

# 2. Data-Driven Testing

## What is Data-Driven Testing?

Data-driven testing executes the same test case multiple times using different input data sets.

---

## Why Use Data-Driven Testing?

* Reduces duplicate test cases
* Improves coverage
* Supports multiple scenarios
* Easy test expansion

---

## Data Sources

| Source | Format                 |
| ------ | ---------------------- |
| CSV    | Comma-separated values |
| JSON   | Structured data        |
| YAML   | Configuration data     |
| Excel  | Tabular data           |

---

# CSV-Based Data-Driven Testing

## Example CSV File

```text id="d1c8qp"
username,password
admin,admin123
user1,pass1
user2,pass2
```

---

## Reading CSV in Robot Framework

```robot id="d2m7ql"
*** Settings ***
Library    CSVLibrary
Library    SeleniumLibrary
```

---

## Data-Driven Test Case

```robot id="d3v5tn"
*** Test Cases ***
Login Test Using CSV
    ${data}=    Read CSV File    data.csv

    FOR    ${row}    IN    @{data}
        Open Browser    https://example.com    chrome
        Input Text      id=username    ${row}[username]
        Input Password  id=password    ${row}[password]
        Click Button    id=login
        Close Browser
    END
```

---

# JSON-Based Data-Driven Testing

## Example JSON File

```json id="j1k4qp"
[
  {
    "username": "admin",
    "password": "admin123"
  },
  {
    "username": "user1",
    "password": "pass1"
  }
]
```

---

## JSON Usage

```robot id="j2m8ql"
*** Settings ***
Library    JSONLibrary
Library    SeleniumLibrary
```

---

## JSON Test Example

```robot id="j3v9tn"
*** Test Cases ***
Login Test Using JSON
    ${data}=    Load JSON From File    data.json

    FOR    ${item}    IN    @{data}
        Open Browser    https://example.com    chrome
        Input Text      id=username    ${item["username"]}
        Input Password  id=password    ${item["password"]}
        Click Button    id=login
        Close Browser
    END
```

---

# Benefits of Data-Driven Testing

* Better test coverage
* Less code duplication
* Easy maintenance
* Supports multiple environments

---

# 3. Test Listeners in Robot Framework

## What are Listeners?

Listeners are hooks that allow you to monitor and modify test execution events.

---

## Use Cases

* Logging test execution
* Capturing screenshots
* Custom reporting
* Integrating external tools

---

## Types of Listeners

| Type              | Description                  |
| ----------------- | ---------------------------- |
| Built-in Listener | Default Robot events         |
| Custom Listener   | User-defined Python listener |

---

## Example Listener Usage

```bash id="l1q7tn"
robot --listener MyListener.py test.robot
```

---

## Custom Listener (Python Example)

```python id="l2m8qp"
class MyListener:
    def start_test(self, name, attrs):
        print(f"Starting test: {name}")

    def end_test(self, name, attrs):
        print(f"Finished test: {name}")
```

---

## Benefits of Listeners

* Real-time monitoring
* Custom logging
* Enhanced reporting
* Integration flexibility

---

# 4. CI/CD Integration with GitHub Actions

## What is GitHub Actions?

GitHub Actions is a CI/CD tool that automates workflows directly from GitHub repositories.

---

## Why Use GitHub Actions with Robot Framework?

* Automated test execution
* Continuous testing
* Faster feedback
* Integration with pull requests

---

## CI/CD Workflow

```text id="c1v7ql"
Git Push → GitHub Actions → Install Dependencies → Run Tests → Publish Reports
```

---

## Example Workflow File

```yaml id="c2m9tn"
name: Robot Framework Tests

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3

    - name: Install Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.10'

    - name: Install dependencies
      run: |
        pip install robotframework
        pip install robotframework-seleniumlibrary

    - name: Run Tests
      run: robot tests/

    - name: Upload Reports
      uses: actions/upload-artifact@v3
      with:
        name: robot-reports
        path: report.html
```

---

## Benefits of CI/CD Integration

* Early bug detection
* Automated regression testing
* Faster release cycles
* Better collaboration

---

# 5. Debugging in Robot Framework

## Common Debugging Techniques

### 1. Log Keyword

```robot id="d1v8ql"
Log    Debug message here
```

---

### 2. Print Variables

```robot id="d2m9tn"
Log    ${username}
```

---

### 3. Run in Debug Mode

```bash id="d3q7qp"
robot --loglevel DEBUG test.robot
```

---

### 4. Pause Execution

```robot id="d4v8ql"
Pause Execution
```

---

### 5. Capture Screenshots

```robot id="d5m9tn"
Capture Page Screenshot
```

---

## Debugging Best Practices

* Use meaningful logs
* Enable debug logs when needed
* Capture screenshots on failure
* Isolate failing test cases

---

# 6. Tags in Robot Framework

## What are Tags?

Tags are labels assigned to test cases for grouping and filtering.

---

## Example Tags

```robot id="t1v8ql"
*** Test Cases ***
Login Test
    [Tags]    smoke    regression
```

---

## Running Tests by Tags

### Run Smoke Tests

```bash id="t2m9tn"
robot --include smoke tests/
```

---

### Exclude Tags

```bash id="t3q7qp"
robot --exclude regression tests/
```

---

## Benefits of Tags

* Selective execution
* Better organization
* Faster test runs
* Environment-based execution

---

# 7. Retry Mechanism

## Why Retry is Needed?

Some tests fail due to:

* Network delays
* UI instability
* Timing issues

---

## Wait Until Keyword Succeeds

```robot id="r1v8ql"
Wait Until Keyword Succeeds
...    1 min
...    5 sec
...    Click Element    id=submit
```

---

## Retry Failed Test Case (External Tool)

Using tools like:

* pytest-rerunfailures
* CI retry strategies

---

## Best Practices for Retries

* Use retries for flaky UI only
* Avoid masking real issues
* Combine with proper waits

---

# 8. Parallel Execution

## Why Parallel Execution?

Parallel execution reduces test execution time.

---

## Approaches

### 1. Pabot (Robot Framework Tool)

Pabot

---

## Install Pabot

```bash id="p1m8ql"
pip install robotframework-pabot
```

---

## Run Tests in Parallel

```bash id="p2v9tn"
pabot tests/
```

---

## Parallel Execution by Suite

```bash id="p3q7qp"
pabot --processes 4 tests/
```

---

## Benefits of Parallel Execution

* Faster execution
* Efficient resource usage
* Scalable test runs
* CI/CD optimization

---

## Limitations

* Shared state issues
* Resource contention
* Need proper test isolation

---

## Parallel Execution Best Practices

* Avoid shared dependencies
* Use isolated test data
* Design independent test cases
* Use environment-specific setups

---

# Summary

In this module, we covered:

* Page Object Model (POM)
* Data-driven testing (CSV/JSON)
* Test listeners
* CI/CD integration using GitHub Actions
* Debugging techniques
* Tags for test filtering
* Retry mechanisms
* Parallel execution using Pabot
