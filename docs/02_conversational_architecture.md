# Conversational Architecture

## Overview

The Retail Fashion Voice Agent is designed to automate common customer support journeys through a secure, voice-enabled conversational experience.

The system authenticates customers using Phone Number and PIN verification before allowing access to order-related actions.

Once authenticated, the agent retrieves all orders associated with the customer account, enables order selection, and routes requests to specialized sub-agents responsible for specific business functions.

The architecture follows a modular multi-agent approach where each customer journey is handled independently while sharing a common authentication and order-context layer.

---

## Architecture Principles

The solution is designed around the following principles:

- Secure customer authentication
- Context-aware conversations
- Modular agent design
- API-driven business operations
- Controlled escalation handling
- Reusable conversational components

---

# Main Agent Flow

## Purpose

The Main Agent acts as the orchestration layer for the entire customer journey.

### Responsibilities

- Customer greeting
- Authentication
- Customer profile retrieval
- Order retrieval
- Order selection
- Session context management
- Service routing

### Session Entity Stored

- selected_order_id

```mermaid
flowchart TD

A([Customer Initiates Voice Call])

--> B[Greeting Agent<br/>Welcome Customer]

--> C[Request Phone Number]

--> D[Request PIN]

--> E{Authentication Successful?}

E -- No --> F[Authentication Failed]

F --> G[Allow Retry]

G --> H{Attempts < 3?}

H -- Yes --> C

H -- No --> I[Escalate to Human Agent]

E -- Yes --> J[Fetch Orders Associated with Phone Number]

J --> K[Present Available Orders]

K --> L[Customer Selects Order ID]

L --> M{Valid Order ID?}

M -- No --> N[Ask Customer to Re-select Order]

N --> L

M -- Yes --> O[Store selected_order_id as Session Entity]

O --> P[Present Service Menu]

P --> Q[Check Order Status]

P --> R[Order Modification]

P --> S[Return / Exchange]

P --> T[Refund Status]

P --> U[Order Cancellation]
```

---

# Order Status Sub-Agent

## Purpose

Provide customers with real-time order and delivery status information.

### Primary Tool

- OrderLookupTool

### Expected Outcome

Customer receives current order status and delivery information.

```mermaid
flowchart TD

A[Customer Selects<br/>Check Order Status]

--> B[Retrieve selected_order_id<br/>from Session Entity]

--> C[Invoke OrderLookupTool]

--> D{Tool Response Received?}

D -- No --> E[Inform Customer Service is Temporarily Unavailable]

E --> F[Offer Human Agent Escalation]

D -- Yes --> G[Fetch Order Details]

G --> H[Fetch Delivery Status]

H --> I[Generate Customer-Friendly Summary]

I --> J[Present Status to Customer]

J --> K[Would You Like Help With Anything Else?]

K --> L[Return to Service Menu]
```

---

# Order Modification Sub-Agent

## Purpose

Allow customers to modify eligible orders.

### Supported Modifications

- Delivery Address
- Delivery Date
- Contact Number

### Primary Tool

- OrderModificationTool

### Expected Outcome

Order details are updated successfully after customer confirmation.

```mermaid
flowchart TD

A[Customer Selects<br/>Return / Exchange]

--> B[Retrieve selected_order_id<br/>from Session Entity]

--> C[Invoke ReturnEligibilityTool]

--> D{Eligible for Return/Exchange?}

D -- No --> E[Inform Customer Item is Not Eligible]

E --> F[Return to Service Menu]

D -- Yes --> G[Ask Customer:<br/>Return or Exchange?]

%% RETURN FLOW

G --> H[Return]

H --> I[Invoke ReturnTool]

I --> J[Invoke SlotBookingTool]

J --> K[Schedule Pickup Slot]

K --> L[Generate Return Confirmation]

L --> M[Present Return Details]

M --> N[Return to Service Menu]

%% EXCHANGE FLOW

G --> O[Exchange]

O --> P[Capture Exchange Preference]

P --> Q[Invoke ExchangeTool]

Q --> R[Invoke RecommendationTool]

R --> S[Present Alternative Products<br/>Upsell / Cross-Sell]

S --> T{Customer Selects Product?}

T -- Yes --> U[Confirm Replacement Item]

T -- No --> U

U --> V[Invoke SlotBookingTool]

V --> W[Schedule Pickup / Delivery Slot]

W --> X[Generate Exchange Confirmation]

X --> Y[Present Exchange Details]

Y --> Z[Return to Service Menu]
```

---

# Return / Exchange Sub-Agent

## Purpose

Handle customer return and exchange requests.

### Primary Tools

- ReturnEligibilityTool
- ReturnTool
- ExchangeTool
- RecommendationTool
- SlotBookingTool

### Expected Outcome

Return pickup or exchange process is successfully initiated.

```mermaid
flowchart TD

A[Customer Selects<br/>Return / Exchange]

--> B[Retrieve selected_order_id<br/>from Session Entity]

--> C[Invoke ReturnEligibilityTool]

--> D{Eligible for Return/Exchange?}

D -- No --> E[Inform Customer Item is Not Eligible]

E --> F[Return to Service Menu]

D -- Yes --> G[Ask Customer:<br/>Return or Exchange?]

%% RETURN FLOW

G --> H[Return]

H --> I[Invoke ReturnTool]

I --> J[Invoke SlotBookingTool]

J --> K[Schedule Pickup Slot]

K --> L[Generate Return Confirmation]

L --> M[Present Return Details]

M --> N[Return to Service Menu]

%% EXCHANGE FLOW

G --> O[Exchange]

O --> P[Capture Exchange Preference]

P --> Q[Invoke ExchangeTool]

Q --> R[Invoke RecommendationTool]

R --> S[Present Alternative Products<br/>Upsell / Cross-Sell]

S --> T{Customer Selects Product?}

T -- Yes --> U[Confirm Replacement Item]

T -- No --> U

U --> V[Invoke SlotBookingTool]

V --> W[Schedule Pickup / Delivery Slot]

W --> X[Generate Exchange Confirmation]

X --> Y[Present Exchange Details]

Y --> Z[Return to Service Menu]
```

---

# Refund Status Sub-Agent

## Purpose

Provide refund tracking and status updates.

### Primary Tool

- RefundTrackerTool

### Expected Outcome

Customer receives refund amount, refund status, and processing information.

```mermaid
flowchart TD

A[Customer Selects<br/>Refund Status]

--> B[Retrieve selected_order_id<br/>from Session Entity]

--> C[Invoke RefundTrackerTool]

--> D{Tool Response Received?}

D -- No --> E[Inform Customer Service is Temporarily Unavailable]

E --> F[Offer Human Agent Escalation]

D -- Yes --> G{Refund Record Found?}

G -- No --> H[Inform Customer No Refund Request Exists]

H --> I[Return to Service Menu]

G -- Yes --> J[Retrieve Refund Details]

J --> K[Retrieve Refund Status]

K --> L[Retrieve Refund Amount]

L --> M[Generate Customer-Friendly Summary]

M --> N[Present Refund Information]

N --> O[Would You Like Help With Anything Else?]

O --> P[Return to Service Menu]
```

---

# Order Cancellation Sub-Agent

## Purpose

Handle eligible order cancellation requests.

### Primary Tool

- CancellationTool

### Expected Outcome

Order cancellation request is processed and confirmation is provided.

```mermaid
flowchart TD

A[Customer Selects<br/>Order Cancellation]

--> B[Retrieve selected_order_id<br/>from Session Entity]

--> C[Invoke CancellationTool]

--> D{Cancellation Eligible?}

D -- No --> E[Inform Customer Order Cannot Be Cancelled]

E --> F[Provide Reason<br/>Already Shipped / Delivered / Already Cancelled]

F --> G[Return to Service Menu]

D -- Yes --> H[Present Cancellation Details]

H --> I[Ask Customer for Confirmation]

I --> J{Customer Confirms?}

J -- No --> K[Cancel Cancellation Request]

K --> L[Return to Service Menu]

J -- Yes --> M[Execute Cancellation]

M --> N{Cancellation Successful?}

N -- No --> O[Inform Customer Cancellation Failed]

O --> P[Offer Human Agent Escalation]

N -- Yes --> Q[Generate Cancellation Confirmation]

Q --> R[Present Cancellation Details]

R --> S[Inform Customer Refund Timeline]

S --> T[Return to Service Menu]
```

---

# Error Handling Strategy

The system handles the following failure scenarios:

- Authentication failures
- Invalid order selection
- Tool execution failures
- API timeouts
- Business rule violations

When automated resolution is not possible, the conversation is transferred to a human support agent with context preservation.

---

# Session Context Management

| Entity | Purpose |
|----------|----------|
| customer_id | Customer identification |
| selected_order_id | Selected order context |
| service_type | Active customer journey |
| authentication_status | Verification status |

---

# Escalation Strategy

Escalation is triggered when:

- Authentication fails after multiple attempts
- Backend services are unavailable
- Customer explicitly requests a human agent
- Business rules prevent automated resolution

Conversation context is transferred to minimize customer effort and repetition.
