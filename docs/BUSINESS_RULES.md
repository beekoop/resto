# Business Rules

## Tables

- Only an available table can be opened.
- A table can have at most one active session.
- Closing a paid table order releases the table.
- Concurrent attempts to open the same table must return a conflict.

## Orders

- A closed or cancelled order cannot be edited.
- The server calculates all prices, taxes, and totals.
- Every mutating command contains a unique `commandId`.
- Order updates contain `expectedOrderVersion`.
- A version mismatch returns `409 Conflict`.

## Order lines

- New lines start as `NOT_SENT`.
- Only `NOT_SENT` lines can be directly edited or removed.
- Sent lines must be corrected through an explicit cancellation or adjustment flow.
- Required modifier selections must be valid before adding a line.

## Kitchen

- Sending to kitchen includes only `NOT_SENT` lines.
- At least one unsent line is required.
- Each send creates an immutable kitchen submission.
- Previously sent lines are never included automatically.
- Duplicate command IDs return the original result.
- Printer failure does not undo an accepted kitchen submission.

## Payments

- Waiters cannot create payments.
- The server recalculates the amount due before payment.
- An order cannot be paid twice.
- Checkout atomically creates payment, closes order, closes table session, releases table, creates receipt job, and records audit and sync events.
- The MVP supports one payment method per order.

## Printing

- Print jobs are persisted before physical printing.
- Kitchen and receipt printing are performed only by the local server.
- A unique printer/document constraint prevents accidental duplicate jobs.
- Failed jobs can be retried or explicitly reprinted by an authorized user.
