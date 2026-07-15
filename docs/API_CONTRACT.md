# Initial API Contract

Base path: `/api/v1`

## System

```http
GET /system/status
```

## Authentication

```http
POST /auth/pin-login
POST /auth/logout
GET  /session
```

## Catalog

```http
GET /categories
GET /products
GET /modifier-groups
GET /modifiers
```

## Tables

```http
GET  /tables
POST /tables/{tableId}/open
GET  /tables/{tableId}/active-order
```

## Orders

```http
POST   /orders
GET    /orders/{orderId}
GET    /orders?status=OPEN
POST   /orders/{orderId}/lines
PATCH  /orders/{orderId}/lines/{lineId}
DELETE /orders/{orderId}/lines/{lineId}
POST   /orders/{orderId}/send-to-kitchen
POST   /orders/{orderId}/request-payment
POST   /orders/{orderId}/cancel
```

## Payments

```http
GET  /open-orders
POST /orders/{orderId}/checkout
GET  /orders/{orderId}/payments
```

## Printing

```http
GET  /print-jobs
POST /print-jobs/{printJobId}/retry
POST /kitchen-submissions/{submissionId}/reprint
POST /printers/{printerId}/test
```

## Command envelope

Every write command includes:

```json
{
  "commandId": "uuid",
  "expectedOrderVersion": 4
}
```

The server returns the stored result when the same command is retried.
