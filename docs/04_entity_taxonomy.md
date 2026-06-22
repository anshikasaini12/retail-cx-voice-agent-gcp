# Entity Taxonomy

## Entity Overview

| Entity | Type | Description | Example |
|----------|----------|----------|----------|
| customer_id | String | Unique customer identifier | C001 |
| phone_number | String | Customer phone number used for authentication | 9876543210 |
| pin | String | Customer authentication PIN | 1234 |
| authentication_status | Boolean | Authentication result | True |
| selected_order_id | String | Order selected by customer | O101 |
| order_status | String | Current order status | Shipped |
| delivery_date | Date | Expected delivery date | 2026-06-22 |
| address | String | Delivery address | Chandigarh, India |
| contact_number | String | Updated receiver contact number | 9876543211 |
| return_reason | String | Reason for return request | Wrong Size |
| exchange_preference | String | Exchange preference | Larger Size |
| pickup_slot | String | Scheduled pickup slot | 10 AM - 12 PM |
| refund_status | String | Refund processing status | Processed |
| refund_amount | Number | Refund amount | 1500 |
| product_category | String | Product category for recommendations | Apparel |
| customer_preferences | String | Customer shopping preferences | Casual Wear |
| service_type | String | Active customer journey | Return Request |

---

# Authentication Entities

## customer_id

### Description
Unique identifier associated with a customer account.

### Used In
- Authentication Flow
- Customer Profile Retrieval
- Order Retrieval

---

## phone_number

### Description
Customer phone number used during authentication.

### Used In
- Authentication Flow
- Customer Lookup

---

## pin

### Description
Authentication PIN provided by the customer.

### Used In
- Authentication Verification

---

## authentication_status

### Description
Stores authentication result for the current session.

### Possible Values
- True
- False

### Used In
- Session Management
- Access Control

---

# Order Management Entities

## selected_order_id

### Description
Stores the order selected by the customer after authentication.

### Example
O101

### Used In
- Order Status
- Order Modification
- Return / Exchange
- Refund Status
- Order Cancellation

---

## order_status

### Description
Current lifecycle state of the order.

### Example Values
- Pending
- Shipped
- Delivered
- Cancelled

---

## delivery_date

### Description
Expected delivery date for the selected order.

### Example
2026-06-22

---

## address

### Description
Delivery address associated with an order.

### Used In
- Order Modification

---

## contact_number

### Description
Receiver contact number for delivery communication.

### Used In
- Order Modification

---

# Return / Exchange Entities

## return_reason

### Description
Reason provided by the customer for returning an item.

### Example Values
- Wrong Size
- Damaged Product
- Incorrect Item
- Quality Issue

---

## exchange_preference

### Description
Customer preference for exchange.

### Example Values
- Different Size
- Different Color
- Alternative Product

---

## pickup_slot

### Description
Preferred pickup schedule selected by the customer.

### Example
10 AM - 12 PM

---

# Refund Entities

## refund_status

### Description
Current status of refund processing.

### Example Values
- Initiated
- Processing
- Processed
- Failed

---

## refund_amount

### Description
Amount associated with the refund request.

### Example
1500

---

# Recommendation Entities

## product_category

### Description
Product category used for recommendation generation.

### Example Values
- Apparel
- Footwear
- Accessories

---

## customer_preferences

### Description
Customer purchase preferences used for personalization.

### Example Values
- Casual Wear
- Formal Wear
- Sportswear

---

# Session Context Entity

## service_type

### Description
Stores the active customer journey being executed.

### Example Values
- Order Status
- Order Modification
- Return Request
- Exchange Request
- Refund Status
- Order Cancellation

### Purpose
Allows conversational context to persist across the session.
