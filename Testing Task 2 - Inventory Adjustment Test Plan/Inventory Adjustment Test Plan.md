# Test Plan - Inventory Adjustment Feature

## Introduction

This test plan outlines the testing strategy for the new **inventory adjustment** feature to be developed and integrated with the new third-party logistics (3PL) partners. The feature will allow customer service agents to adjust inventory levels, which will need to be synchronized across multiple 3PL providers and the company's internal systems. The objective is to ensure that all inventory adjustments are accurately recorded, synchronized, auditable, and robust enough to handle integration with external 3PL systems.

### Objectives

- Ensure that inventory adjustments are processed correctly.
- Verify that adjustments are synchronized across all the 3PL systems and the company's internal systems.
- Test error handling and integrations with external systems.
- Verify that the system scales and performs well under stress or heavy loads.
- Ensure that the feature does not negatively impact existing functionalities.

### Scope

- Testing of the functionality for adjusting inventory levels (positive and negative adjustment).
- Testing the communication between internal systems and third-party logistics providers via REST APIs.
- User interface testing for the application used by the customer service agents
- Auditing and logging of adjustments performed by customer service agents.
- Performance testing under expected load and stress conditions.

### Out of Scope

- End-to-end testing of third-party logistics providers’ systems.

## Test Strategy

### 1. Functional Testing

**Positive Scenarios**:

- **Single Warehouse Positive Adjustment**: Adjust inventory levels by a positive integer (increase inventory) in a single warehouse and verify that the update is reflected in both the internal system and the respective 3PL warehouse.

- **Single Warehouse Negative Adjustment**: Adjust inventory levels by a negative integer (decrease inventory) in a single warehouse and verify that the update is reflected in both the internal system and the respective 3PL warehouse.

- **Multiple Warehouse Positive Adjustment**: Adjust inventory levels by a positive integer (increase inventory) affecting multiple warehouses and ensure synchronization across all relevant 3PL systems and the internal system.

- **Multiple Warehouse Negative Adjustment**: Adjust inventory levels by a negative integer (decrease inventory) affecting multiple warehouses and ensure synchronization across all relevant 3PL systems and the internal system.

- **Audit Log Verification**: Ensure that each inventory adjustment action is logged, showing the customer service agent's ID, inventory changes, and timestamps.

- **Boundary Testing**: Ensure inventory adjustments can be made on the lowest and highest valid integer values (e.g. 0 and maximum allowed inventory levels).

- **Multi-Agent Adjustments**: Simulate multiple agents making concurrent inventory adjustments and verify that the system correctly handles race conditions.

**Negative Scenarios**:

- **Invalid Inventory Adjustment Value**: Attempt to adjust inventory by non-integer or invalid values (e.g., text or decimal numbers) and verify that the system rejects these inputs.

- **Non-Authorized User**: Ensure that non-authorized users (e.g., agents without permissions) cannot perform any inventory adjustments.

- **Invalid Warehouse**: Attempt to adjust inventory for a non-existent or invalid warehouse and verify that the system returns an error message.

**Edge Cases**:

- **Zero Inventory Adjustment**: Test adjusting inventory by 0 (no change) and verify that no updates are made.

- **Adjustment at Warehouse Capacity Limits**: Adjust inventory to test the system’s handling when warehouses are near their capacity limits (e.g., full warehouses).

- **Negative Inventory**: Ensure that the system handles negative inventory correctly (i.e., understock or depletion) and maintains accurate records.

- **Adjustment Exceeding Available Capacity**: Perform positive inventory adjustment by an amount greater than the available capacity in a warehouse and ensure the system raises an appropriate error message.

- **Adjustment Resulting to Negative Inventory**: Perform negative inventory by an amount less than the current inventory and ensure that the system handles negative inventory correctly (i.e., backorders, pre-sales) and maintains accurate records.

### 2. Integration Testing

**REST API Communication Testing**:

- Test API calls to ensure proper communication between internal systems and 3PL systems. This includes ensuring that POST, PUT, and DELETE requests are correctly formatted and received by the 3PL’s API based on the API documentations.

- Verify that the inventory adjustment data (positive or negative) is correctly transmitted to the respective warehouses.

- Ensure that responses from the 3PL APIs are correctly parsed and handled, including successful status codes and error codes (e.g., 404 for invalid warehouse or 500 for server issues).

**Error Handling**:

- Test the handling of failure scenarios like network outages, 3PL API downtime, or 3PL systems rejecting inventory updates (e.g., invalid warehouse codes or unavailable inventory slots).

- Verify that the system appropriately retries failed requests or logs errors for review.

  - Ensure that retries would not result to duplicate adjustments

- Ensure that in case of failure, descriptive error messages that clearly explains the nature of the error are returned to the user (customer service agent).

**Data Synchronization**:

- Verify that all inventory adjustments made in the internal system are correctly reflected in all 3PL warehouses.

- Ensure that the changes are synchronized both ways: If a change is made in the 3PL system, it should be propagated back to the internal system.

### 3. Regression Testing

**API Endpoint Validation**:

- Ensure that no existing API endpoints are broken by the new inventory adjustment feature and that backward compatibility is maintained in case we have to do a rollback to the existing in-house warehousing system

**Data Integrity Tests**:

- Ensure that other features, such as order processing and stock tracking, are not impacted by changes in inventory levels.

### 4. Smoke Testing

**Critical Functionality Verification**:

- Verify that core functionalities, such as creating new orders or processing payments, continue to work properly after implementing the inventory adjustment feature.

- Ensure that any existing features related to order fulfillment, customer service, and inventory management are not broken by the new feature.

### 5. Performance Testing

**Load Testing**:

- Simulate multiple customer service agents making concurrent inventory adjustments to verify that the system handles a high volume of requests and that inventory synchronization remains accurate.

- Measure the system's response time for both single and bulk inventory adjustments (e.g., multiple warehouses in a single request if possible).

**Stress Testing**:

- Increase the load beyond the expected usage to determine how the system behaves under stress (e.g., more than 100 concurrent agents or excessive inventory adjustments).

- Identify system bottlenecks and failure points in the API communication or database handling during stress conditions.

**Scalability Testing**:

- Test how the system scales as the number of warehouses or 3PL partners increases. This will ensure that the system can scale horizontally without significant performance degradation.

### 6. Security Testing

- Ensure that the API endpoints can only be accessed by the 3PL partners with the API keys secured.

## Test Automation

- Develop automated test scripts for candidate test cases to be included in the regression suite.

- Execute regression suite automated test cases on every deployment to the test environments to efficiently ensure that all systems are still behaving as expected

## Test Environment

**DEV Environment**:

- The environment typically used by the developers to deploy and test their work-in-progress codes before pushing them to the test environments.

- QA Engineers may work in parallel with the developers on this environment to give early QA feedback to the code.

**UAT Environment**:

- The main testing environment used by the QA Engineers where functional testing (system, integration, regression, and user acceptance testing) will be performed, as it mirrors production setup closely in terms of data and functionality.

**PRE-PROD Environment**:

- The final testing environment before production release where non-functional testing (performance, load, and stress testing) and smoke testing will be performed, as it mirrors production setup closely in terms of data, configuration, allocated hardware resources, etc.

**PROD Environment**:

- The live production environment used by end users.

- Final deployment stage after all tests are passed.

## Test Deliverables

1. Test Plan Document (this document)

2. Test Cases covering all scenarios, including functional, integration, and performance tests.

3. Test Scripts for automated testing where applicable.

4. Test Data for all test cases (e.g., sample inventory levels, warehouse IDs, agent information).

5. Test Execution Logs documenting the results of each test.

6. Defect Reports detailing any identified defects or issues during testing.

## Test Schedule

- Test Planning: 1 week

- Test Case Development: 1 week

- Test Execution:

  - Functional Testing: 2 weeks

  - Integration Testing: 2 weeks

  - Regression Testing: 1 week

  - Performance Testing: 1 week

  - Security Testing: 1 week

- Defect Fixes and Retesting: 1 week

- Final Report and Sign-Off: 1 week

## Risks and Mitigation

| **Risk**                                                                           | **Mitigation**                                                                      |
| ---------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| Delays in integration with third-party logistics systems                           | Early coordination with 3PL providers and parallel testing on sandbox environments. |
| Unforeseen performance issues when handling large numbers of inventory adjustments | Regular load testing throughout development and performance tuning of APIs          |
| Incomplete or faulty logging and auditing                                          | Thorough testing of audit logs and agent tracking for all adjustment actions        |

---
