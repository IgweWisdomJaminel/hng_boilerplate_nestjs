# Authentication and User Management API

API DESIGN LINK: [https://app.swaggerhub.com/apis/IGWEWISDOM20001_1/api-documentation/1.0.0](https://igwewisdomjaminel.github.io/SwaggerApi2/)

DATABASE DESIGN LINK: [https://dbdiagram.io/d/Hng_stage3-669165369939893daecaa02a
](https://dbdiagram.io/d/Hng_stage3-669165369939893daecaa02a)

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
│ │ └── company/
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


Database Design Documentation


To view the database design as image, follow this link:

https://dbdiagram.io/d/jam_js_boilerplate-669165369939893daecaa02a


Overview
This documentation outlines the structure and relationships of the database entities for managing users, organizations, authentication, messaging, payments, settings, activities, and more. This database is designed to support a comprehensive system with robust features.



Entities and Relationships
Users
Description: Stores information about users.
Fields:
id: Primary key, auto-increment.
userId: Unique identifier for the user.
first_name: First name of the user.
last_name: Last name of the user.
username: Username of the user, not null.
email: Email address of the user, unique, not null.
password: Password of the user, not null.
gender: Gender of the user.
nationality: Nationality of the user.
state: State of residence of the user.
address: Address of the user.
role: Role of the user, not null.
createdAt: Timestamp when the user was created, defaults to current timestamp.
updatedAt: Timestamp when the user was last updated, defaults to current timestamp.
Organizations
Description: Stores information about organizations.
Fields:
id: Primary key, auto-increment.
orgId: Unique identifier for the organization.
name: Name of the organization, not null.
description: Description of the organization.
createdAt: Timestamp when the organization was created, defaults to current timestamp.
updatedAt: Timestamp when the organization was last updated, defaults to current timestamp.
UserOrganizations
Description: Maps users to organizations.
Fields:
user_id: Foreign key referencing Users.id, not null.
organization_id: Foreign key referencing Organizations.id, not null.
Tokens
Description: Stores accessToken and refreshTokens for users.
Fields:
id: Primary key, auto-increment.
user_id: Foreign key referencing Users.id, not null.
accessToken :Used to access protected resources.
refreshToken: This is used to generate an accessToken after a previous one is expired.
createdAt: Timestamp when the token was created, defaults to current timestamp.
expiresAt: Expiry timestamp for the token, not null.
Messages
Description: Stores messages sent to users.
Fields:
id: Primary key, auto-increment.
user_id: Foreign key referencing Users.id, not null.
subject: Subject of the message.
body: Body of the message.
status: Status of the message.
createdAt: Timestamp when the message was created, defaults to current timestamp.
updatedAt: Timestamp when the message was last updated, defaults to current timestamp.
Templates
Description: Stores various templates.
Fields:
id: Primary key, auto-increment.
name: Name of the template, not null.
content: Content of the template, not null.
type: Type of the template, not null.
createdAt: Timestamp when the template was created, defaults to current timestamp.
updatedAt: Timestamp when the template was last updated, defaults to current timestamp.
Payments
Description: Stores payment transactions.
Fields:
id: Primary key, auto-increment.
user_id: Foreign key referencing Users.id, not null.
amount: Amount of the payment, not null.
currency: Currency of the payment, not null.
transaction_ref: Transaction reference, not null.
payment_method: Payment method used, not null.
payment_gateway_tx_ref: Payment gateway transaction reference.
status: Status of the payment, not null.
createdAt: Timestamp when the payment was created, defaults to current timestamp.
updatedAt: Timestamp when the payment was last updated, defaults to current timestamp.
Settings
Description: Stores user settings.
Fields:
id: Primary key, auto-increment.
user_id: Foreign key referencing Users.id, not null.
setting_type: Type of setting, (general settings, profile settings...)
key: Setting key, not null.
value: Setting value, not null.
createdAt: Timestamp when the setting was created, defaults to current timestamp.
updatedAt: Timestamp when the setting was last updated, defaults to current timestamp.
Pages
Description: Stores various static pages content.
Fields:
id: Primary key, auto-increment.
title: Title of the page, not null.
content: Content of the page, not null.
type: Type of the page, not null.
createdAt: Timestamp when the page was created, defaults to current timestamp.
updatedAt: Timestamp when the page was last updated, defaults to current timestamp.
Activities
Description: Logs user activities.
Fields:
id: Primary key, auto-increment.
user_id: Foreign key referencing Users.id, not null.
action: Description of the action performed, not null.
createdAt: Timestamp when the activity was created, defaults to current timestamp.
Invites
Description: Stores invitation information.
Fields:
id: Primary key, auto-increment.
inviter_id: Foreign key referencing Users.id, not null.
invitee_email: Email address of the invitee, not null.
token: Invitation token, not null.
status: Status of the invitation, not null.
createdAt: Timestamp when the invitation was created, defaults to current timestamp.
updatedAt: Timestamp when the invitation was last updated, defaults to current timestamp.
Notifications
Description: Stores user notifications.
Fields:
id: Primary key, auto-increment.
user_id: Foreign key referencing Users.id, not null.
message: Notification message, not null.
read: Boolean indicating if the notification is read, defaults to false.
createdAt: Timestamp when the notification was created, defaults to current timestamp.
Blogs
Description: Stores blog posts.
Fields:
id: Primary key, auto-increment.
title: Title of the blog post, not null.
content: Content of the blog post, not null.
author_id: Foreign key referencing Users.id, not null.
createdAt: Timestamp when the blog post was created, defaults to current timestamp.
updatedAt: Timestamp when the blog post was last updated, defaults to current timestamp.
Charts
Description: Stores chart data.
Fields:
id: Primary key, auto-increment.
user_id: Foreign key referencing Users.id, not null.
data: Chart data in JSON format, not null.
type: Type of chart, not null.
createdAt: Timestamp when the chart was created, defaults to current timestamp.
updatedAt: Timestamp when the chart was last updated, defaults to current timestamp.
Metadata
Description: Stores user metadata.
Fields:
id: Primary key, auto-increment.
user_id: Foreign key referencing Users.id, not null.
data: Metadata in JSON format, not null.
createdAt: Timestamp when the metadata was created, defaults to current timestamp.
Languages
Description: Stores supported languages.
Fields:
id: Primary key, auto-increment.
code: Language code, not null.
name: Language name, not null.
Regions
Description: Stores supported regions.
Fields:
id: Primary key, auto-increment.
code: Region code, not null.
name: Region name, not null.
EmailTemplates
Description: Stores email templates.
Fields:
id: Primary key, auto-increment.
name: Name of the email template, not null.
subject: Subject of the email template, not null.
body: Body of the email template, not null.
createdAt: Timestamp when the email template was created, defaults to current timestamp.
updatedAt: Timestamp when the email template was last updated, defaults to current timestamp.


Relationships
User and Organizations: Many-to-Many relationship via UserOrganizations.
User and RefreshTokens: One-to-Many relationship.
User and Messages: One-to-Many relationship.
User and Payments: One-to-Many relationship.
User and Settings: One-to-Many relationship.
User and Activities: One-to-Many relationship.
User and Notifications: One-to-Many relationship.
User and Blogs: One-to-Many relationship.
User and Charts: One-to-Many relationship.
User and Metadata: One-to-Many relationship.
User and Invites: One-to-Many relationship (inviter).













This README provides a comprehensive overview of our  project, including its structure, API documentation, security measures, dependencies, and instructions for setup and running the application. It follows a standard README structure and includes all the necessary information for developers to understand and work with our project.



License
Include a license file in the root of your project. For example, to use the MIT License, create a LICENSE file with the following content:




MIT License

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

