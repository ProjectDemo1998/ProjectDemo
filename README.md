# Customer RESTful API

This project contains a simple RESTful API for managing customer entities. It supports CRUD (Create, Read, Update, Delete) operations using HTTP verbs (POST, GET, PUT, DELETE).

## Endpoints

### GET /api/customer
Retrieve a list of all customers.

### GET /api/customer/{id}
Retrieve details of a specific customer by ID.

### POST /api/customer
Create a new customer.

### PUT /api/customer/{id}
Update details of an existing customer by ID.

### DELETE /api/customer/{id}
Delete an existing customer by ID.

## Usage

1. Clone this repository.
2. Build and run the project.
3. Use a tool like Postman or cURL to interact with the API endpoints.

## Error Handling

The API returns appropriate HTTP status codes for different scenarios:

- 200 OK: Successful GET request.
- 201 Created: Successful POST request.
- 204 No Content: Successful PUT or DELETE request.
- 400 Bad Request: Malformed request or missing parameters.
- 404 Not Found: Resource not found
