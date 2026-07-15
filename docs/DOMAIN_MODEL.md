# Domain Model

## Core entities

### Identity

- Store
- Device
- User
- Role
- Permission
- UserRole

### Catalog

- Category
- Product
- ProductPrice
- Tax
- ModifierGroup
- Modifier
- ProductModifierGroup

### Restaurant

- DiningTable
- TableSession

### Ordering

- Order
- OrderLine
- OrderLineModifier
- KitchenSubmission
- KitchenSubmissionLine

### Payment

- PaymentMethod
- Payment

### Printing

- Printer
- PrinterRoute
- PrintJob
- PrintAttempt

### Reliability

- ProcessedCommand
- AuditEvent
- SyncOutboxEvent

## Order aggregate

```text
Order
|- OrderLine[]
|  `- OrderLineModifier[]
|- KitchenSubmission[]
|- Payment[]
`- TableSession
```

The order owns financial totals and lifecycle rules. Kitchen submissions are immutable snapshots of newly submitted lines.

## Important snapshots

Order lines store product name, unit price, tax rate, modifier details, and calculated totals at the time of sale. Historical orders must not change when catalog configuration changes.
