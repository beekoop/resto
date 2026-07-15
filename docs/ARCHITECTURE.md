# Architecture

## Deployment model

A dedicated Android cashier device is the local restaurant server and operational source of truth.

```text
Waiter browsers        Cashier UI        Back-office browser
       \                   |                   /
                    Restaurant LAN
                          |
                  Android local server
                  - Foreground service
                  - Embedded HTTP server
                  - WebSocket notifications
                  - SQLite / Room
                  - Print worker
                  - Sync worker
                          |
                    Cloud platform
                   when internet works
```

## Main decisions

- Responsive HTML interface for browser-enabled devices
- Optional Capacitor shell on the cashier Android device
- Java Android foreground service
- Embedded REST and WebSocket server
- SQLite local database
- Centralized printing from the Android server
- Persistent print queue
- Outbox-based cloud synchronization
- Command IDs for idempotency
- Optimistic order versions for concurrent editing

## Suggested modules

```text
identity
catalog
restaurant
ordering
kitchen
payment
printing
reporting
audit
synchronization
shared
```

## Reliability principles

- Persist before acknowledging
- Never trust client totals
- Never print directly from waiter browsers
- Never silently repeat payment or kitchen submission
- Distinguish order acceptance from physical print success
- Keep all sensitive state transitions transactional
