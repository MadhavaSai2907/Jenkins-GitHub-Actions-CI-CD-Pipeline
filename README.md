# Task-1 : Jenkins CI/CD Pipeline for Flask Application

## Objective

This project demonstrates a complete CI/CD pipeline using Jenkins for a Python Flask web application. The pipeline automates the process of building, testing, and deploying the application whenever changes are pushed to the repository.

---

## Project Overview

A Jenkins pipeline is configured to:

* Automatically trigger on code changes (GitHub webhook)
* Install dependencies
* Run unit tests using pytest
* Deploy the Flask application
* Send email notifications on success/failure

---

## Tech Stack

* Python (Flask)
* Jenkins
* GitHub
* Pytest
* MongoDB (for application data)
* Gmail SMTP (for notifications)

---

## Prerequisites

Ensure the following are installed:

* Python 3.x
* pip
* Jenkins (running on EC2/Linux)
* Git
* MongoDB (running locally on port 27017)

---

## Jenkins Setup

1. Install Jenkins on a Linux/EC2 instance
2. Install required plugins:

   * Pipeline
   * Git
   * GitHub Integration
   * Email Extension Plugin
3. Configure Python and Git in Jenkins
4. Configure SMTP for email notifications using Gmail App Password

---

## Project Structure

```
.
├── app.py
├── requirements.txt
├── test_app.py
├── Jenkinsfile
├── templates/
└── README.md
```

---

## CI/CD Pipeline Stages

### 1. Build Stage

* Creates a virtual environment
* Installs dependencies from `requirements.txt`

### 2. Test Stage

* Executes unit tests using pytest
* Ensures application stability before deployment

### 3. Deploy Stage

* Runs the Flask application
* Application starts using:

  ```
  nohup python app.py &
  ```

---

## GitHub Webhook Integration

* Configured webhook to trigger Jenkins pipeline automatically
* URL used:

  ```
  http://<public-ip>:8080/github-webhook/
  ```
* Trigger condition: Push to `main` branch

---

## Email Notification Setup

* Configured using Gmail SMTP:

  * SMTP Server: smtp.gmail.com
  * Port: 587
  * TLS: Enabled
  * Authentication: App Password

  NOTE: App password can be generated through 
  
  ```https://myaccount.google.com/apppasswords```

  <img width="1624" height="843" alt="image" src="https://github.com/user-attachments/assets/5546ac03-c89a-4b4f-b017-8e6deb465058" />


* Pipeline sends:

  * Success email on successful build
  * Failure email on build failure
  
<img width="695" height="313" alt="image" src="https://github.com/user-attachments/assets/26f919e6-1818-4560-acce-cfdb739c3240" />

---

## How to Run

1. Push code to GitHub repository
2. Jenkins automatically triggers pipeline
3. Pipeline executes:

   * Build → Test → Deploy
4. Email notification is sent with build status

---

# Task-2 : Flask CI/CD Pipeline using GitHub Actions

## Overview

This project demonstrates a complete CI/CD pipeline for a Flask application using GitHub Actions. The pipeline automates testing, building, and deployment to staging and production environments.

---

## Tech Stack

* Python (Flask)
* Pytest (Testing)
* GitHub Actions (CI/CD)
* MongoDB (via Flask-PyMongo)

---

##  Branch Strategy

| Branch    | Purpose                |
| --------- | ---------------------- |
| `main`    | Production environment |
| `staging` | Pre-production testing |

---

## CI/CD Workflow

The pipeline is defined in:

```
.github/workflows/ci-cd.yml
```

### Workflow Triggers

| Action                | Trigger                     |
| --------------------- | --------------------------- |
| CI (Build & Test)     | Push to `main` or `staging` |
| Staging Deployment    | Push to `staging` branch    |
| Production Deployment | Create a GitHub Release     |

---

## Workflow Steps

### 1. Install Dependencies

* Installs required Python packages using `pip`

### 2. Run Tests

* Executes test cases using `pytest`

### 3. Build

* Prepares the application after successful tests

### 4. Deploy to Staging

* Triggered when code is pushed to `staging`

### 5. Deploy to Production

* Triggered when a release is created

---

## GitHub Secrets

Configured under:

**Settings → Secrets → Actions**

| Secret Name       | Purpose           |
| ----------------- | ----------------- |
| `STAGING_HOST`    | Staging server    |
| `STAGING_USER`    | SSH user          |
| `STAGING_SSH_KEY` | SSH private key   |
| `PROD_HOST`       | Production server |
| `PROD_USER`       | SSH user          |
| `PROD_SSH_KEY`    | SSH private key   |

>  Dummy values can be used for demonstration.

---

## Running Tests Locally

```bash
pip install -r requirements.txt
pytest
```

---

## How to Trigger Pipeline

### Staging Deployment

```bash
git checkout staging
git push origin staging
```

---

### Production Deployment

1. Go to **GitHub → Releases**
2. Click **Create new release**
3. Add:

   * Tag: `v1.0`
   * Title: `First Release`
4. Click **Publish release**

---

## Workflow Screenshots

### CI Pipeline Success



---

###  Staging Deployment

<img width="1880" height="691" alt="image" src="https://github.com/user-attachments/assets/b062f379-e74e-4244-a4c5-eda6b8e08eca" />


---

###  Production Deployment

<img width="1533" height="773" alt="image" src="https://github.com/user-attachments/assets/d5af37a7-f638-4ecc-93bf-cb17edd2d49c" />


---

##  Project Structure

```
project/
│
├── app.py
├── requirements.txt
├── tests/
│   └── test_app.py
├── templates/
├── .github/
│   └── workflows/
│       └── ci-cd.yml
└── README.md
```

---



