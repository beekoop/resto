# Roadmap

## Phase 1: Freeze the single-app architecture

- Confirm one standalone Android APK
- Define waiter, cashier, administrator, and server modes
- Confirm supported Android versions and screen sizes
- Confirm primary cashier device responsibilities
- Confirm waiter-device connection model
- Remove separate frontend, back-office, and local-node deployments from the MVP

## Phase 2: Android and Capacitor foundation

- Create Java Android project
- Add Capacitor frontend
- Configure development, UAT, and production builds
- Add foreground service
- Add secure local configuration
- Add boot recovery
- Add application logging
- Add device identity

## Phase 3: Embedded local server

- Embedded HTTP / REST server
- WebSocket notifications
- Session management
- Health endpoint
- Loopback communication for the bundled frontend
- Authorized LAN communication for secondary devices
- Device pairing and connection status

## Phase 4: Local database and reliability foundation

- SQLite / Room migrations
- Repository abstraction
- Local transactions
- Processed-command table
- Idempotency handling
- Audit events
- Synchronization outbox
- Restart recovery

## Phase 5: Offline back office

- Categories
- Products and prices
- Taxes
- Modifier groups and options
- Product-to-modifier assignments
- Tables
- Users and roles
- Payment methods
- Printers and routing
- Local configuration status

## Phase 6: Core waiter ordering

- PIN login
- Role- and device-mode navigation
- Table grid
- Table sessions
- Product catalog and search
- Product selection
- Modifier validation
- Kitchen notes
- Order and line management
- Server-calculated totals
- Sent and unsent line states

## Phase 7: Kitchen workflow

- Immutable kitchen submissions
- Persistent print queue
- Simulated printer
- ESC/POS network printing
- Printer routing
- Retry and reprint
- Printer status and diagnostics

At the end of this phase, a waiter can send a valid table order to the kitchen.

## Phase 8: Cashier settlement

- Open-order list
- Retrieve table order
- Cash payment
- Change calculation
- Atomic checkout
- Receipt generation
- Receipt printing
- Order closure
- Table release

At the end of this phase, a cashier can collect payment and close the table.

## Phase 9: Multi-device operation

- Same APK in waiter mode
- QR-code pairing
- Fixed-IP configuration
- Optional mDNS discovery
- Device authorization
- WebSocket order updates
- Reconnection handling
- Clear local-server-unavailable state

## Phase 10: Cloud synchronization

- Background sync worker
- Local outbox processing
- Cloud acknowledgements
- Retry with backoff
- Sync checkpoints
- Configuration download
- Conflict recording and policy
- Sync status UI

## Phase 11: System administration

- Local server status
- Connected devices
- Database status
- Printer status
- Pending and failed print jobs
- Pending and failed sync events
- Application and schema versions
- Backup, restore, export, and diagnostics

## Phase 12: Reports

- Daily sales
- Payment-method summary
- Product sales
- Open orders
- Cancelled and voided orders
- Waiter and cashier summaries
- Printer and synchronization failures

## Phase 13: Hardening and pilot

- Unit and integration tests
- End-to-end vertical-slice tests
- Offline and restart tests
- Duplicate-command tests
- Concurrent order tests
- Printer-failure tests
- Security review
- Pilot restaurant deployment
- Staff training
- Production-readiness checklist
