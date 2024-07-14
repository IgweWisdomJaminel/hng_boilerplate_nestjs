# Boilerplate Documentation


API DESIGN LINK: [https://app.swaggerhub.com/apis/IGWEWISDOM20001_1/api-documentation/1.0.0](https://igwewisdomjaminel.github.io/SwaggerApi2/)

DATABASE DESIGN LINK: https://dbdiagram.io/d/Hng_stage3-669165369939893daecaa02a


## Overview

This boilerplate provides a robust and scalable foundation for building a comprehensive system with a wide range of features. It is structured to ensure that your system, codebase remains modular, maintainable, and easy to extend or modify.
This documentation provides instructions on how to keep your code decoupled, coding standards to follow, database design, API design and includes a license file.


## Project Structure

The project is structured in a way to separate concerns and maintain modularity. Here is an overview of the directory structure:


## /project-root

```

├── src
│  ├── controllers
     |--- v1
│  ├── database
│  ├── routes
     |--- v1
│  ├── services
│  ├── utils
│  ├── middlewares
│  └── server.ts
├── app.ts 
├── .env
├── .package.json
├── .gitignore
```



## controllers/v1:

- Purpose: Contains the controller logic for version 1 of your API. Controllers handle incoming requests, process them (often using services), and return responses to the client.
- Usage: Each controller typically maps to a specific route and contains methods for handling different HTTP methods (GET, POST, PUT, DELETE). For example, a UserController might have methods like getUser, createUser, updateUser, and deleteUser.



## database:

- Purpose: Manages the database connection and any database-related configurations.
- Usage: This directory might include ORM (Object-Relational Mapping) setup, database models or schemas, and migration scripts. It ensures that your application can communicate with the database efficiently.


## routes/v1:

- Purpose: Defines the routing logic for version 1 of your API. Routes determine which controller methods should be called based on the incoming request's URL and HTTP method.
- Usage: Each route file typically maps URL paths to controller methods. For example, a userRoutes.js file might map /users to UserController methods.

## services:

- Purpose: Contains the business logic of your application. Services are responsible for handling the core functionality, processing data, and interacting with the database.
- Usage: Each service typically corresponds to a specific domain or feature. For example, a UserService might handle user-related operations such as creating a user, updating user information, or fetching user data.

## utils:

- Purpose: Contains utility functions and helpers that are used throughout the application.
- Usage: These might include functions for data validation, formatting, logging, or other common tasks that can be reused across different parts of the application.

## middlewares:

- Purpose: Contains middleware functions that process requests before they reach the controller.
- Usage: Middleware can be used for various purposes such as authentication, logging, error handling, and request validation. For example, an authMiddleware.js file might check if a user is authenticated before allowing them to access certain routes.

## server.ts:

- Purpose: The entry point for your server. This file initializes the server, sets up middleware, and starts listening for incoming requests.
- Usage: This file will typically import the app configuration from app.ts, set up any necessary middleware, define the base routes, and start the server.

## app.ts:

- Purpose: Configures the main application setup.
- Usage: This file might initialize your Express application, apply global middleware, and configure other application-wide settings.



# Coding Standards



## JavaScript/TypeScript Standards
- Style Guide: Follow Airbnb JavaScript Style Guide
- Linting: Use ESLint with Airbnb configuration.
- Formatting: Use Prettier for consistent code formatting.

## Naming Conventions

- Variables: Use camelCase for variables and functions.
- Classes: Use PascalCase for class names.
- Constants: Use UPPER_SNAKE_CASE for constants.

## Best Practices

- Single Responsibility Principle: Ensure each module or function has one responsibility.
- DRY (Don't Repeat Yourself): Avoid code duplication by abstracting common logic.


# Database Design Documentation

To view the database design as image, follow this link:

DATABASE DESIGN LINK: [https://dbdiagram.io/d/Hng_stage3-669165369939893daecaa02a

](https://dbdiagram.io/d/Hng_stage3-669165369939893daecaa02a)



## Overview

This documentation outlines the structure and relationships of the database entities for managing users, organizations, authentication, messaging, payments, settings, activities, and more. This database is designed to support a comprehensive system with robust features.


## Entities and Relationships

## Users

Description: Stores information about users.
Fields:

- id: Primary key, auto-increment.
- userId: Unique identifier for the user.
- first_name: First name of the user.
- last_name: Last name of the user.
- username: Username of the user, not null.
- email: Email address of the user, unique, not null.
- password: Password of the user, not null.
- gender: Gender of the user.
- nationality: Nationality of the user.
- state: State of residence of the user.
- address: Address of the user.
- role: Role of the user, not null.
- createdAt: Timestamp when the user was created, defaults to current timestamp.
- updatedAt: Timestamp when the user was last updated, defaults to current timestamp.
  

## Organizations

Description: Stores information about organizations.
Fields:

- id: Primary key, auto-increment.
- orgId: Unique identifier for the organization.
- name: Name of the organization, not null.
- description: Description of the organization.
- createdAt: Timestamp when the organization was created, defaults to current timestamp.
- updatedAt: Timestamp when the organization was last updated, defaults to current timestamp.
   

## UserOrganizations

Description: Maps users to organizations.
Fields:

- user_id: Foreign key referencing Users.id, not null.
- organization_id: Foreign key referencing Organizations.id, not null.  

## Tokens

Description: Stores accessToken and refreshTokens for users.
Fields:

- id: Primary key, auto-increment.
- user_id: Foreign key referencing Users.id, not null.
- accessToken :Used to access protected resources.
- refreshToken: This is used to generate an accessToken after a previous one is expired.
- createdAt: Timestamp when the token was created, defaults to current timestamp.
- expiresAt: Expiry timestamp for the token, not null.


## Messages

Description: Stores messages sent to users.
Fields:

- id: Primary key, auto-increment.
- user_id: Foreign key referencing Users.id, not null.
- subject: Subject of the message.
- body: Body of the message.
- status: Status of the message.
- createdAt: Timestamp when the message was created, defaults to current timestamp.
- updatedAt: Timestamp when the message was last updated, defaults to current timestamp.


## Templates

Description: Stores various templates.
Fields:

- id: Primary key, auto-increment.
- name: Name of the template, not null.
- content: Content of the template, not null.
- type: Type of the template, not null.
- createdAt: Timestamp when the template was created, defaults to current timestamp.
- updatedAt: Timestamp when the template was last updated, defaults to current timestamp.



## Payments

Description: Stores payment transactions.
Fields:

- id: Primary key, auto-increment.
- user_id: Foreign key referencing Users.id, not null.
- amount: Amount of the payment, not null.
- currency: Currency of the payment, not null.
- transaction_ref: Transaction reference, not null.
- payment_method: Payment method used, not null.
- payment_gateway_tx_ref: Payment gateway transaction reference.
- status: Status of the payment, not null.
- createdAt: Timestamp when the payment was created, defaults to current timestamp.
- updatedAt: Timestamp when the payment was last updated, defaults to current timestamp.


## Settings

Description: Stores user settings.
Fields:

- id: Primary key, auto-increment.
- user_id: Foreign key referencing Users.id, not null.
- setting_type: Type of setting, (general settings, profile settings...)
- key: Setting key, not null.
- value: Setting value, not null.
- createdAt: Timestamp when the setting was created, defaults to current timestamp.
- updatedAt: Timestamp when the setting was last updated, defaults to current timestamp.


## Pages

Description: Stores various static pages content.
Fields:

- id: Primary key, auto-increment.
- title: Title of the page, not null.
- content: Content of the page, not null.
- type: Type of the page, not null.
- createdAt: Timestamp when the page was created, defaults to current timestamp.
- updatedAt: Timestamp when the page was last updated, defaults to current timestamp.


## Activities

Description: Logs user activities.
Fields:

- id: Primary key, auto-increment.
- user_id: Foreign key referencing Users.id, not null.
- action: Description of the action performed, not null.
- createdAt: Timestamp when the activity was created, defaults to current timestamp.


## Invites

Description: Stores invitation information.
Fields:

- id: Primary key, auto-increment.
- inviter_id: Foreign key referencing Users.id, not null.
- invitee_email: Email address of the invitee, not null.
- token: Invitation token, not null.
- status: Status of the invitation, not null.
- createdAt: Timestamp when the invitation was created, defaults to current timestamp.
- updatedAt: Timestamp when the invitation was last updated, defaults to current timestamp.


## Notifications

Description: Stores user notifications.
Fields:

- id: Primary key, auto-increment.
- user_id: Foreign key referencing Users.id, not null.
- message: Notification message, not null.
- read: Boolean indicating if the notification is read, defaults to false.
- createdAt: Timestamp when the notification was created, defaults to current timestamp.


## Blogs

Description: Stores blog posts.
Fields:

- id: Primary key, auto-increment.
- title: Title of the blog post, not null.
- content: Content of the blog post, not null.
- author_id: Foreign key referencing Users.id, not null.
- createdAt: Timestamp when the blog post was created, defaults to current timestamp.
- updatedAt: Timestamp when the blog post was last updated, defaults to current timestamp.


## Charts

Description: Stores chart data.
Fields:

- id: Primary key, auto-increment.
- user_id: Foreign key referencing Users.id, not null.
- data: Chart data in JSON format, not null.
- type: Type of chart, not null.
- createdAt: Timestamp when the chart was created, defaults to current timestamp.
- updatedAt: Timestamp when the chart was last updated, defaults to current timestamp.


## Metadata

Description: Stores user metadata.
Fields:

- id: Primary key, auto-increment.
- user_id: Foreign key referencing Users.id, not null.
- data: Metadata in JSON format, not null.
- createdAt: Timestamp when the metadata was created, defaults to current timestamp.


## Languages

Description: Stores supported languages.
Fields:

- id: Primary key, auto-increment.
- code: Language code, not null.
- name: Language name, not null.



## Regions

Description: Stores supported regions.
Fields:

- id: Primary key, auto-increment.
- code: Region code, not null.
- name: Region name, not null.



## EmailTemplates

Description: Stores email templates.
Fields:

- id: Primary key, auto-increment.
- name: Name of the email template, not null.
- subject: Subject of the email template, not null.
- body: Body of the email template, not null.
- createdAt: Timestamp when the email template was created, defaults to current timestamp.
- updatedAt: Timestamp when the email template was last updated, defaults to current timestamp.


## Relationships

- User and Organizations: Many-to-Many relationship via UserOrganizations.
- User and RefreshTokens: One-to-Many relationship.
- User and Messages: One-to-Many relationship.
- User and Payments: One-to-Many relationship.
- User and Settings: One-to-Many relationship.
- User and Activities: One-to-Many relationship.
- User and Notifications: One-to-Many relationship.
- User and Blogs: One-to-Many relationship.
- User and Charts: One-to-Many relationship.
- User and Metadata: One-to-Many relationship.
- User and Invites: One-to-Many relationship (inviter).


## Conclusion

Each table is designed to store specific information with clearly defined relationships to maintain data integrity and support the various features of the application. This database design covers a wide range of functionalities, ensuring a scalable and robust system.


# API Documentation

API DESIGN LINK: [https://app.swaggerhub.com/apis/IGWEWISDOM20001_1/api-documentation/1.0.0](https://igwewisdomjaminel.github.io/SwaggerApi2/)

Endpoints


##### User Management

- POST /api/register: Register a new user
- POST /api/login: User login
- POST /api/logout: User logout
- GET /api/auth/me: Get authenticated user details
- GET /api/users: Get all users
- POST /api/users: Create a new user
- GET /api/users/{id}: Get user details
- PUT /api/users/{id}: Update user details
- DELETE /api/users/{id}: Delete a user


#### Password Management

- POST /api/password/forgot: Send password reset link
- POST /api/password/reset: Reset password
- POST /api/password/change: Change password


#### Authentication

- POST /api/magic-link: Send magic link for login
- POST /api/auth/social: Social login (Google, Facebook, etc.)


#### Email Templates

- GET /api/email/templates: Get all email templates
- POST /api/email/templates: Create a new email template
- PUT /api/email/templates/{id}: Update an email template
- DELETE /api/email/templates/{id}: Delete an email template


#### Payments

- POST /api/payments/stripe: Create a Stripe payment
- POST /api/payments/flutterwave: Create a Flutterwave payment
- POST /api/payments/lemonsqueezy: Create a LemonSqueezy payment
- POST /api/payments/initialize: Initialize a payment
- GET /api/payments/verify: Verify a payment
- GET /api/payments/history: Get payment history


#### Organizations

- GET /api/organisations: Get all organisations
- POST /api/organisations: Create a new organisation
- GET /api/organisations/{id}: Get organisation details
- PUT /api/organisations/{id}: Update organisation details DELETE /api/organisations/{id}: Delete an organisation


#### Super Admin

- GET /api/superadmin/users: Get all users (superadmin view)
- GET /api/superadmin/organisations: Get all organisations (superadmin view)
- GET /api/superadmin/payments: Get all payments (superadmin view)
- GET /api/superadmin/activity-log: Get activity log


#### Miscellaneous

- POST /api/invite: Generate an invite link
- POST /api/notifications/push: Send a push notification


## Example Requests and Responses


## Register a new user

#### Request:

#### POST /api/register 

```
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
```

#### Response:


#### json
#### 200 OK

```
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
```


## Security

This API uses JWT (JSON Web Tokens) for authentication. All authenticated endpoints require a valid JWT token to be included in the Authorization header of the request.


# License

Include a license file in the root of your project. For example, to use the MIT License, create a LICENSE file with the following content:

## MIT License

```
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
```
