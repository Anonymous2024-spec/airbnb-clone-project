# AirBnB Clone Project

## Project Overview

The AirBnB Clone Project is a comprehensive backend system designed to replicate the core functionalities of the popular accommodation booking platform, Airbnb. This project focuses on building a robust, scalable, and secure REST API that handles property listings, user management, bookings, payments, and reviews.

### Project Goals

- Develop a production-ready backend system with industry-standard architecture
- Implement secure authentication and authorization mechanisms
- Design and build a relational database that efficiently handles complex relationships
- Create RESTful APIs following best practices
- Integrate payment processing and booking management systems
- Apply CI/CD practices for automated testing and deployment
- Master backend development patterns and scalable system design

### Tech Stack

- **Backend Framework**: Django (Python)
- **Database**: PostgreSQL
- **API Architecture**: RESTful API
- **Authentication**: JWT (JSON Web Tokens)
- **ORM**: Django ORM
- **Version Control**: Git & GitHub
- **CI/CD**: GitHub Actions
- **Containerization**: Docker

---

## Team Roles and Responsibilities

As this is a solo project, I will be taking on multiple roles throughout the development lifecycle:

### Backend Developer
**Responsibilities:**
- Design and implement RESTful API endpoints
- Develop business logic for core features (bookings, payments, listings)
- Integrate third-party services and APIs
- Write clean, maintainable, and well-documented code
- Implement error handling and logging mechanisms

### Database Administrator
**Responsibilities:**
- Design the database schema with proper normalization
- Create and manage database migrations
- Optimize queries for performance
- Implement database indexing strategies
- Ensure data integrity and consistency through constraints

### DevOps Engineer
**Responsibilities:**
- Set up CI/CD pipelines using GitHub Actions
- Configure Docker containers for development and production environments
- Manage environment variables and secrets
- Automate testing and deployment processes
- Monitor application performance and logs

### Security Engineer
**Responsibilities:**
- Implement authentication and authorization systems
- Secure API endpoints against common vulnerabilities (OWASP Top 10)
- Manage sensitive data encryption
- Implement rate limiting and request throttling
- Conduct security audits and vulnerability assessments

### Quality Assurance Engineer
**Responsibilities:**
- Write unit tests and integration tests
- Perform API testing and validation
- Create test documentation
- Ensure code coverage meets project standards
- Conduct manual testing of critical features

---

## Technology Stack

### Django
**Purpose:** Django is a high-level Python web framework that serves as the backbone of our backend system. It provides a robust ORM, built-in authentication, and a powerful admin interface. Django enables rapid development while maintaining security and scalability.

### PostgreSQL
**Purpose:** PostgreSQL is our primary relational database management system. It offers advanced features like JSONB support, full-text search, and excellent performance with complex queries. PostgreSQL ensures data integrity through ACID compliance and supports the complex relationships required for our booking platform.

### Django REST Framework (DRF)
**Purpose:** DRF extends Django to simplify the creation of RESTful APIs. It provides serializers for data validation, viewsets for CRUD operations, and built-in authentication classes. DRF enables us to build a clean, browsable API with minimal code.

### JWT (JSON Web Tokens)
**Purpose:** JWT is used for secure, stateless authentication across our API. It allows users to authenticate once and receive a token that can be used for subsequent requests, eliminating the need for session storage and enabling horizontal scaling.

### Docker
**Purpose:** Docker containerizes our application, ensuring consistency across development, testing, and production environments. It simplifies deployment, manages dependencies, and allows for easy scaling of services.

### GitHub Actions
**Purpose:** GitHub Actions automates our CI/CD pipeline, running tests on every commit, performing code quality checks, and deploying to staging/production environments. This ensures code reliability and accelerates the development workflow.

### Celery (Task Queue)
**Purpose:** Celery handles asynchronous tasks such as sending email notifications, processing payments, and generating reports. It improves API response times by offloading time-consuming operations to background workers.

### Redis
**Purpose:** Redis serves as a caching layer and message broker for Celery. It speeds up frequently accessed data retrieval and manages task queues for asynchronous processing.

---

## Database Design

The database architecture follows a normalized relational model designed to handle the complex interactions between users, properties, bookings, and payments.

### Key Entities

#### 1. User
**Fields:**
- `user_id` (Primary Key, UUID): Unique identifier for each user
- `email` (String, Unique): User's email address for authentication
- `password_hash` (String): Securely hashed password
- `first_name` (String): User's first name
- `last_name` (String): User's last name
- `phone_number` (String): Contact number
- `profile_picture` (String): URL to user's profile image
- `is_host` (Boolean): Indicates if user can list properties
- `created_at` (DateTime): Account creation timestamp
- `updated_at` (DateTime): Last profile update timestamp

**Relationships:**
- A User can have multiple Properties (One-to-Many as host)
- A User can make multiple Bookings (One-to-Many as guest)
- A User can write multiple Reviews (One-to-Many)

#### 2. Property
**Fields:**
- `property_id` (Primary Key, UUID): Unique identifier for each property
- `host_id` (Foreign Key → User): Reference to the property owner
- `title` (String): Property listing title
- `description` (Text): Detailed property description
- `location` (String): Property address/location
- `price_per_night` (Decimal): Nightly rental rate
- `number_of_guests` (Integer): Maximum guest capacity
- `number_of_bedrooms` (Integer): Total bedrooms
- `number_of_bathrooms` (Integer): Total bathrooms
- `amenities` (JSON/Array): List of available amenities
- `availability_status` (Boolean): Whether property is currently bookable
- `created_at` (DateTime): Listing creation timestamp
- `updated_at` (DateTime): Last update timestamp

**Relationships:**
- A Property belongs to one User/Host (Many-to-One)
- A Property can have multiple Bookings (One-to-Many)
- A Property can have multiple Reviews (One-to-Many)

#### 3. Booking
**Fields:**
- `booking_id` (Primary Key, UUID): Unique identifier for each booking
- `property_id` (Foreign Key → Property): Reference to booked property
- `guest_id` (Foreign Key → User): Reference to the guest making the booking
- `check_in_date` (Date): Booking start date
- `check_out_date` (Date): Booking end date
- `number_of_guests` (Integer): Total guests for the booking
- `total_price` (Decimal): Calculated total cost
- `booking_status` (Enum): Status (pending, confirmed, cancelled, completed)
- `created_at` (DateTime): Booking creation timestamp
- `updated_at` (DateTime): Last update timestamp

**Relationships:**
- A Booking belongs to one Property (Many-to-One)
- A Booking belongs to one User/Guest (Many-to-One)
- A Booking has one Payment (One-to-One)

#### 4. Review
**Fields:**
- `review_id` (Primary Key, UUID): Unique identifier for each review
- `property_id` (Foreign Key → Property): Reference to reviewed property
- `user_id` (Foreign Key → User): Reference to the reviewer
- `rating` (Integer): Rating score (1-5 stars)
- `comment` (Text): Written review content
- `created_at` (DateTime): Review creation timestamp
- `updated_at` (DateTime): Last update timestamp

**Relationships:**
- A Review belongs to one Property (Many-to-One)
- A Review belongs to one User (Many-to-One)

#### 5. Payment
**Fields:**
- `payment_id` (Primary Key, UUID): Unique identifier for each payment
- `booking_id` (Foreign Key → Booking): Reference to associated booking
- `amount` (Decimal): Payment amount
- `payment_method` (Enum): Method (credit_card, debit_card, paypal, stripe)
- `payment_status` (Enum): Status (pending, completed, failed, refunded)
- `transaction_id` (String): External payment gateway transaction reference
- `payment_date` (DateTime): When payment was processed
- `created_at` (DateTime): Record creation timestamp

**Relationships:**
- A Payment belongs to one Booking (One-to-One)

### Entity Relationship Summary

```
User (1) ──────< (Many) Property
User (1) ──────< (Many) Booking
User (1) ──────< (Many) Review

Property (1) ──────< (Many) Booking
Property (1) ──────< (Many) Review

Booking (1) ──────── (1) Payment
```

---

## Feature Breakdown

### 1. User Management
The user management system handles all user-related operations including registration, authentication, and profile management. Users can sign up as guests or hosts, manage their personal information, and maintain secure access to their accounts. This feature implements JWT-based authentication for secure, stateless sessions and includes password reset functionality, email verification, and role-based access control to differentiate between guests and hosts.

### 2. Property Listings Management
This feature allows hosts to create, update, and manage their property listings. Hosts can add detailed descriptions, set pricing, upload photos, specify amenities, and manage availability calendars. The system supports advanced filtering and search capabilities, enabling guests to find properties based on location, price range, amenities, and availability. Property validation ensures all listings meet quality standards before being published.

### 3. Booking System
The booking system manages the entire reservation lifecycle from search to completion. It handles date availability checks, prevents double bookings through database constraints, calculates pricing based on duration and seasonal rates, and manages booking status transitions (pending, confirmed, cancelled, completed). The system includes conflict detection to ensure properties aren't double-booked and sends automated notifications to both guests and hosts at key stages of the booking process.

### 4. Payment Processing
This feature integrates with payment gateways to handle secure financial transactions. It processes booking payments, manages refunds for cancellations, handles payment failures gracefully, and maintains detailed payment records for accounting purposes. The system implements PCI compliance standards, secures sensitive payment data, and provides transaction history for both users and administrators. Support for multiple payment methods (credit cards, PayPal, Stripe) ensures flexibility for users.

### 5. Review and Rating System
The review system allows guests to rate and review properties after their stay, fostering trust and transparency in the platform. It implements validation to ensure only verified guests who have completed bookings can leave reviews, prevents duplicate reviews, and calculates aggregate ratings for properties. Hosts can respond to reviews, and the system includes moderation capabilities to flag inappropriate content. Reviews significantly influence property visibility and booking decisions.

### 6. Search and Filter Functionality
Advanced search capabilities enable users to find properties that match their specific needs. The system supports filtering by location, price range, dates, number of guests, amenities, property type, and ratings. It implements efficient database queries with proper indexing to ensure fast search results even with large datasets. The search feature includes pagination, sorting options, and may incorporate full-text search for keyword-based queries.

### 7. Admin Dashboard
The admin dashboard provides comprehensive oversight and management capabilities for platform administrators. It offers analytics and reporting on bookings, revenue, user activity, and property performance. Admins can manage user accounts, moderate content, handle disputes, and configure system settings. The dashboard includes tools for monitoring system health, managing featured listings, and generating financial reports for business intelligence.

---

## API Security

Security is paramount in the AirBnB Clone project, especially given the sensitive nature of user data, financial transactions, and property information. The following security measures are implemented to protect the system:

### Authentication & Authorization

**Implementation:**
- JWT (JSON Web Tokens) for stateless authentication
- Token expiration and refresh mechanisms
- Role-based access control (RBAC) for guests, hosts, and admins
- Multi-factor authentication (MFA) for sensitive operations

**Importance:**
Authentication ensures that only legitimate users can access the system, while authorization controls what actions each user can perform. This is critical for protecting user accounts from unauthorized access, preventing malicious actors from manipulating bookings or payments, and ensuring hosts can only manage their own properties. Without robust authentication, the entire platform would be vulnerable to account takeovers and data breaches.

### Data Encryption

**Implementation:**
- HTTPS/TLS for all API communications
- Password hashing using bcrypt or Argon2
- Encryption of sensitive data at rest (payment information, personal details)
- Secure storage of API keys and secrets using environment variables

**Importance:**
Encryption protects sensitive user data both in transit and at rest. Payment information, personal identification details, and authentication credentials must never be stored or transmitted in plain text. This prevents data interception during transmission, protects against database breaches, and ensures compliance with data protection regulations (GDPR, PCI DSS). Compromised user data can lead to identity theft, financial fraud, and severe legal consequences.

### Input Validation & Sanitization

**Implementation:**
- Server-side validation of all user inputs
- SQL injection prevention through parameterized queries (Django ORM)
- Cross-Site Scripting (XSS) protection through output encoding
- Request payload size limits to prevent denial-of-service attacks

**Importance:**
Input validation is the first line of defense against injection attacks and malicious data. Without proper validation, attackers could inject malicious SQL queries to access or manipulate database records, execute scripts in other users' browsers (XSS), or corrupt data integrity. In a booking platform, this could lead to unauthorized bookings, price manipulation, or exposure of sensitive property and user information.

### Rate Limiting & Throttling

**Implementation:**
- API request rate limits per user/IP address
- Progressive throttling for repeated failed authentication attempts
- CAPTCHA implementation for sensitive endpoints
- DDoS protection through request queuing

**Importance:**
Rate limiting prevents abuse of the API and protects system resources. Without throttling, attackers could launch brute-force attacks to guess passwords, overwhelm the system with requests causing service disruption, or scrape large amounts of data. For a booking platform, this also prevents bots from monopolizing property bookings during peak times, ensuring fair access for legitimate users.

### API Security Headers

**Implementation:**
- Content Security Policy (CSP) headers
- X-Frame-Options to prevent clickjacking
- X-Content-Type-Options to prevent MIME-type sniffing
- Strict-Transport-Security (HSTS) for enforced HTTPS

**Importance:**
Security headers provide additional layers of defense against common web vulnerabilities. They prevent the API from being embedded in malicious sites, protect against MIME-type confusion attacks, and ensure all communications occur over secure channels. These headers are essential for maintaining the integrity of the application's security posture.

### Audit Logging & Monitoring

**Implementation:**
- Comprehensive logging of authentication attempts, API requests, and data modifications
- Real-time monitoring and alerting for suspicious activities
- Secure log storage with tamper-proof mechanisms
- Regular security audits and penetration testing

**Importance:**
Audit logs provide visibility into system activities and are crucial for detecting security breaches, investigating incidents, and maintaining compliance with regulatory requirements. In a booking platform handling financial transactions, audit trails are essential for dispute resolution, fraud detection, and forensic analysis. Monitoring enables rapid response to security incidents before significant damage occurs.

---

## CI/CD Pipeline

### What is CI/CD?

CI/CD stands for Continuous Integration and Continuous Deployment/Delivery. It's a set of practices that automate the software development lifecycle, from code integration to production deployment.

**Continuous Integration (CI)** automatically tests and validates code changes whenever developers commit to the repository, ensuring that new code integrates smoothly with the existing codebase and doesn't introduce bugs.

**Continuous Deployment/Delivery (CD)** automates the release process, deploying tested and validated code to staging and production environments with minimal manual intervention.

### Why CI/CD is Important for This Project

1. **Early Bug Detection**: Automated testing catches issues immediately after code is committed, reducing the cost and time of fixing bugs later in the development cycle.

2. **Code Quality Assurance**: Automated linting, formatting checks, and security scans ensure consistent code quality and adherence to best practices.

3. **Faster Development Cycles**: Automation eliminates manual testing and deployment tasks, allowing for more frequent releases and faster feature delivery.

4. **Reduced Deployment Risk**: Automated deployments follow consistent processes, reducing human error and making rollbacks easier if issues arise.

5. **Team Collaboration**: CI/CD provides immediate feedback on code changes, facilitating better collaboration and preventing integration conflicts.

6. **Reliable Releases**: Every deployment goes through the same automated testing and validation pipeline, ensuring production releases are stable and predictable.

### CI/CD Tools and Workflow

#### Primary Tools

**GitHub Actions**
Our main CI/CD platform, integrated directly with our GitHub repository. GitHub Actions executes automated workflows triggered by events like push, pull requests, and releases. It's chosen for its seamless integration, free tier for public repositories, and extensive marketplace of pre-built actions.

**Docker**
Containerizes the application, ensuring consistency across development, testing, and production environments. Docker eliminates "it works on my machine" problems and simplifies deployment by packaging the application with all its dependencies.

**pytest & Coverage.py**
Automated testing framework for Python/Django applications. Pytest runs unit tests, integration tests, and generates code coverage reports to ensure adequate test coverage.

**PostgreSQL (Test Database)**
A separate test database instance is created for running integration tests, ensuring tests don't affect production data and can run in isolation.

#### CI/CD Pipeline Stages

**Stage 1: Code Quality Checks**
- Linting with flake8/pylint to enforce coding standards
- Code formatting verification with black
- Security vulnerability scanning with bandit
- Dependency vulnerability checks

**Stage 2: Automated Testing**
- Unit tests execution for individual components
- Integration tests for API endpoints
- Database migration tests
- Code coverage analysis (minimum 80% threshold)

**Stage 3: Build & Containerization**
- Docker image building
- Image optimization and layer caching
- Tagging with version numbers and commit SHAs
- Push to Docker registry

**Stage 4: Deployment**
- Automatic deployment to staging environment on main branch
- Manual approval gate for production deployment
- Database migration execution
- Health checks and smoke tests post-deployment
- Rollback mechanisms if deployment fails

**Stage 5: Monitoring & Notifications**
- Deployment status notifications via email/Slack
- Performance monitoring alerts
- Error tracking and logging aggregation

### Sample GitHub Actions Workflow

The CI/CD pipeline is defined in `.github/workflows/main.yml` and triggers on every push to the repository and on pull requests. It runs parallel jobs for testing and quality checks, builds Docker images for successful builds, and deploys to staging/production based on branch and approval gates.

---

## Getting Started

### Prerequisites
- Python 3.11+
- PostgreSQL 14+
- Docker & Docker Compose
- Git

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/airbnb-clone-project.git
cd airbnb-clone-project

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Set up environment variables
cp .env.example .env
# Edit .env with your configuration

# Run migrations
python manage.py migrate

# Create superuser
python manage.py createsuperuser

# Run development server
python manage.py runserver
```

### Running Tests

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=.

# Run specific test file
pytest tests/test_users.py
```

---

## Project Structure

```
airbnb-clone-project/
├── .github/
│   └── workflows/
│       └── main.yml
├── apps/
│   ├── users/
│   ├── properties/
│   ├── bookings/
│   ├── reviews/
│   └── payments/
├── config/
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── tests/
├── docker/
├── docs/
├── .env.example
├── .gitignore
├── docker-compose.yml
├── Dockerfile
├── manage.py
├── requirements.txt
└── README.md
```

---

## Contributing

This is a solo learning project, but feedback and suggestions are welcome! If you notice any issues or have recommendations, feel free to open an issue.

---

## License

This project is created for educational purposes as part of the ALX Backend Specialization program.

---

## Acknowledgments

- ALX Africa for the comprehensive backend curriculum
- Django and PostgreSQL communities for excellent documentation
- Open-source contributors whose tools make this project possible

---

**Project Status**: 🚧 In Development

**Author**: Naana Shifah  
**Course**: ALX Backend Specialization  
**Start Date**: October 13, 2025  
**Target Completion**: February 20, 2025
