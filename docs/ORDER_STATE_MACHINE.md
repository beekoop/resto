# Order State Machine

## Order states

```text
OPEN
  |
  +--> PARTIALLY_SENT
  |       |
  |       +--> SENT_TO_KITCHEN
  |
  +--> AWAITING_PAYMENT
          |
          +--> PAID
                  |
                  +--> CLOSED
```

Exceptional terminal states:

```text
CANCELLED
VOIDED
```

## Line kitchen states

```text
NOT_SENT -> QUEUED -> SENT
     |
     `-> CANCELLED
```

## Rules

- `OPEN`: order exists and may contain unsent lines.
- `PARTIALLY_SENT`: order contains both sent and unsent lines.
- `SENT_TO_KITCHEN`: all active lines have been submitted.
- `AWAITING_PAYMENT`: service is complete and cashier settlement is expected.
- `PAID`: valid payment exists.
- `CLOSED`: transaction and table session are complete.
