# API Testing with Postman & Newman

This project demonstrates automated REST API testing using Postman and Newman. The collection includes comprehensive tests for various API endpoints, ensuring functionality and reliability.

## Features

- Automated tests for GET, POST, PUT, DELETE requests
- Structured test collection for different API endpoints
- Configurable environment settings
- Pre-request scripts for dynamic data generation
- Test scripts for result validation and response verification

## API Documentation

For detailed API documentation, refer to: [Postman API Documentation](https://documenter.getpostman.com/view/19885870/2sAYX5M3Gi)

## Technologies Used

- Postman
- Newman

## Prerequisites

Ensure the following dependencies are installed:

- Node.js
- Newman
- Newman HTML Report Library

## Installation Guide

### Install Postman

Download and install Postman from the official website.

### Clone the Repository

```sh
git clone https://github.com/your-repository/API_Testing_with_Postman_Newman.git
cd API_Testing_with_Postman_Newman
```

### Import Postman Collection

1. Open Postman.
2. Click on **Import**.
3. Select and import the collection file from the repository.

### Import Postman Environment

1. In Postman, click on the **gear icon** (top right corner).
2. Select **Import** and choose the environment file.

### Install Newman and Report Library

```sh
npm install -g newman
npm install -g newman-reporter-htmlextra
```

## Running Tests

### Select Environment

1. In Postman, choose the correct environment from the dropdown.

### Execute Test Collection

1. Navigate to **Collections**.
2. Select the imported test collection.
3. Click on **Runner**.
4. Select the environment and run the tests.

### View Results

- Test results will be displayed in the **Runner** tab.
- Detailed request and response validation logs are available.

## Test Scenarios

### 1. Create a New Booking

**Endpoint:** `POST /booking`

#### Pre-request Script:

```javascript
var firstName = pm.variables.replaceIn("{{$randomFirstName}}");
pm.environment.set("firstName", firstName);

var lastName = pm.variables.replaceIn("{{$randomLastName}}");
pm.environment.set("lastName", lastName);

var totalPrice = pm.variables.replaceIn("{{$randomInt}}");
pm.environment.set("totalPrice", totalPrice);

var depositPaid = pm.variables.replaceIn("{{$randomBoolean}}");
pm.environment.set("depositPaid", depositPaid);

const moment = require('moment');
const today = moment();
var checkin = today.add(1, 'd').format("YYYY-MM-DD");
pm.environment.set("checkin", checkin);
var checkout = today.add(1, 'd').format("YYYY-MM-DD");
pm.environment.set("checkout", checkout);

const additionalNeeds = ["Breakfast", "Lunch", "Dinner", "Wifi"];
pm.variables.set("additionalNeed", additionalNeeds[Math.floor(Math.random()*additionalNeeds.length)]);
```

#### Request Body:

```json
{
   "firstname": "{{firstName}}",
   "lastname": "{{lastName}}",
   "totalprice": {{totalPrice}},
   "depositpaid": {{depositPaid}},
   "bookingdates": {
       "checkin": "{{checkin}}",
       "checkout": "{{checkout}}"
   },
   "additionalneeds": "{{additionalNeed}}"
}
```

### 2. Retrieve Booking Details

**Endpoint:** `GET /booking/{id}`

### 3. Generate Authentication Token

**Endpoint:** `POST /auth`

#### Request Body:

```json
{
   "username": "admin",
   "password": "password123"
}
```

### 4. Update Booking Information

**Endpoint:** `PUT /booking/{id}`

#### Request Body:

```json
{
   "firstname": "{{updated_firstName}}",
   "lastname": "{{updated_lastName}}",
   "totalprice": {{updated_totalPrice}},
   "depositpaid": {{updated_depositPaid}},
   "bookingdates": {
       "checkin": "{{updated_checkin}}",
       "checkout": "{{updated_checkout}}"
   },
   "additionalneeds": "{{updated_additionalNeed}}"
}
```

### 5. Delete a Booking Record

**Endpoint:** `DELETE /booking/{id}`

## Running Tests with Newman

### Command-Line Execution

```sh
newman run API_Testing_CRUD.postman_collection.json -e API_Testing_CRUD.postman_environment.json
```

### Generate HTML Report

```sh
newman run API_Testing_CRUD.postman_collection.json -e API_Testing_CRUD.postman_environment.json -r cli,htmlextra
```

## Uploading to GitHub

### Initialize Git and Push the Project

```sh
git init
git add .
git commit -m "Initial commit - API Testing with Postman & Newman"
git branch -M main
git remote add origin https://github.com/your-github-username/API_Testing_with_Postman_Newman.git
git push -u origin main
```

---

This guide provides a structured approach to API testing using Postman and Newman, ensuring streamlined validation of RESTful services.

