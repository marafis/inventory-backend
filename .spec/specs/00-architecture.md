# Spec 00: Architecture & Framework Baseline

## Target Stack
- Java 21, Spring Boot 4.0.8, Spring Data JPA, Spring Security, Spring Validation
- PostgreSQL, Flyway migrations
- Apache Kafka (Transactional Outbox pattern)
- Testcontainers (PostgreSQL, Kafka) for integration testing

## Modular Monolith Structure
Packages: `com.mmr.inventory.[product|warehouse|inventory|supplier|purchaseorder|reporting|shared]`
Each module contains: `api`, `application`, `domain`, `infrastructure`.

## Concurrency & Data Integrity Strategies
- Inventory quantities: Optimistic locking via `@Version` field on `Inventory` entity.
- Database constraints: `CHECK (quantity >= 0)`, `CHECK (reserved_quantity <= quantity)`, `UNIQUE(product_id, warehouse_id)`.
- Idempotency support via `Idempotency-Key` header mapped to `idempotency_keys` table.