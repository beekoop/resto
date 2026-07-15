# Restaurant POS MVP

An offline-first restaurant point-of-sale system for quick-service and small table-service restaurants, delivered as one standalone Android application.

## Primary MVP goal

A waiter can open a table order, add products and modifiers, send new items to the kitchen, and a cashier can collect payment and close the table.

## Product architecture

The complete product is packaged in a single Android APK. The application contains the front end, back office, local server, local database, printing, and synchronization components.

```text
Standalone Android application
|- Capacitor web frontend
|  |- Waiter mode
|  |- Cashier mode
|  |- Back-office mode
|  `- System status
|- Java Android native layer
|  |- Foreground service
|  |- Embedded REST and WebSocket server
|  |- SQLite / Room
|  |- ESC/POS printing
|  |- Background synchronization
|  `- Device and network integration
`- Local operational data
   |- Catalog and configuration
   |- Users and permissions
   |- Tables and orders
   |- Payments
   |- Print jobs
   `- Synchronization outbox
```

The primary cashier Android device runs server mode and is the restaurant-local source of truth. The same APK can run in waiter, cashier, or administrator mode. A waiter tablet may also use the embedded local web interface if that deployment option is enabled later.

The system remains operational without internet as long as the main Android device, local database, and required local network or printer connection are available.

## User roles

- **Waiter:** table and order-taking only
- **Cashier:** counter orders, payments, receipts, and order closure
- **Administrator:** products, categories, modifiers, users, tables, printers, reports, and system configuration

## MVP capabilities

- One standalone Android APK
- Capacitor-based responsive frontend bundled in the APK
- Offline back-office operations
- PIN login and role-based navigation
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

- Separate desktop or web back-office deployment
- Separate mandatory local server or mini-PC
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
