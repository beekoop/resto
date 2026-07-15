# Restaurant POS MVP

An offline-first restaurant point-of-sale system for quick-service and small table-service restaurants.

## Primary MVP goal

A waiter can open a table order, add products and modifiers, send new items to the kitchen, and a cashier can collect payment and close the table.

## Architecture

The restaurant runs from a dedicated Android cashier device acting as the local server.

```text
Browser-enabled waiter tablets / cashier terminals / back-office devices
                              |
                        Local Wi-Fi
                              |
                     Android POS server
                     - Embedded HTTP API
                     - Responsive web UI
                     - SQLite database
                     - Kitchen print queue
                     - Cloud sync outbox
```

The system remains operational when the internet is unavailable, provided the local Android server and restaurant network are available.

## User roles

- **Waiter:** table and order-taking only
- **Cashier:** counter orders, payments, receipts, and order closure
- **Administrator:** catalog, users, tables, printers, and reports

## MVP capabilities

- PIN login
- Table management
- Counter and table orders
- Product categories
- Products and prices
- Modifier groups and modifiers
- Kitchen notes
- Incremental kitchen submissions
- Persistent kitchen printing
- Cash payment
- Receipt printing
- Basic audit history
- Idempotent commands
- Local offline operation
- Deferred cloud synchronization

## Explicitly out of scope

- Split payments
- Tips
- Refunds
- Loyalty and gift cards
- Reservations
- Delivery and online ordering
- Inventory and purchasing
- Accounting integration
- Kitchen display system
- Complex table merge and split
- Multi-server high availability

## Documentation

- [MVP Scope](docs/MVP_SCOPE.md)
- [Architecture](docs/ARCHITECTURE.md)
- [Domain Model](docs/DOMAIN_MODEL.md)
- [Business Rules](docs/BUSINESS_RULES.md)
- [Order State Machine](docs/ORDER_STATE_MACHINE.md)
- [API Contract](docs/API_CONTRACT.md)
- [Vertical Slice Plan](docs/VERTICAL_SLICE_PLAN.md)
- [Acceptance Tests](docs/ACCEPTANCE_TESTS.md)
- [Roadmap](docs/ROADMAP.md)
