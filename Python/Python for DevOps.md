# Python for DevOps

Automation, Scripting, and Cloud Integration

---

## Introduction

Python has become one of the most important programming language for **DevOps, Engineers** due to its simplicity, flexibility, and powerful ecosystem.

In DevOps, Python is not used to build large applications &mdash; it is used to:
* Automate repetitive tasks
* Integrate tools and services
* Manage infrastructure
* Improve reliability and efficiency

This guide builds Python knowledge step-by-step, focusing only on what **DevOps, engineers actually need**.

---

## Day &mdash; Python in the DevOps World

### What is DevOps?
DevOps is a culture and set of practices that focus on:
* Automation
* Collaboration between development and operations
* Continuous integration and deliver
* Faster releases with higher reliability

DevOps engineers solve problems by **automating systems**, not by manually managing them.

### Why Python for DevOps?
Python is widely used in DevOps because:
* **Easy to read and write**<br>Python code is a simple and readable, even for beginners.
* **Cross-platform**<br>Python scripts run on Linux, Windows, and macOS.
* **Huge ecosystem**<br>Libraries exist for cloud, containers, API, monitoring, and automation.
* **Strong community support**<br>Problems are easy to troubleshoot with abundant resources.

### Core Use Cases of Python in DevOps
Python is commonly used for:
* CI/ CD automation
* Infrastructure provisioning
* Cloud automation
* Configuration management
* Monitoring and alerting
* Log analysis
* API integration
* Container and Kubernetes automation
* Cost optimization scripts

### Four Pillars of Programming (DevOps Perspective)
* Keywords
* Data Types
* Operators
* Logical Reasoning

---

## Day 02 &mdash; Data Types

### What is a Data Types?
A data type defines **what kind of data** a variable holds.<br>
Python is a **dynamically typed language**, meaning you don't declare data types explicitly.

---

### Built-in Python Data Types

#### Numeric Types

| Data Types | Description      | Example      |
|:-----------|:-----------------|:-------------|
| `int`      | Whole numbers    | `a = 10`     |
| `float`    | Decimal numbers  | `b = 10.5`   |
| `complex`  | Complex numbers  | `c = 2 + 3j` |

#### Sequence Types

| Type    | Description                  | Example                          |
|:--------|:-----------------------------|:---------------------------------|
| `str`   | Text                         | `name = "DevOps"`                |
| `list`  | Mutable ordered collection   | `servers = ["web", "app", "db"]` |
| `tuple` | Immutable ordered collection | `(10, 20) `                      |

#### Mapping Types

| Type   | Description     | Example                                          |
|--------|-----------------|--------------------------------------------------|
| `dict` | Key-Value pairs | `config = {"env": "prod", "region":"us-east-1"}` |

### Set Types

Sets are of two types:
* `set` &mdash; A mutable collection of unique, unordered elements (no duplicates allowed).
```python
fruits = {"apple", "banana", "apple"}  # duplicates removed
print(fruits)  # {'apple', 'banana'}
fruits.add("mango")  # can be modified
```

* `frozenset` &mdash; Same as a set, but immutable &mdash; it cannot be changed after creation.
```python
permissions = frozenset({"read", "write", "execute"})
print(permissions)  # frozenset({'read', 'write', 'execute'})
permissions.add("delete")  # ❌ AttributeError: can't modify a frozenset
```

---

#### Boolean Type
`is_active = True`

---

#### None Type
`result = None`

---

## Day 03 &mdash; Keywords and Variables

### Python Keywords
Keywords are **reserved words** with special meaning.<br>
Example:
* `if, else, for, while`
* `def, return`
* `try, except`
* `True, False, None`

```python
import keyword
print(keyword,kwlist)
```

### Variables
Variables store values in memory.<br>
**Rules**
* Must start with a letter or underscore
* Cannot start with a number
* Case-sensitive
* Cannot use Keywords

```python
service = "nginx"
port = 80
enabled = True
```

---

### Variable Scope (LEGB Rule)
Python resolve variables in the order:
1. Local
2. Enclosing
3. Global
4. Built-in

---

## Day 04 &mdash; Functions, Modules, and Packages
### Functions
Functions group reusable logic
```python
def greet (name):
    return f"Hello {name}"
```

**Benefits**:
* Code reuse
* Better readability
* Easier maintenance

---

### Modules

A modules is a Python file.

`import os`<br>
`import sys`<br>
`import json`

---

### Packages
Packages are collections of modules.
>my_package/ <br>
> |&mdash; __init__.py <br>
> |&mdash; module1.py <br>
> |&mdash; module2.py

Package help organize large DevOps automation projects.

---

## Day 05 &mdash; Arguments & Environment Variables

### Command Line Arguments
Used to pass runtime values
```python
import sys
print(sys.argv)
```

### Environment Variables
Used to store secrets and configs.
```python
import os
db_host = os.getenv("DB_HOST", "localhost")
```
**Best Practice**: Never hardcode credentials

---

## Day 06 &mdash; Operators
### Operator Categories
* Arithmetic
* Comparison
* Logical
* Assignment
* Bitwise
* Identity
* Membership

```python
a = 10
b = 5
print(a + b)
print(a > b)
```
Operator precedence matters in a automation logic.

---

## Day 07 &mdash; Conditional Statements

### if/ elif/ else
```python
if cpu > 80:
    print("Scale Up")
else: 
    print("Normal")
```

**Used heavily in**:
* Monitoring scripts
* Decision-making automation
* CI/ CD workflows

---

## Day 08 &mdash; Lists and Tuples

### Lists

* Mutable
* Ordered
* Used for Dynamic data

```python
instances = ["web1", "web2"]
instances.append ("web3")
```

---

### Tuples

* Immutable
* Safer for fixed data

```python
regions = ("us-east-1", "us-west-2")
```

---

## Day 09 &mdash; Loops

### for Loop

```python
for server in servers:
    print(server)
```

### while

```python
while retries <3:
    retries += 1
```

---

### `break`, `continue`, `else`

* **break** &mdash; Immediately exits the loop when a condition is met.
```python
for i in range(10):
    if i == 5:
        break
    print(i)
```
`Output:0 1 2 3 4`  

* **continue** &mdash; **Skips** the current iteration and moves to the next one.
```python
for i in range (6):
    if i == 3:
        continue
    print (i)
```
`Output: 0 1 2 4 5`


* **else** &mdash; Run only if the loop completes without hitting a `break`.

```python
for i in range(5):
    if i == 10:
        break
    print(i)
else:
    print("Loop finished normally!")  # ✅ runs because break was never hit

```
`Output: 0 1 2 3 4 → Loop finished normally!`

> The `else` block is skipped if `break` is triggered:

```python
for i in range(5):
    if i == 3:
        break
else:
    print("This won't print")
```

---

## Day 10 &mdash; User Input & Exception Handling

### Input Handling
```python
name = input("Enter name: ")
```

---

### Exception Handling

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Error occurred")
```
Essential for **fault-tolerant DevOps scripts**

---

## Day 11 &mdash; Dictionaries & Sets
### Dictionaries
Used heavily for:
* Configurations
* API responses
* Metadata
### Sets
**Used for**:
* Removing duplicates
* Comparing resources

`unique_users = set(users)`

---

## Day 12 &mdash; File Operations
### File Handling

```python
with open ("config.txt", "r") as file:
    data = file.read()
```

**Used for**:
* Config management
* Log parsing
* Report generation

---

## Day 13 &mdash; Boto3 (AWS Automation)

### What is Boto3?
Boto3 is the AWS SDK for Python.

**Used to**:
* Create EC2, S3, IAM, RDS
* Automate AWS operations
* Optimize cloud costs

```python
import boto3
s3 = boto3.client("s3")
```

---


## Day 14 & 15 &mdash; GitHub & JIRA Integration

### DevOps Use Case

* Automatically create JIRA tickets
* Trigger workflows from GitHub events
* Integrate incident management

Python acts as the glue language between tools.

---

## Day 16 &mdash; Interview & Practical Concepts

### Key Interview Topics
* Mutable vs Immutable
* List Vs. Tuple
* Global vs. local variables
* Exception handling
* Virtual environments
* Decorators
* Lambda functions

---

## Additional Topics (Often Missed)

### Virtual Environments
```python
python -m venv venv
source venv/bin/activate
```

### Logging (Critical for DevOps)

```python
import logging
logging.basicConfig(level = logging.INFO)
```

### JSON & API Handling

```python
import json
data = json.loads(response.txt)
```

---

## Final Thoughts

Python is not about writing complex software in DevOps. <br>
Python is about:
* Automation
* Reliability
* Integration
* Speed

A DevOps engineer with strong Python fundamentals:
* Automates faster
* Troubleshoots better
* Scales systems efficiently






















