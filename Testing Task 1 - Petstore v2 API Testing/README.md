# Testing Task 1 - Petstore v2 API Testing

## Setup:

- Download the latest Postman app from the official [Postman website](https://www.postman.com/downloads/)
- Download the postman collection, environment, and globals, and import them to Postman
- Navigate to the collection and select the UAT environment
- Run the collection

![image](https://github.com/user-attachments/assets/ab7134d9-403c-4b0b-8a30-07740655f6f7)

## Observations and Issues Encountered:

- The Swagger Petstore API v2 server doesn't behave as expected and some scenarios from the documentation cannot be replicated
- The Swagger Petstore API documentation link provided is for the v2 of the API Petsore server.
  - Swagger now has the v3 for the API server which behaves more accurately to what's in the v3 Swagger API documentation
- I created my Postman tests according to the specification in Swagger, thus, some tests in the Postman collection are expected to fail, catching bugs to the app instead of the tests
