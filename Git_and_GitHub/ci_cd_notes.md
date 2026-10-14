I/CD — Continuous Integration & Continuous Delivery

# 1. CI — Continuous Integration

## 1. What is CI?

**CI stands for Continuous Integration.**

Continuous Integration is a software development practice in which developers frequently integrate their code changes into a shared repository, and automated checks are run to identify problems early.

**Simple example:**

Imagine three developers are working on the same application.

- Developer A works on login.
- Developer B works on signup.
- Developer C works on the dashboard.

Whenever code changes are pushed or a pull request is opened, CI can automatically run tests to check whether the changes are working as expected.

## 2. Why Do We Need CI?

Without CI:

```
Developer writes code
        ↓
Pushes code
        ↓
Manual testing
        ↓
Problems discovered later
```

With CI:

```
Developer writes code
        ↓
Pushes code
        ↓
Automated checks
        ↓
Results: Pass or Fail
```

**Benefits of CI:**

- Detects bugs early.
- Reduces repetitive manual testing.
- Checks whether new changes break existing functionality.
- Provides faster feedback to developers.
- Improves code quality.

## 3. How Does CI Work?

A basic CI pipeline follows these steps:

```
Developer
    ↓
Git Push / Pull Request
    ↓
CI Pipeline Starts
    ↓
Checkout Code
    ↓
Set Up Environment
    ↓
Install Dependencies
    ↓
Build and Run Tests
    ↓
Pass or Fail
```

### Understanding the steps

1. **Git Push / Pull Request:** A developer pushes code or creates a pull request.
2. **Checkout Code:** The CI runner obtains the repository code.
3. **Set Up Environment:** Required software, such as Python or Node.js, is configured.
4. **Install Dependencies:** Required libraries and packages are installed.
5. **Build and Test:** The project is built if needed, and automated tests are executed.
6. **Pass or Fail:** The pipeline reports whether the configured checks succeeded.

**Main question CI answers:**

"Does this code pass our automated checks?"

A passing pipeline does not guarantee that the application is bug-free. It means the checks configured in the pipeline have passed.

## 4. What Is GitHub Actions?

GitHub Actions is an automation platform provided by GitHub.

We can use it to automate tasks such as:

- Running tests.
- Building applications.
- Checking code quality.
- Deploying applications.

For our example, we will use GitHub Actions to implement CI.

### Workflow File Location

```
project/
└── .github/
    └── workflows/
        └── ci.yml
```

The `ci.yml` file defines when the workflow runs and what tasks it executes.

## 5. Understanding a CI Workflow

Example: A simple Python project using pytest.

```
name: CI

on:
  push:
    branches:
      - main

  pull_request:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.12"

      - name: Install pytest
        run: python -m pip install pytest

      - name: Run tests
        run: python -m pytest
```

### Important parts

**A. `name`**

```
name: CI
```

Defines the workflow name displayed in GitHub Actions.

**B. `on` — Trigger**

```
on:
  push:
    branches:
      - main
```

Defines when the workflow starts.

This example also runs when a pull request targets `main`.

**C. `jobs`**

```
jobs:
  test:
```

A job is a group of steps that execute on a runner. Here, `test` is the job ID.

**D. `runs-on` — Runner**

```
runs-on: ubuntu-latest
```

GitHub provides a hosted Ubuntu machine to execute the job.

**E. `steps`**

Steps are individual tasks executed within the job.

| Step | Purpose |
| --- | --- |
| `actions/checkout@v4` | Checks out repository code |
| `actions/setup-python@v5` | Sets up Python |
| `python -m pip install pytest` | Installs pytest |
| `python -m pytest` | Runs automated tests |

### Difference Between `uses` and `run`

**`uses`** — Runs an existing GitHub Action.

```
uses: actions/checkout@v4
```

**`run`** — Executes a shell command.

```
run: python -m pytest
```

**Remember:** `uses` = Existing action; `run` = Command.

## 6. Simple Python Testing Example

Project structure:

```
project/
├── app/
│   ├── __init__.py
│   └── main.py
├── tests/
│   └── test_main.py
└── .github/
    └── workflows/
        └── ci.yml
```

Application code — `app/main.py`

```
def hello():
    return "Hello from CI!"
```

Test code — `tests/test_main.py`

```
from app.main import hello

def test_hello():
    assert hello() == "Hello from CI!"
```

### How does this test work?

- `hello()` returns a message.
- `test_hello()` calls the function.
- `assert` checks whether the actual result matches the expected result.
- If they match, the test passes; otherwise, it fails.

### Run the test locally

```
python -m pip install pytest
python -m pytest
```

On Windows, you can also use:

```
py -m pytest
```

When you push the project to GitHub, the configured workflow can run these tests automatically.

**Important:** This workflow installs pytest only. If your application requires other packages, add those dependencies to the workflow as well.

## 7. Quick Revision

| Term | Meaning |
| --- | --- |
| CI | Continuous Integration |
| Pipeline | A sequence of automated tasks |
| Workflow | Instructions defining automated tasks |
| Trigger | Event that starts a workflow |
| Job | Group of steps executed by a runner |
| Runner | Machine that executes the job |
| Step | Individual action or command |
| `uses` | Uses an existing GitHub Action |
| `run` | Executes a shell command |
| `pytest` | Python testing framework |

**Final point to remember:**

CI automatically checks code changes so that developers can detect problems early.
