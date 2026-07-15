# Acceptance Tests

## Core flow

### Open table

Given Table 2 is available  
When a waiter opens Table 2  
Then a table session and order are created  
And Table 2 becomes occupied.

### Add product

Given an open order  
When the waiter adds Grilled Chicken with valid modifiers  
Then the line is saved as `NOT_SENT`  
And totals are calculated by the server.

### Send to kitchen

Given an order with unsent items  
When the waiter sends the order  
Then one immutable kitchen submission is created  
And one print job is persisted  
And submitted lines become sent.

### Retry kitchen command

Given a kitchen command was processed  
When the same `commandId` is submitted again  
Then the original response is returned  
And no additional ticket is created.

### Checkout

Given an unpaid table order  
When the cashier completes cash payment  
Then one payment is recorded  
And the order closes  
And the table becomes available  
And one receipt print job is created.

### Retry checkout

Given checkout completed successfully  
When the same command is retried  
Then the original payment result is returned  
And no second payment is created.

## Failure cases

- Two waiters attempt to open the same table
- Browser loses connection after command processing
- Printer is offline
- Internet is offline
- Android service restarts
- Order version is stale
- Two cashiers attempt payment
- Waiter attempts payment
