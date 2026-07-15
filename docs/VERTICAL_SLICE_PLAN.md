# First Vertical Slice

## Goal

Deliver one complete, testable restaurant transaction before implementing the full back office.

## Seed data

- Store: Demo Restaurant
- Users: John (Waiter), Sarah (Cashier), Mike (Administrator)
- Tables: T1, T2, T3
- Products: Tomato Soup, French Fries, Grilled Chicken
- Modifier group: Cooking Preference
- Payment method: Cash
- Printer: Simulated Kitchen Printer

## Flow

1. Start Android foreground server.
2. Open browser UI.
3. John logs in using PIN.
4. John opens Table 2.
5. John adds Grilled Chicken.
6. John selects Medium and adds a kitchen note.
7. John sends the order to kitchen.
8. Server creates an immutable submission and persistent print job.
9. Simulated printer records the ticket.
10. Sarah logs in.
11. Sarah retrieves Table 2.
12. Sarah accepts cash payment.
13. Server closes order and table session.
14. Receipt job is created.
15. Table 2 becomes available.

## Completion criteria

- No duplicate ticket from retries
- No duplicate payment from retries
- Browser refresh does not lose order
- Internet is not required
- Printer failure is visible and recoverable
- All important actions are audited
