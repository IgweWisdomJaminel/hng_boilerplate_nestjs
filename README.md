# Authentication and User Management API

API DESIGN LINK: https://app.swaggerhub.com/apis/IGWEWISDOM20001_1/api-documentation/1.0.0
DATABASE DESIGN LINK: https://dbdiagram.io/d/Hng_stage3-669165369939893daecaa02a


## Table of Contents
1. [Introduction](#introduction)
2. [Project Structure](#project-structure)
3. [API Documentation](#api-documentation)
4. [Security](#security)
5. [Dependencies](#dependencies)
6. [Setup and Installation](#setup-and-installation)
7. [Running the Application](#running-the-application)
8. [Testing](#testing)
9. [Contributing](#contributing)
10. [License](#license)

## Introduction

This project is a comprehensive Authentication and User Management API built using Java Spring Boot. It provides a robust set of endpoints for user registration, authentication, password management, social login, and various administrative functions.

## Project Structure

src/
├── main/
│ ├── java/
│ │ └── com/
│ │ └── yourcompany/
│ │ └── authapi/
│ │ ├── config/
│ │ ├── controller/
│ │ ├── dto/
│ │ ├── exception/
│ │ ├── model/
│ │ ├── repository/
│ │ ├── service/
│ │ └── util/
│ └── resources/
│ ├── application.properties
│ └── templates/
└── test/
└── java/
└── com/
└── yourcompany/
└── authapi/
├── controller/
└── service/

gradle
Copy

## API Documentation

### Endpoints

1. **User Management**
   - POST /api/register: Register a new user
   - POST /api/login: User login
   - POST /api/logout: User logout
   - GET /api/auth/me: Get authenticated user details
   - GET /api/users: Get all users
   - POST /api/users: Create a new user
   - GET /api/users/{id}: Get user details
   - PUT /api/users/{id}: Update user details
   - DELETE /api/users/{id}: Delete a user

2. **Password Management**
   - POST /api/password/forgot: Send password reset link
   - POST /api/password/reset: Reset password
   - POST /api/password/change: Change password

3. **Authentication**
   - POST /api/magic-link: Send magic link for login
   - POST /api/auth/social: Social login (Google, Facebook, etc.)

4. **Email Templates**
   - GET /api/email/templates: Get all email templates
   - POST /api/email/templates: Create a new email template
   - PUT /api/email/templates/{id}: Update an email template
   - DELETE /api/email/templates/{id}: Delete an email template

5. **Payments**
   - POST /api/payments/stripe: Create a Stripe payment
   - POST /api/payments/flutterwave: Create a Flutterwave payment
   - POST /api/payments/lemonsqueezy: Create a LemonSqueezy payment
   - POST /api/payments/initialize: Initialize a payment
   - GET /api/payments/verify: Verify a payment
   - GET /api/payments/history: Get payment history

6. **Organizations**
   - GET /api/organisations: Get all organisations
   - POST /api/organisations: Create a new organisation
   - GET /api/organisations/{id}: Get organisation details
   - PUT /api/organisations/{id}: Update organisation details
   - DELETE /api/organisations/{id}: Delete an organisation

7. **Super Admin**
   - GET /api/superadmin/users: Get all users (superadmin view)
   - GET /api/superadmin/organisations: Get all organisations (superadmin view)
   - GET /api/superadmin/payments: Get all payments (superadmin view)
   - GET /api/superadmin/activity-log: Get activity log

8. **Miscellaneous**
   - POST /api/invite: Generate an invite link
   - POST /api/notifications/push: Send a push notification

### Example Requests and Responses

#### Register a new user

Reuest:
```json
POST /api/register
{
  "userId": "user123",
  "first_name": "John",
  "last_name": "Doe",
  "username": "johndoe",
  "email": "john@example.com",
  "password": "securepassword",
  "gender": "male",
  "nationality": "USA",
  "state": "California",
  "address": "123 Main St, Anytown, CA 12345"
}
Response:

json
Copy
200 OK
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": 1,
    "userId": "user123",
    "first_name": "John",
    "last_name": "Doe",
    "username": "johndoe",
    "email": "john@example.com",
    "gender": "male",
    "nationality": "USA",
    "state": "California",
    "address": "123 Main St, Anytown, CA 12345",
    "role": "USER",
    "created_at": "2023-07-13T12:00:00Z",
    "updated_at": "2023-07-13T12:00:00Z"
  }
}
Security
This API uses JWT (JSON Web Tokens) for authentication. All authenticated endpoints require a valid JWT token to be included in the Authorization header of the request.

Copy
Authorization: Bearer <token>
Dependencies
Spring Boot Starter Web
Spring Boot Starter Data JPA
Spring Boot Starter Security
Spring Boot Starter Validation
Spring Boot Starter Mail
JSON Web Token (JWT)
MySQL Connector
Lombok
ModelMapper
Springfox Swagger UI
Setup and Installation
Clone the repository
Configure the database connection in application.properties
Run mvn clean install to build the project and download dependencies
Running the Application
Run the application using:


DATABASE 










This README provides a comprehensive overview of our  project, including its structure, API documentation, security measures, dependencies, and instructions for setup and running the application. It follows a standard README structure and includes all the necessary information for developers to understand and work with our project.
