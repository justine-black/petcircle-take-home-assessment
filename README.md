# Pet Circle Take Home Assessment

As part of my application to the Senior QA & Test Engineer role for Pet Circle, I'm asked to take on two tasks - creating an API testing framework and creating a test plan.

## Testing Task 1: API Testing

### Implementation and Setup:

Navigate to [Testing Task 1 - Petstore v2 API Testing](/Testing%20Task%201%20-%20Petstore%20v2%20API%20Testing/) subdirectory to see instructions on how to setup the postman collection

### Requirements:

1. Setup: Access the Swagger Petstore API documentation https://petstore.swagger.io/
2. Scenario Creation: Using the documentation, devise test scenarios for each CRUD
   operation (Create, Read, Update, Delete) for the "Pets" resource
3. Create: Design scenarios to test the creation of pets in the Petstore. Consider
   various inputs and edge cases.
4. Read: Create scenarios to test retrieving pet details from the Petstore. Include
   scenarios for existing and non-existing pets.
5. Update: Design scenarios to test updating existing pet details in the Petstore. Include
   scenarios for updating different attributes.
6. Delete: Develop scenarios to test deleting pets from the Petstore. Consider
   scenarios for deleting existing and non-existing pets.

## Testing Task 2: Test Plan

A hypothetical new feature is being added to an e-commerce company's tech stack. Using
the brief below, please write a test plan for this new feature in whatever format you prefer.

### Implementation and Setup:

Navigate to [Testing Task 2 - Inventory Adjustment Test Plan](/Testing%20Task%202%20-%20Inventory%20Adjustment%20Test%20Plan/) subdirectory to see my **Test Plan** for this task

### Context:

A company is experiencing rapid growth and is outgrowing its current capacity to manage
inventory and order fulfilment in-house. To scale efficiently, the company has decided to
partner with multiple third-party logistics providers (3PLs) to handle warehousing and
shipping. Previously, the company has relied on its own first-party warehouses and systems
to manage these operations.

### Requirements:

The company has an existing in-house inventory management system used by customer
service agents to perform one-off inventory level adjustments. You are tasked with **creating
a test plan to test inventory adjustments**. Any changes to inventory will need to be
updated across all 3PL warehouses and the company's internal systems, and any changes
must be auditable (belonging to a customer service agent). Inventory adjustments can be
positive or negative integers. An inventory adjustment can affect one to many warehouses.
Communications between internal and external systems are made through REST APIs

### Considerations:

When writing your test plan be sure to consider the following:

- **Functional Testing**: What positive scenarios need to be tested? Also consider
  negative paths and edge cases.
- **Integration Testing**: The third-party logistics will use their own system. What
  integration testing and error handling need to be tested?
- **Performance Testing**: What performance, load or stress tests need to be carried
  out?
- **Regression Testing**: Are there specific areas to run regressions against?
