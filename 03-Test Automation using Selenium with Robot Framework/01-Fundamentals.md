# DevOps Training Content

# Module 5: Robot Framework Fundamentals

---

# 1. Introduction to Robot Framework

## What is Robot Framework?

Robot Framework is an open-source automation testing framework used for:

* Test automation
* Acceptance testing
* Robotic Process Automation (RPA)

It follows a:

* Keyword-driven testing approach

Robot Framework is widely used for:

* Web testing
* API testing
* Database testing
* Desktop automation

---

# Features of Robot Framework

| Feature        | Description                     |
| -------------- | ------------------------------- |
| Keyword-Driven | Easy-to-read test syntax        |
| Open Source    | Free to use                     |
| Extensible     | Supports custom libraries       |
| Cross Platform | Works on Windows/Linux/macOS    |
| Rich Reports   | Generates HTML reports and logs |

---

# Why Use Robot Framework?

Robot Framework helps teams:

* Simplify test automation
* Improve readability
* Reuse test components
* Reduce maintenance effort

---

# Robot Framework Architecture

```text id="8k3qtm"
Test Cases → Keywords → Libraries → Application
```

---

# Components of Robot Framework

| Component  | Purpose                     |
| ---------- | --------------------------- |
| Test Cases | Define automation tests     |
| Keywords   | Reusable actions            |
| Libraries  | Built-in/external functions |
| Variables  | Store reusable values       |
| Reports    | Execution summaries         |

---

# Supported Testing Types

* UI Testing
* API Testing
* Regression Testing
* Smoke Testing
* Acceptance Testing

---

# Common Robot Framework Libraries

| Library         | Purpose          |
| --------------- | ---------------- |
| BuiltIn         | Core keywords    |
| SeleniumLibrary | Web automation   |
| RequestsLibrary | API testing      |
| DatabaseLibrary | Database testing |
| OperatingSystem | File operations  |

---

# 2. Robot Framework Installation

## Prerequisites

Before installing Robot Framework:

* Install Python
* Install pip package manager

---

# Verify Python Installation

```bash id="5m8vpa"
python --version
```

---

# Verify pip Installation

```bash id="3n7qkl"
pip --version
```

---

# Install Robot Framework

## Using pip

```bash id="2x9tmd"
pip install robotframework
```

---

# Verify Installation

```bash id="1k4zpl"
robot --version
```

---

# Install SeleniumLibrary

For web automation:

```bash id="7v2qnb"
pip install robotframework-seleniumlibrary
```

---

# Install RequestsLibrary

For API testing:

```bash id="9m6wrt"
pip install robotframework-requests
```

---

# Recommended IDEs

| IDE     | Support             |
| ------- | ------------------- |
| VS Code | Excellent           |
| PyCharm | Good                |
| RIDE    | Robot Framework IDE |

---

# VS Code Extensions

Recommended extensions:

* Robot Framework Language Server
* Python Extension

---

# 3. Test Data Syntax

## Robot Framework File Structure

Robot Framework test files use:

```text id="4x8qln"
.robot
```

extension.

---

# Main Sections in Robot Framework

| Section            | Purpose                  |
| ------------------ | ------------------------ |
| *** Settings ***   | Libraries and setup      |
| *** Variables ***  | Store variables          |
| *** Test Cases *** | Define tests             |
| *** Keywords ***   | Custom reusable keywords |

---

# Basic Robot Framework Structure

```robot id="7p2mqa"
*** Settings ***
Library    SeleniumLibrary

*** Variables ***
${URL}     https://example.com

*** Test Cases ***
Open Website
    Open Browser    ${URL}    chrome
    Close Browser
```

---

# *** Settings *** Section

## Purpose

Used for:

* Importing libraries
* Resource files
* Setup/teardown configuration

---

# Example

```robot id="6v3qkt"
*** Settings ***
Library    SeleniumLibrary
Library    OperatingSystem
```

---

# *** Variables *** Section

## Purpose

Stores reusable values.

---

# Variable Types

| Variable Type | Syntax      |
| ------------- | ----------- |
| Scalar        | ${variable} |
| List          | @{list}     |
| Dictionary    | &{dict}     |

---

# Example Variables

```robot id="1z7qmp"
*** Variables ***
${URL}       https://example.com
@{BROWSERS}  chrome  firefox
&{USER}      username=admin   password=admin123
```

---

# *** Test Cases *** Section

## Purpose

Contains executable test cases.

---

# Example Test Case

```robot id="8r5vql"
*** Test Cases ***
Login Test
    Open Browser    https://example.com    chrome
    Input Text      id=username    admin
    Input Password  id=password    admin123
    Click Button    id=login
    Close Browser
```

---

# Test Case Structure

```text id="5w1xkn"
Test Case Name
    Keyword    Argument1    Argument2
```

---

# 4. Keyword-Driven Testing Basics

## What is Keyword-Driven Testing?

Keyword-driven testing uses reusable keywords to represent actions.

Example:

* Open Browser
* Click Button
* Input Text

This improves:

* Readability
* Reusability
* Maintainability

---

# Keyword-Driven Workflow

```text id="0m8qtp"
Test Case → Keywords → Libraries → Application
```

---

# Types of Keywords

| Type              | Description                      |
| ----------------- | -------------------------------- |
| Built-in Keywords | Default Robot Framework keywords |
| Library Keywords  | Imported library functions       |
| User Keywords     | Custom-defined keywords          |

---

# Built-In Keywords

Robot Framework includes many built-in keywords.

Examples:

* Log
* Sleep
* Should Be Equal
* Run Keyword

---

# Example Built-In Keywords

```robot id="4v7qms"
*** Test Cases ***
Example Test
    Log    Hello Robot Framework
    Should Be Equal    10    10
```

---

# SeleniumLibrary Keywords

| Keyword       | Purpose          |
| ------------- | ---------------- |
| Open Browser  | Launch browser   |
| Click Element | Click UI element |
| Input Text    | Enter text       |
| Close Browser | Close browser    |

---

# Example Selenium Test

```robot id="2p8qtw"
*** Settings ***
Library    SeleniumLibrary

*** Test Cases ***
Google Search
    Open Browser    https://google.com    chrome
    Input Text      name=q    Robot Framework
    Close Browser
```

---

# Advantages of Keyword-Driven Testing

* Easy for non-programmers
* Reusable automation
* Simplified maintenance
* Better readability

---

# 5. Execution Using Robot Command

## How Robot Tests Execute

Robot Framework executes test files using the:

```text id="6x2vmp"
robot
```

command.

---

# Basic Execution Command

```bash id="7n4qla"
robot test.robot
```

---

# Execute Specific Folder

```bash id="3k9wtn"
robot tests/
```

---

# Run Specific Test Case

```bash id="9q1xrl"
robot --test "Login Test" test.robot
```

---

# Output Files Generated

| File        | Purpose                 |
| ----------- | ----------------------- |
| report.html | Test summary            |
| log.html    | Detailed execution logs |
| output.xml  | Machine-readable output |

---

# HTML Report Example

After execution:

```text id="8w6qmp"
report.html
```

shows:

* Passed tests
* Failed tests
* Execution statistics

---

# Log File Features

```text id="2m7vqa"
log.html
```

contains:

* Step-by-step execution
* Screenshots
* Keyword details
* Error information

---

# Custom Output Directory

```bash id="1x5qkn"
robot -d results tests/
```

---

# Generate Console Output

```bash id="0r8vpl"
robot --console verbose test.robot
```

---

# 6. Variables in Robot Framework

# Scalar Variables

## Syntax

```robot id="5q2vtn"
${USERNAME}
```

---

# Example

```robot id="9m4xkp"
*** Variables ***
${USERNAME}    admin
```

---

# List Variables

## Syntax

```robot id="4z8qtr"
@{BROWSERS}
```

---

# Example

```robot id="6k1vpm"
*** Variables ***
@{BROWSERS}    chrome    firefox    edge
```

---

# Access List Item

```robot id="3q9xln"
${BROWSERS}[0]
```

---

# Dictionary Variables

## Syntax

```robot id="2n7vqa"
&{USER}
```

---

# Example

```robot id="8m5qtp"
*** Variables ***
&{USER}    username=admin    password=admin123
```

---

# Access Dictionary Value

```robot id="4p1xkm"
${USER}[username]
```

---

# Variable Best Practices

* Use meaningful names
* Centralize reusable variables
* Avoid hardcoding values
* Store secrets securely

---

# 7. Simple Custom Keywords

## What are Custom Keywords?

Custom keywords are reusable user-defined actions.

They help:

* Reduce duplication
* Improve readability
* Simplify maintenance

---

# *** Keywords *** Section

Used to define custom reusable keywords.

---

# Example Custom Keyword

```robot id="1v7qpm"
*** Keywords ***
Open Application
    Open Browser    https://example.com    chrome
    Maximize Browser Window
```

---

# Using Custom Keyword

```robot id="6x4qtn"
*** Test Cases ***
Launch Test
    Open Application
    Close Browser
```

---

# Custom Keyword with Arguments

## Example

```robot id="9p2vkl"
*** Keywords ***
Login User
    [Arguments]    ${username}    ${password}
    Input Text     id=username    ${username}
    Input Password id=password    ${password}
```

---

# Reusable Login Test

```robot id="5m8qtr"
*** Test Cases ***
Valid Login
    Open Browser    https://example.com    chrome
    Login User      admin    admin123
    Close Browser
```

---

# Benefits of Custom Keywords

| Benefit         | Description        |
| --------------- | ------------------ |
| Reusability     | Reuse common steps |
| Readability     | Cleaner test cases |
| Maintainability | Easy updates       |
| Modularity      | Better structure   |

---

# Recommended Project Structure

```text id="7n3vql"
project/
│
├── tests/
├── keywords/
├── resources/
├── variables/
└── reports/
```

---

# Robot Framework Best Practices

* Use reusable keywords
* Keep tests independent
* Use descriptive test names
* Organize resources properly
* Store test data separately
* Generate reports after execution

---

# Summary

In this module, we covered:

* Robot Framework fundamentals
* Installation using pip
* Robot Framework syntax
* Settings, Variables, and Test Cases sections
* Keyword-driven testing
* Built-in libraries
* Test execution using robot command
* HTML reports and logs
* Variable types
* Creating custom keywords
