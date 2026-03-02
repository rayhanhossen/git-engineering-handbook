# CI/CD Pipelines: GitHub Actions & GitLab CI

Continuous Integration and Continuous Deployment (CI/CD) automate the process of testing, building, and deploying your code every time you push a commit.



To create a pipeline, you need two things:

1. **The Configuration File:** A YAML file in your repository telling the system *what* to do.
2. **The Runner:** The actual server or virtual machine that executes the instructions in your YAML file. Both GitHub and GitLab provide free shared runners, but you can also host your own.

---

## Part 1: GitHub Actions (GitHub's CI/CD)

GitHub Actions uses **Workflows** made up of **Jobs** and **Steps**.

### 1. Writing a GitHub CI/CD Pipeline
To create a pipeline, create a file at this exact path in your repository: 
`.github/workflows/main.yml`

**Example `.yml` File:**
```yaml
name: Django CI Pipeline

# 1. Triggers: When should this run?
on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

# 2. Jobs: What should it do?
jobs:
  build-and-test:
    runs-on: ubuntu-latest # Uses GitHub's free shared runner

    steps:
      # Step 1: Get the code from the repo
      - name: Checkout Code
        uses: actions/checkout@v4

      # Step 2: Set up the Python environment
      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11' # Specify your Django project's Python version
          cache: 'pip' # Speeds up future runs by caching dependencies

      # Step 3: Install dependencies
      - name: Install Dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt

      # Step 4: Run environment checks and migrations
      - name: Check Migrations
        run: |
          python manage.py makemigrations --check --dry-run
          python manage.py migrate

      # Step 5: Run the Django test suite
      - name: Run Tests
        run: |
          python manage.py test

```

### 2. Setting Up a GitHub Self-Hosted Runner

If you want to run GitHub Actions on your own private server (like an AWS EC2 instance or a local machine) instead of GitHub's free servers:

1. Go to your GitHub Repository.
2. Click **Settings** > **Actions** > **Runners**.
3. Click the green **New self-hosted runner** button.
4. Select your server's Operating System (e.g., Linux).
5. GitHub will generate a list of terminal commands. SSH into your server and paste those commands one by one to download, configure, and start the runner.
6. In your `.yml` file, change `runs-on: ubuntu-latest` to `runs-on: self-hosted`.

---

## Part 2: GitLab CI/CD

GitLab uses a slightly different terminology, relying heavily on **Stages** to define the order of execution.

### 1. Writing a GitLab CI/CD Pipeline

To create a pipeline, create a file at the exact root of your repository named:
`.gitlab-ci.yml`

**Example `.yml` File:**

```yaml
# 1. Stages: Define the exact order of operations
stages:
  - install
  - test
  - build

# 2. Jobs: Define what happens in each stage
install_dependencies:
  stage: install
  image: python:3.11 # Uses a Python Docker image as the runner environment
  script:
    - echo "Installing dependencies..."
    - python -m venv venv # Create a virtual environment
    - source venv/bin/activate # Activate it
    - pip install -r requirements.txt
  artifacts:
    paths:
      - venv/ # Save the virtual environment to pass to the next stages

run_unit_tests:
  stage: test
  image: python:3.11
  script:
    - echo "Running Django tests..."
    - source venv/bin/activate # Reactivate the environment from the artifact
    - python manage.py makemigrations --check --dry-run # Ensure models match DB
    - python manage.py test

prepare_production_build:
  stage: build
  image: python:3.11
  script:
    - echo "Preparing Django for production..."
    - source venv/bin/activate
    - python manage.py collectstatic --noinput # Gather static files (CSS, JS)
    - python manage.py check --deploy # Run Django's security/deployment checks
  only:
    - main # Only run this job when pushing to the main branch

```

### 2. Setting Up a GitLab Runner

GitLab relies heavily on external runners. To set one up on your own server:

1. **Install GitLab Runner on your server:**
```bash
# For Debian/Ubuntu
sudo apt-get install gitlab-runner

```


2. **Get your Registration Token:**
Go to your GitLab Repository > **Settings** > **CI/CD** > Expand the **Runners** section. Copy the Registration Token.
3. **Register the Runner on your server:**
Run the following command on your server:
```bash
sudo gitlab-runner register

```


4. **Follow the prompts:**
* **URL:** `https://gitlab.com/` (or your self-hosted GitLab URL)
* **Token:** Paste the token you copied.
* **Executor:** Type `docker` (this is the most common and flexible) and provide a default image like `ubuntu:latest`.



---

## Summary: How to actually trigger them?

Once you have created either `.github/workflows/main.yml` or `.gitlab-ci.yml` and committed it to your repository, **you do not need to manually start the CI/CD pipeline.**

Simply run your daily Git commands:

```bash
git add .
git commit -m "ci: add initial pipeline configuration"
git push origin main

```