# Spec 01: Core Domain & Data Schema

## Entities
1. `Product`: id (UUID), sku (UNIQUE), name, description, category_id, uom, min_stock, reorder_level, status (ACTIVE/INACTIVE), version, created_at, updated_at.
2. `Warehouse`: id (UUID), code (UNIQUE), name, address, country, status.
3. `WarehouseLocation`: id, warehouse_id, code (e.g., A01-01).
4. `Inventory`: id, product_id, warehouse_id, quantity, reserved_quantity, version.
    - Formula: Available = quantity - reserved_quantity.
5. `InventoryMovement` (Immutable): id, product_id, warehouse_id, movement_type, quantity, stock_before, stock_after, reference_type, reference_id, performed_by, created_at.

## Flyway Migration Rules
- V1__init_core_schema.sql (products, warehouses, warehouse_locations, inventory, inventory_movements, idempotency_keys).