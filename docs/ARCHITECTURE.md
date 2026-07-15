# Architecture

## Governing decision

The Restaurant POS MVP is delivered as one standalone Android application. It contains the complete user interface, offline back office, local REST server, SQLite database, kitchen and receipt printing, and cloud synchronization capabilities.

There are no separately deployed frontend, back-office, or mandatory local-server applications in the MVP.

## Deployment model

The main cashier Android device runs the application in server mode and acts as the restaurant-local operational source of truth.

```text
Main cashier Android device
|
|- Capacitor web frontend
|  |- Waiter mode
|  |- Cashier mode
|  |- Back-office mode
|  `- System status
|
|- Java Android native layer
|  |- Foreground service
|  |- Embedded HTTP / REST server
|  |- WebSocket notifications
|  |- SQLite / Room
|  |- Print worker
|  |- Sync worker
|  `- Android device integration
|
`- Local restaurant database
   |- Catalog and configuration
   |- Users and permissions
   |- Tables and active orders
   |- Payments and receipts
   |- Print queue
   `- Synchronization outbox
```

Additional waiter tablets use the same APK in waiter mode. They connect over the restaurant LAN to the server mode running on the main cashier device. A browser-based thin-client option may be supported later because the frontend is web-based, but it is not a separate MVP deliverable.

## Application modes

### Server mode

Enabled on the primary cashier device:

- Hosts the local REST API
- Hosts WebSocket notifications
- Owns the authoritative SQLite database
- Coordinates table and order state
- Owns kitchen and receipt printing
- Runs cloud synchronization
- Publishes health and diagnostics information

### Waiter mode

- PIN login
- Table selection
- Product and modifier selection
- Kitchen notes
- Send new items to kitchen
- View sent and unsent lines
- No financial operations

### Cashier mode

- Counter and table orders
- Retrieve open orders
- Accept payments
- Print receipts
- Close orders and release tables
- Monitor printer failures

### Back-office mode

- Products and categories
- Modifier groups and options
- Tables
- Users and roles
- Taxes and payment methods
- Printer configuration
- Reports and system status

All back-office operations must work without internet and write to the local database first.

## Frontend architecture

The responsive frontend is bundled inside the APK using Capacitor. Suggested routes include:

```text
/login
/waiter/tables
/waiter/orders/:id
/cashier/orders
/cashier/payment/:id
/backoffice/products
/backoffice/categories
/backoffice/modifiers
/backoffice/tables
/backoffice/users
/backoffice/printers
/system/status
```

The local frontend communicates with the embedded server using the loopback interface. Secondary Android devices connect using the main device's authorized LAN address.

## Main technical decisions

- One Android APK and one codebase
- Capacitor frontend bundled inside the application
- Java Android native services
- Foreground service for server availability
- Embedded REST and WebSocket server
- SQLite / Room local operational database
- Main cashier device as the local source of truth
- Centralized ESC/POS printing from the native layer
- Persistent print queue
- Outbox-based cloud synchronization
- Command IDs for idempotency
- Optimistic order versions for concurrent editing
- Role- and device-mode-based navigation

## Suggested modules

```text
app-shell
identity
catalog
restaurant
ordering
kitchen
payment
printing
backoffice
reporting
audit
synchronization
system-status
shared
```

## Repository structure

```text
/
|- README.md
|- docs/
|  |- architecture/
|  |- requirements/
|  |- api/
|  |- database/
|  |- screens/
|  `- testing/
|- android/
|  |- app/
|  |- native-server/
|  |- printing/
|  |- sync/
|  `- capacitor-web/
`- tools/
```

## Reliability principles

- Persist locally before acknowledging a successful operation
- Keep local operations available without internet
- Never trust client-submitted totals
- Never print directly from frontend JavaScript
- Never silently repeat a payment or kitchen submission
- Distinguish order acceptance from physical print success
- Keep sensitive state transitions transactional
- Recover active orders, print jobs, and sync events after app or device restart
