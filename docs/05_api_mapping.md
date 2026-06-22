# API Mapping

## Overview

This document defines the mapping between customer intents, conversational tools, backend APIs, input parameters, and expected outputs.

The objective is to maintain traceability between customer requests and backend business operations.

---

## API Mapping Matrix

| Intent | Tool | API | Input Parameters | Output |
|----------|----------|----------|----------|----------|
| Order Status | OrderLookupTool | checkOrderStatus() | order_id | Order details, delivery status |
| Order Modification | OrderModificationTool | modifyOrder() | order_id, address/contact/delivery_date | Updated order details |
| Return / Exchange | ReturnEligibilityTool | checkReturnEligibility() | order_id | Eligibility status |
| Return / Exchange | ReturnTool / ExchangeTool | initiateReturnExchange() | order_id, request_type | Return or exchange confirmation |
| Return / Exchange | SlotBookingTool | getDeliverySlots() | order_id | Available pickup slots |
| Refund Status | RefundTrackerTool | getRefundStatus() | order_id | Refund status, refund amount |
| Upsell / Cross-Sell | RecommendationTool | getProductRecommendations() | customer_id, order_history | Product recommendations |
| Order Cancellation | CancellationTool | cancelOrder() | order_id | Cancellation confirmation |

---

# 1. checkOrderStatus()

## Purpose

Retrieve order details and current delivery status.

## Invoked By

- OrderLookupTool

## Input

| Parameter | Type | Description |
|----------|----------|----------|
| order_id | String | Selected customer order |

## Output

| Field | Description |
|----------|----------|
| orderId | Order identifier |
| status | Current order status |
| deliveryDate | Expected delivery date |
| items | Products included in order |

## Sample Response

```json
{
  "orderId": "O101",
  "status": "Shipped",
  "deliveryDate": "2026-06-22",
  "items": ["T-shirt", "Jeans"]
}
```

---

# 2. modifyOrder()

## Purpose

Update eligible order details.

## Invoked By

- OrderModificationTool

## Input

| Parameter | Type | Description |
|----------|----------|----------|
| order_id | String | Selected customer order |
| address | String | Updated delivery address |
| contact_number | String | Updated contact number |
| delivery_date | Date | Updated delivery date |

## Output

| Field | Description |
|----------|----------|
| orderId | Order identifier |
| status | Update status |
| updatedField | Modified value |

## Sample Response

```json
{
  "orderId": "O101",
  "status": "Updated",
  "newAddress": "New Delhi"
}
```

---

# 3. checkReturnEligibility()

## Purpose

Determine whether an order is eligible for return or exchange.

## Invoked By

- ReturnEligibilityTool

## Input

| Parameter | Type | Description |
|----------|----------|----------|
| order_id | String | Selected customer order |

## Output

| Field | Description |
|----------|----------|
| eligible | Return eligibility status |
| reason | Eligibility explanation |

---

# 4. initiateReturnExchange()

## Purpose

Initiate return or exchange workflow.

## Invoked By

- ReturnTool
- ExchangeTool

## Input

| Parameter | Type | Description |
|----------|----------|----------|
| order_id | String | Selected customer order |
| request_type | String | Return or Exchange |

## Output

| Field | Description |
|----------|----------|
| orderId | Order identifier |
| status | Request status |
| pickupDate | Scheduled pickup date |

## Sample Response

```json
{
  "orderId": "O101",
  "status": "Return Initiated",
  "pickupDate": "2026-06-25"
}
```

---

# 5. getDeliverySlots()

## Purpose

Retrieve available pickup or rescheduling slots.

## Invoked By

- SlotBookingTool

## Input

| Parameter | Type | Description |
|----------|----------|----------|
| order_id | String | Selected customer order |

## Output

| Field | Description |
|----------|----------|
| slot_id | Slot identifier |
| slot_time | Available slot |

---

# 6. getRefundStatus()

## Purpose

Retrieve refund details and processing status.

## Invoked By

- RefundTrackerTool

## Input

| Parameter | Type | Description |
|----------|----------|----------|
| order_id | String | Selected customer order |

## Output

| Field | Description |
|----------|----------|
| refundStatus | Current refund status |
| amount | Refund amount |

## Sample Response

```json
{
  "orderId": "O101",
  "refundStatus": "Processed",
  "amount": 1500
}
```

---

# 7. getProductRecommendations()

## Purpose

Generate personalized product recommendations.

## Invoked By

- RecommendationTool

## Input

| Parameter | Type | Description |
|----------|----------|----------|
| customer_id | String | Customer identifier |
| order_history | String | Previous purchases |

## Output

| Field | Description |
|----------|----------|
| product_name | Recommended product |
| category | Product category |
| confidence_score | Recommendation relevance |

---

# 8. cancelOrder()

## Purpose

Cancel eligible customer orders.

## Invoked By

- CancellationTool

## Input

| Parameter | Type | Description |
|----------|----------|----------|
| order_id | String | Selected customer order |

## Output

| Field | Description |
|----------|----------|
| orderId | Order identifier |
| status | Cancellation status |
| refundEligibility | Refund eligibility information |

## Sample Response

```json
{
  "orderId": "O101",
  "status": "Cancelled"
}
```
