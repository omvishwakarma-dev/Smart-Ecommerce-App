# Smart Ecommerce App

A full-stack e-commerce web application built with Flask, Celery, Redis and Vue.js. It supports product management, monthly report generation, daily reminders, and CSV export, with role-based access control.

## Tech Stack
- **Flask**: Python backend framework
- **Celery**: asynchronous task queue for background jobs
- **Redis**: message broker and result backend for Celery
- **Vue CLI**: frontend framework tooling
- **Flask-Security**: authentication and roles
- **Flask-CORS**: cross-origin requests
- **SQLite**: database
- **CSS**: styling

## Features
- User, manager and admin roles with role-based access control
- Category and product management with approval requests
- Shopping cart and checkout
- Background tasks with Celery: daily reminders and monthly reports
- Automated reminders for inactive users
- Export of product data to CSV

## Architecture
The app follows the **MVC** pattern:
- **Model:** SQLAlchemy models define the database schema
- **View:** Vue frontend
- **Controller:** Flask routes and Celery tasks

## Database Schema
1. **User:** email, username, password, roles
2. **Role:** user roles and access levels
3. **Request:** approval requests
4. **Category:** product categories
5. **Category Requests:** category creation requests
6. **Category Update Request:** category update requests
7. **Category Delete Request:** category deletion requests
8. **Product:** name, expiry date, price, stock
9. **Cart:** user shopping cart
10. **BoughtProducts:** purchase records

## API Overview
- User and manager sign-up/login
- Category management (add, modify, delete, request approvals)
- Product management (add, modify, delete, purchase)
- Cart operations (add, remove, checkout)
- Role-based dashboards
- OpenAPI spec: `Backend/api.yaml`

## Screenshots
![Login](screenshots/login.png)
![Dashboard](screenshots/dashboard.png)
![Cart](screenshots/cart.png)

## Setup

### Prerequisites
- WSL (Windows Subsystem for Linux)
- Python 3, Node.js and npm, Redis, MailHog

### Install
1. Clone the repository.
2. Open a WSL terminal and set up the backend:
   ```bash
   cd Backend
   source venv/bin/activate
   pip install -r requirements.txt
   ```
3. Set up the frontend:
   ```bash
   cd freshcart
   npm install
   ```

### Run
Open 6 terminals:

**1. Frontend**
```bash
cd freshcart
npm run serve
```

**2. Backend**
```bash
cd Backend
source venv/bin/activate
python app.py
```

**3. Redis**
```bash
redis-server
```

**4. Celery worker**
```bash
cd Backend
celery -A app.celery worker -l info
```

**5. Celery beat**
```bash
cd Backend
celery -A app.celery beat --max-interval 2 -l info
```

**6. MailHog (email testing)**
```bash
~/go/bin/MailHog
```

### Access
- Backend: http://127.0.0.1:5000/
- Frontend: http://localhost:8080/

## Author
Om Vishwakarma