# MVP Scope

## Objective

Build the smallest reliable restaurant POS as one standalone Android application that supports a complete table-service transaction:

1. Administrator configures products, categories, modifiers, users, tables, payment methods, and printers inside the Android app.
2. Waiter logs in on an Android tablet running the same application.
3. Waiter opens an available table.
4. Waiter adds products, modifiers, and kitchen notes.
5. Waiter sends new items to the kitchen.
6. The main cashier Android device persists and prints the kitchen ticket.
7. Cashier retrieves the table order.
8. Cashier accepts payment.
9. Order closes and the table becomes available.
10. Changes synchronize to the cloud when internet access is available.

## Single-application boundary

The MVP produces one Android APK containing:

- Capacitor web frontend
- Waiter interface
- Cashier interface
- Complete back office
- System administration screens
- Java Android foreground service
- Embedded REST and WebSocket server
- SQLite / Room local database
- ESC/POS kitchen and receipt printing
- Background cloud synchronization

The MVP does not require a separate web application, desktop application, cloud-dependent frontend, local mini-PC, or separately deployed back-office system.

## Device modes

### Primary cashier device

Runs server mode and owns:

- Authoritative local restaurant database
- Local API and WebSocket server
- Kitchen and receipt printing
- Synchronization outbox
- Device pairing and system status

### Waiter device

Runs the same APK in waiter mode and connects to the primary cashier device through the restaurant LAN.

### Administrator usage

Back-office screens run within the same APK. They can be used directly on the cashier device or another authorized Android device, subject to the chosen authority and synchronization rules.

## Waiter capabilities

- PIN login
- View table status
- Open a table
- Add products and modifiers
- Add kitchen notes
- Edit or remove unsent items
- Send new items to kitchen
- Add another round
- View previous kitchen submissions
- Request payment

Waiters cannot process payments, change protected prices, perform refunds, or access administrator functions.

## Cashier capabilities

- PIN login
- Create counter orders
- Retrieve table orders
- Review order totals
- Accept one payment method
- Calculate cash change
- Close order
- Release table
- Print or reprint receipt
- View and retry printer failures

## Administrator capabilities

All administrator functions are part of the Android application and must be usable without internet:

- Products and categories
- Product prices and taxes
- Modifier groups and options
- Product-to-modifier assignments
- Tables
- Users and roles
- Payment methods
- Printers and routing
- Basic reports
- System and synchronization status
- Backup and diagnostics controls

## Offline boundary

Internet loss must not prevent:

- Login for previously authorized users
- Local back-office configuration
- Counter and table orders
- Kitchen printing
- Cash payment
- Receipt printing
- Order closure
- Table release

The main Android server device must be running for multi-device restaurant operation. Secondary devices should show a clear `LOCAL_SERVER_UNAVAILABLE` state when they cannot reach it.

## Explicitly out of scope

- Separate web or desktop back office
- Separate mandatory local-server deployment
- Browser-side provisional orders while the main Android device is unreachable
- Split payments
- Tips
- Refunds
- Loyalty and gift cards
- Reservations
- Delivery and online ordering
- Advanced inventory and purchasing
- Accounting integration
- Kitchen display system
- Complex table merge and split
- Multi-server high availability
