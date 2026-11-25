# Loan Management System

A Django-based web application for managing customer registration, loan applications, loan approvals, EMI payments, and repayment records. The project includes separate customer and administrator workflows, loan analytics, and PDF document generation.

## Features

### Customer
- Register with personal, contact, address, employment, identity, and bank details
- Log in and view a customer dashboard
- Submit loan applications with loan type, amount, duration, and purpose
- Track the status of submitted applications
- View approved loan details and EMI information
- Make EMI payment entries and view payment history
- Check paid and remaining EMI counts
- Download EMI payment receipts in PDF format
- Download a loan closure certificate after all EMIs are recorded as paid
- Use the EMI calculator

### Administrator
- Access an administrator login and dashboard
- View overall customer and loan counts
- View pending, approved, and rejected loan applications
- Review loan applications and record approval details
- Calculate EMI during loan approval
- View loan analytics, including loan counts and approved amounts

> **Note:** The repository currently implements standard Django views and URL routes. It does not currently expose a documented REST API.

## Technology Stack

| Area | Technology |
|---|---|
| Backend | Python, Django 5.2.9 |
| Frontend | HTML5, CSS, JavaScript, Django Templates |
| Database | MySQL |
| ORM | Django ORM |
| PDF generation | ReportLab |
| Image uploads | Django `ImageField` (requires Pillow) |

## Project Structure

```text
loan-management-project/
├── loan_app/
│   ├── migrations/
│   ├── models.py
│   ├── views.py
│   ├── urls.py
│   ├── admin.py
│   └── tests.py
├── loan_project/
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
├── media/
├── templates/
│   ├── home.html
│   ├── register.html
│   ├── login.html
│   ├── dashboard.html
│   ├── apply_loan.html
│   ├── loan_status.html
│   ├── admin_login.html
│   ├── admin_dashboard.html
│   ├── all_loans.html
│   ├── approve_loan.html
│   ├── emi_calculator.html
│   ├── emi_payment.html
│   ├── pay_emi.html
│   ├── payment_history.html
│   ├── emi_status.html
│   ├── loan_details.html
│   └── loan_analytics.html
├── manage.py
└── .gitignore
```

## Data Models

The application defines four main Django models:

- **AccountHolder** – stores customer profile, contact, address, identity-document, bank, and employment information.
- **LoanApplication** – stores the loan type, requested amount, duration, purpose, application date, and status.
- **LoanApproval** – stores the approved amount, interest rate, EMI, duration, and approval date.
- **Payment** – stores EMI payment amount, payment method, payment date, and EMI number.

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Hamsa-C/loan-management-project.git
cd loan-management-project
```

### 2. Create and activate a virtual environment

**Windows**

```bash
python -m venv venv
venv\Scripts\activate
```

**macOS / Linux**

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
pip install "Django==5.2.9" mysqlclient Pillow reportlab
```

The repository does not currently include a `requirements.txt` file. The command above lists the main packages indicated by the source code and database configuration.

### 4. Configure MySQL

Make sure MySQL Server is installed and running. Create the database:

```sql
CREATE DATABASE loan_project;
```

The current Django settings use a MySQL database named `loan_project` and a local MySQL server. Before running the application, update `DATABASES` in `loan_project/settings.py` with your own MySQL username and password.

For safer configuration, move database credentials and Django's `SECRET_KEY` into environment variables rather than committing them to source control. Do not use the repository's current development settings in production.

### 5. Apply migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

### 6. Run the development server

```bash
python manage.py runserver
```

Open the application at:

```text
http://127.0.0.1:8000/
```

The Django administration site is available at:

```text
http://127.0.0.1:8000/admin/
```

To create a Django admin account:

```bash
python manage.py createsuperuser
```

## Main Application Routes

| Route | Purpose |
|---|---|
| `/` | Home page |
| `/register/` | Customer registration |
| `/login/` | Customer login |
| `/dashboard/` | Customer dashboard |
| `/apply-loan/` | Submit a loan application |
| `/loan-status/` | View loan application status |
| `/emi-calculator/` | EMI calculator |
| `/emi-payment/` | View approved loans for EMI payment |
| `/payment-history/` | View payment history |
| `/emi-status/` | View EMI repayment status |
| `/admin-login/` | Application administrator login |
| `/admin-dashboard/` | Administrator dashboard |
| `/all-loans/` | View all loan applications |
| `/pending-loans/` | View pending applications |
| `/approved-loans/` | View approved applications |
| `/loan-analytics/` | View loan analytics |

Some routes require an application session or a loan record ID. See `loan_app/urls.py` for the complete route definitions.

## Important Security Notes

This repository is a learning/demo project and should not be deployed with its current security configuration. Before using real customer information or deploying it:

- Never store customer passwords as plain text. Use Django's authentication system and password hashing.
- Move the database password and Django secret key to environment variables; rotate any credentials that have been committed.
- Replace the hard-coded administrator login with Django authentication, permissions, and role-based access control.
- Add authorization checks to every view that reads or changes a loan, approval, payment, receipt, or certificate. Verify that a customer can access only their own records.
- Validate and sanitize uploaded files and user-submitted data.
- Use `DEBUG = False`, configure `ALLOWED_HOSTS`, HTTPS, secure cookies, and Django's deployment checklist before production use.
- Do not use real Aadhaar, PAN, bank, or other sensitive personal data in a public demo.

## Future Improvements

- Add a `requirements.txt` file for reproducible installation
- Move secrets and database configuration to environment variables
- Use Django's built-in authentication and permissions
- Add form validation and automated tests for registration, loan approval, EMI calculations, and payments
- Add pagination, search, and filtering to administrator loan lists
- Add payment gateway integration if actual online payments are required

## Author

**Hamsa C**

GitHub: [Hamsa-C](https://github.com/Hamsa-C)
