# Demo Script

## Overview

This document contains representative customer journeys used to demonstrate the Retail CX Voice Agent.

The scenarios cover both successful customer interactions and exception handling workflows.

---

# Scenario 1: Order Status (Happy Path)

## Objective

Demonstrate order tracking functionality.

### Customer

Where is my order?

### System Flow

1. Customer authenticates successfully.
2. Customer order list is retrieved.
3. Customer selects an order.
4. Customer selects **Order Status** from the service menu.
5. OrderLookupTool is invoked.
6. Order status information is retrieved.
7. Agent presents current status and delivery details.

### Expected Outcome

Customer receives accurate order tracking information.

---

# Scenario 2: Order Modification (Happy Path)

## Objective

Demonstrate order modification workflow.

### Customer

I want to change my delivery address.

### System Flow

1. Customer authenticates successfully.
2. Customer selects an order.
3. Customer selects **Order Modification**.
4. Agent captures updated address.
5. OrderModificationTool is invoked.
6. Agent presents proposed modification.
7. Customer confirms request.
8. Modification is executed.
9. Confirmation is presented.

### Expected Outcome

Order details are updated successfully.

---

# Scenario 3: Return Request (Happy Path)

## Objective

Demonstrate return workflow.

### Customer

I would like to return this item.

### System Flow

1. Customer authenticates successfully.
2. Customer selects an order.
3. Customer selects **Return / Exchange**.
4. ReturnEligibilityTool validates eligibility.
5. Customer selects Return.
6. ReturnTool is invoked.
7. Available pickup slots are retrieved.
8. Customer selects a pickup slot.
9. Return request is created.
10. Confirmation is presented.

### Expected Outcome

Return request is initiated successfully.

---

# Scenario 4: Exchange Request with Recommendation

## Objective

Demonstrate exchange workflow and product recommendation capability.

### Customer

I need a different size.

### System Flow

1. Customer authenticates successfully.
2. Customer selects an order.
3. Customer selects **Return / Exchange**.
4. ReturnEligibilityTool validates eligibility.
5. Customer selects Exchange.
6. ExchangeTool is invoked.
7. RecommendationTool provides alternative products or sizes.
8. Customer selects preferred option.
9. Pickup slot is scheduled.
10. Exchange confirmation is presented.

### Expected Outcome

Exchange request is successfully created.

---

# Scenario 5: Refund Status (Happy Path)

## Objective

Demonstrate refund tracking functionality.

### Customer

What is the status of my refund?

### System Flow

1. Customer authenticates successfully.
2. Customer selects an order.
3. Customer selects **Refund Status**.
4. RefundTrackerTool is invoked.
5. Refund information is retrieved.
6. Agent presents refund amount and processing status.

### Expected Outcome

Customer receives refund status information.

---

# Scenario 6: Order Cancellation (Happy Path)

## Objective

Demonstrate order cancellation workflow.

### Customer

I want to cancel my order.

### System Flow

1. Customer authenticates successfully.
2. Customer selects an order.
3. Customer selects **Order Cancellation**.
4. Cancellation eligibility is validated.
5. Agent requests confirmation.
6. Customer confirms cancellation.
7. CancellationTool is invoked.
8. Cancellation confirmation is presented.

### Expected Outcome

Eligible order is cancelled successfully.

---

# Scenario 7: Authentication Failure (Exception Path)

## Objective

Demonstrate security controls.

### Customer

Provides incorrect credentials repeatedly.

### System Flow

1. Customer enters invalid PIN.
2. Authentication fails.
3. Retry counter increments.
4. Customer exceeds maximum retry limit.
5. Conversation is escalated.

### Expected Outcome

Unauthorized access is prevented.

---

# Scenario 8: Return Not Eligible (Exception Path)

## Objective

Demonstrate business rule enforcement.

### Customer

I want to return this item.

### System Flow

1. Customer authenticates successfully.
2. Customer selects an order.
3. ReturnEligibilityTool is invoked.
4. Order is determined to be ineligible.
5. Agent explains reason.
6. Customer is returned to the service menu.

### Expected Outcome

Ineligible return requests are blocked.

---

# Scenario 9: API Failure (Exception Path)

## Objective

Demonstrate failure handling and escalation.

### Customer

Track my order.

### System Flow

1. Customer authenticates successfully.
2. Customer selects Order Status.
3. OrderLookupTool is invoked.
4. Backend service fails.
5. Agent informs customer.
6. Escalation option is provided.

### Expected Outcome

Failure is handled gracefully without generating inaccurate information.

---

# Demo Coverage Summary

| Scenario | Journey Type |
|----------|----------|
| Order Status | Happy Path |
| Order Modification | Happy Path |
| Return Request | Happy Path |
| Exchange Request | Happy Path |
| Refund Status | Happy Path |
| Order Cancellation | Happy Path |
| Authentication Failure | Exception Path |
| Return Not Eligible | Exception Path |
| API Failure | Exception Path |

---

# Success Criteria

The demo is considered successful when:

- Authentication is enforced.
- Customer context is maintained across interactions.
- Tools are invoked correctly.
- Business rules are enforced.
- Exception scenarios are handled safely.
- Escalation paths function as expected.
