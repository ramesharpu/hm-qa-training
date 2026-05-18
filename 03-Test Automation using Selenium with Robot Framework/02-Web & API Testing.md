# DevOps Training Content

# Module 6: Robot Framework Web UI & API Automation

---

# 1. SeleniumLibrary for Web UI Automation

## What is SeleniumLibrary?

SeleniumLibrary is a Robot Framework library used for browser-based web automation.

It integrates:

* Robot Framework
* Selenium WebDriver

to automate web applications.

---

# Why SeleniumLibrary?

SeleniumLibrary enables:

* Cross-browser testing
* UI automation
* Functional testing
* Regression testing

Supported browsers:

* Chrome
* Firefox
* Edge
* Safari

---

# SeleniumLibrary Architecture

```text id="8q2vml"
Robot Framework → SeleniumLibrary → WebDriver → Browser
```

---

# Install SeleniumLibrary

```bash id="5m7qpa"
pip install robotframework-seleniumlibrary
```

---

# Install Browser Driver

Examples:

* ChromeDriver
* GeckoDriver

---

# Import SeleniumLibrary

```robot id="2x9qtn"
*** Settings ***
Library    SeleniumLibrary
```

---

# Opening Browser

## Example

```robot id="7v4qmp"
*** Test Cases ***
Open Website
    Open Browser    https://example.com    chrome
    Maximize Browser Window
```

---

# Browser Management Keywords

| Keyword                 | Purpose               |
| ----------------------- | --------------------- |
| Open Browser            | Launch browser        |
| Close Browser           | Close current browser |
| Close All Browsers      | Close all sessions    |
| Maximize Browser Window | Maximize browser      |

---

# Locators in SeleniumLibrary

## What are Locators?

Locators identify web elements on a webpage.

---

# Types of Locators

| Locator | Example                     |
| ------- | --------------------------- |
| id      | id=username                 |
| name    | name=email                  |
| xpath   | xpath=//input[@type='text'] |
| css     | css=.login-btn              |
| class   | class=container             |
| link    | link=Login                  |

---

# Locator Example

```robot id="4n8qtp"
Input Text    id=username    admin
Click Button  xpath=//button[@type='submit']
```

---

# Web Interactions

## Input Text

```robot id="9k2vqm"
Input Text    id=username    admin
```

---

## Click Button

```robot id="1m7qpl"
Click Button    id=login
```

---

## Click Element

```robot id="3x5qtn"
Click Element    xpath=//a[text()='Home']
```

---

## Select Dropdown Value

```robot id="6v1qmp"
Select From List By Label    id=country    India
```

---

## Checkbox Interaction

```robot id="8q4vkl"
Select Checkbox    id=remember
```

---

# Handling Waits

## Why Waits are Important

Web applications may load dynamically.

Without waits:

* Tests may fail
* Elements may not be available

---

# Types of Waits

| Wait Type     | Purpose            |
| ------------- | ------------------ |
| Implicit Wait | Default wait       |
| Explicit Wait | Wait for condition |
| Sleep         | Static delay       |

---

# Explicit Wait Example

```robot id="7n3qtm"
Wait Until Element Is Visible    id=login    10s
```

---

# Wait Until Page Contains

```robot id="5x8vpl"
Wait Until Page Contains    Dashboard
```

---

# Avoid Using Sleep Frequently

```robot id="2m4qka"
Sleep    5s
```

Best practice:
Use explicit waits instead of static delays.

---

# Assertions in SeleniumLibrary

## Verify Page Contains

```robot id="1p7vqn"
Page Should Contain    Welcome
```

---

## Verify Element Visible

```robot id="4v2qtm"
Element Should Be Visible    id=logout
```

---

# Screenshot Capture

```robot id="9x5qpl"
Capture Page Screenshot
```

---

# Complete UI Test Example

```robot id="6m8vtn"
*** Settings ***
Library    SeleniumLibrary

*** Test Cases ***
Login Test
    Open Browser    https://example.com    chrome
    Input Text      id=username    admin
    Input Password  id=password    admin123
    Click Button    id=login
    Wait Until Page Contains    Dashboard
    Page Should Contain          Dashboard
    Capture Page Screenshot
    Close Browser
```

---

# SeleniumLibrary Best Practices

* Use stable locators
* Prefer explicit waits
* Avoid hardcoded delays
* Capture screenshots on failures
* Use reusable keywords

---

# 2. RequestsLibrary for API Testing

## What is RequestsLibrary?

RequestsLibrary is used for REST API automation testing in Robot Framework.

It simplifies:

* API requests
* Response validation
* Authentication testing

---

# Install RequestsLibrary

```bash id="3q7vpl"
pip install robotframework-requests
```

---

# Import RequestsLibrary

```robot id="8m4qtn"
*** Settings ***
Library    RequestsLibrary
```

---

# API Testing Workflow

```text id="5v1qkl"
Send Request → Receive Response → Validate Response
```

---

# HTTP Methods

| Method | Purpose       |
| ------ | ------------- |
| GET    | Retrieve data |
| POST   | Create data   |
| PUT    | Update data   |
| DELETE | Remove data   |

---

# Create Session

```robot id="2x8qmp"
Create Session    mysession    https://reqres.in
```

---

# GET Request Example

```robot id="9n5qvl"
*** Test Cases ***
Get Users
    Create Session    api    https://reqres.in
    ${response}=    GET On Session    api    /api/users?page=2
    Status Should Be    200    ${response}
```

---

# Validate Response Content

```robot id="4m7qtp"
Should Contain    ${response.text}    Michael
```

---

# POST Request Example

```robot id="6x2vkl"
*** Test Cases ***
Create User
    Create Session    api    https://reqres.in

    ${body}=    Create Dictionary
    ...    name=John
    ...    job=Tester

    ${response}=    POST On Session
    ...    api
    ...    /api/users
    ...    json=${body}

    Status Should Be    201    ${response}
```

---

# API Assertions

| Assertion        | Purpose              |
| ---------------- | -------------------- |
| Status Should Be | Validate status code |
| Should Contain   | Verify response text |
| Should Be Equal  | Compare values       |

---

# Validate JSON Response

```robot id="7q3vmp"
Should Be Equal    ${response.json()}[data][0][id]    1
```

---

# Authentication Example

```robot id="1v8qtn"
Create Session
...    api
...    https://example.com
...    auth=${AUTH}
```

---

# API Testing Best Practices

* Validate status codes
* Verify response schema
* Use reusable sessions
* Store endpoints in variables
* Handle authentication securely

---

# 3. Test Suites Structure

## What is a Test Suite?

A test suite is a collection of related test cases grouped together.

---

# Benefits of Test Suites

* Better organization
* Easier maintenance
* Modular testing
* Improved scalability

---

# Recommended Project Structure

```text id="8p4vql"
project/
│
├── tests/
│   ├── ui/
│   ├── api/
│   └── regression/
│
├── resources/
│
├── variables/
│
├── keywords/
│
└── reports/
```

---

# Suite Structure Example

```robot id="5m1qtn"
tests/
    login.robot
    dashboard.robot
    api_tests.robot
```

---

# Running Entire Test Suite

```bash id="2v7qpl"
robot tests/
```

---

# Running Specific Suite

```bash id="9x3vkm"
robot tests/ui/
```

---

# Test Suite Setup & Teardown

## Example

```robot id="6n5qtp"
*** Settings ***
Suite Setup       Open Browser
Suite Teardown    Close Browser
```

---

# Test Setup & Teardown

```robot id="4q8vpl"
*** Settings ***
Test Setup       Login User
Test Teardown    Logout User
```

---

# 4. Resource Files

## What are Resource Files?

Resource files store:

* Reusable keywords
* Variables
* Common configurations

---

# Benefits of Resource Files

| Benefit         | Description         |
| --------------- | ------------------- |
| Reusability     | Shared keywords     |
| Maintainability | Centralized updates |
| Cleaner Tests   | Reduced duplication |

---

# Resource File Example

## common.resource

```robot id="3m7qvl"
*** Keywords ***
Login User
    Input Text    id=username    admin
    Input Password    id=password    admin123
```

---

# Import Resource File

```robot id="8v2qtn"
*** Settings ***
Resource    ../resources/common.resource
```

---

# Using Resource Keyword

```robot id="1n5qpl"
*** Test Cases ***
Login Test
    Login User
```

---

# Variables File

## Example

```robot id="7m4qtk"
*** Variables ***
${URL}    https://example.com
```

---

# Benefits of Resource Organization

* Centralized management
* Better modularity
* Easier collaboration
* Reduced maintenance effort

---

# 5. Handling Dynamic Data

## What is Dynamic Data?

Dynamic data changes during execution.

Examples:

* Generated usernames
* Timestamps
* Session tokens
* API responses

---

# Generate Random Data

## Example

```robot id="5x1qvm"
${random}=    Generate Random String    5
```

---

# Current Date & Time

```robot id="9m6qpl"
${date}=    Get Current Date
```

---

# Store API Response Data

```robot id="4v8qtn"
${user_id}=    Set Variable    ${response.json()}[id]
```

---

# Using Variables Dynamically

```robot id="2q7vkp"
Input Text    id=username    user_${random}
```

---

# Reading External Test Data

Robot Framework supports:

* CSV files
* JSON files
* YAML files
* Excel integration

---

# Environment-Based Variables

```robot id="8n3qvl"
${ENV}    staging
${BASE_URL}    https://staging.example.com
```

---

# Dynamic Data Best Practices

* Avoid hardcoded values
* Generate unique test data
* Store reusable data centrally
* Use external data sources

---

# 6. Error Handling in Robot Framework

## Why Error Handling Matters

Automation failures can occur because of:

* Network issues
* Slow applications
* Invalid data
* Missing elements

Proper error handling improves test reliability.

---

# Run Keyword And Ignore Error

## Example

```robot id="6x4qtm"
${status}    ${message}=    
...    Run Keyword And Ignore Error
...    Click Element    id=optionalButton
```

---

# Run Keyword And Continue On Failure

```robot id="1m9qvl"
Run Keyword And Continue On Failure
...    Page Should Contain    Dashboard
```

---

# Handling Optional Elements

```robot id="7v2qkp"
Run Keyword If Element Exists
...    id=popup
...    Click Element    id=close
```

---

# TRY/EXCEPT Example

```robot id="3q5vtn"
TRY
    Click Element    id=submit
EXCEPT
    Log    Submit button not found
END
```

---

# Capture Screenshot on Failure

```robot id="9n1qpl"
Run Keyword If Test Failed    Capture Page Screenshot
```

---

# Retry Mechanism

```robot id="5v7qtm"
Wait Until Keyword Succeeds
...    30 sec
...    5 sec
...    Click Element    id=submit
```

---

# Error Handling Best Practices

* Use retries for unstable elements
* Capture screenshots on failure
* Use proper waits
* Avoid unnecessary test termination
* Log meaningful error messages

---

# Summary

In this module, we covered:

* SeleniumLibrary for UI automation
* Web locators and interactions
* Wait handling and assertions
* RequestsLibrary for API testing
* GET and POST requests
* API response validation
* Test suite organization
* Resource file management
* Dynamic data handling
* Error handling techniques
