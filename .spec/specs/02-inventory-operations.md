# Spec 02: Inventory Operations & Concurrency Rules

## REST Contracts & Behaviours
- `POST /api/v1/inventory/receipts`: Increases `quantity`. Creates `RECEIPT` movement.
- `POST /api/v1/inventory/issues`: Verifies `available >= requested`. Decreases `quantity`. Creates `ISSUE` movement.
- `POST /api/v1/inventory/transfers`: Atomic multi-warehouse adjustment. Decreases source, increases destination. Creates two movement records.
- `POST /api/v1/inventory/reservations`: Increases `reserved_quantity`. Total `quantity` remains unchanged.

## Outbox Pattern Integration
Every inventory movement inserts a record into `outbox_events` within the same database transaction.