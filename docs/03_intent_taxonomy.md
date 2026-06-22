# Intent Taxonomy

## Intent Overview

| Intent | Tool(s) | API(s) | Primary Outcome |
|----------|----------|----------|----------|
| Order Status | OrderLookupTool | checkOrderStatus() | Retrieve order and delivery status |
| Order Modification | OrderModificationTool | modifyOrder() | Update eligible order details |
| Return / Exchange | ReturnEligibilityTool, ReturnTool, ExchangeTool, SlotBookingTool | checkReturnEligibility(), initiateReturnExchange(), getDeliverySlots() | Initiate return or exchange journey |
| Refund Status | RefundTrackerTool | getRefundStatus() | Retrieve refund information |
| Upsell / Cross-Sell | RecommendationTool | getProductRecommendations() | Recommend relevant products |
| Cancel Order | CancellationTool | cancelOrder() | Cancel eligible order |

---

# 1. Order Status

### Phrases

- Where is my order?
- Track my package
- What's the status of my order?
- Has my order been shipped?
- When will my order arrive?

### Entities

- selected_order_id

### Tool

- OrderLookupTool

### API

- checkOrderStatus()

### Expected Outcome

Customer receives current order status, delivery date, and shipment information.

---

# 2. Order Modification

### Phrases

- Change my delivery address.
- Update my contact number.
- Reschedule my delivery.
- Modify my order details.
- Change the receiver information.

### Entities

- selected_order_id
- address
- phone_number
- delivery_date

### Tool

- OrderModificationTool

### API

- modifyOrder()

### Expected Outcome

Eligible order details are successfully updated after customer confirmation.

---

# 3. Return / Exchange

### Phrases

- I want to return this item.
- I'd like to exchange my product.
- Start a return request.
- Replace this item with another size.
- Return my order.

### Entities

- selected_order_id
- return_reason
- exchange_preference
- pickup_slot

### Tools

- ReturnEligibilityTool
- ReturnTool
- ExchangeTool
- SlotBookingTool

### APIs

- checkReturnEligibility()
- initiateReturnExchange()
- getDeliverySlots()

### Expected Outcome

Return or exchange request is successfully initiated and pickup slot is scheduled.

---

# 4. Refund Status

### Phrases

- Where is my refund?
- Check my refund status.
- Has my refund been processed?
- When will I receive my refund?
- Refund update.

### Entities

- selected_order_id

### Tool

- RefundTrackerTool

### API

- getRefundStatus()

### Expected Outcome

Customer receives refund amount, refund status, and processing details.

---

# 5. Upsell / Cross-Sell

### Phrases

- Show me similar products.
- Recommend another product.
- What other options do you have?
- Suggest matching items.
- Recommend something similar.

### Entities

- selected_order_id
- product_category
- customer_preferences

### Tool

- RecommendationTool

### API

- getProductRecommendations()

### Expected Outcome

Customer receives personalized product recommendations based on order history and context.

---

# 6. Cancel Order

### Phrases

- Cancel my order.
- I no longer want this order.
- Stop my shipment.
- Cancel this purchase.
- Cancel the selected order.

### Entities

- selected_order_id

### Tool

- CancellationTool

### API

- cancelOrder()

### Expected Outcome

Eligible order is cancelled and cancellation confirmation is provided.
