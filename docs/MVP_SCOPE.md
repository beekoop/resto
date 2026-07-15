# MVP Scope

## Objective

Build the smallest reliable restaurant POS that supports a complete table-service transaction:

1. Waiter logs in.
2. Waiter opens an available table.
3. Waiter adds products, modifiers, and kitchen notes.
4. Waiter sends new items to the kitchen.
5. A kitchen ticket is persisted and printed exactly once.
6. Cashier retrieves the table order.
7. Cashier accepts payment.
8. Order closes and table becomes available.

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

Waiters cannot process payments, change prices, perform refunds, or access back-office functions.

## Cashier capabilities

- PIN login
- Create counter order
- Retrieve table orders
- Review order totals
- Accept one payment method
- Calculate cash change
- Close order
- Release table
- Print or reprint receipt
- View printer failures

## Administrator capabilities

- Products and categories
- Product prices and taxes
- Modifier groups and options
- Tables
- Users and roles
- Payment methods
- Printers and routing
- Basic reports
- System status

## Offline boundary

Internet loss must not prevent local ordering, kitchen printing, cash payment, receipts, or local back-office operations.

The MVP requires the Android local server to be reachable. Browser-side provisional ordering while the local server is unavailable is postponed.
