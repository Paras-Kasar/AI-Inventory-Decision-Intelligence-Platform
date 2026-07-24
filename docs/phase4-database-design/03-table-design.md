# Phase 4.4.3 – Table Design

> **Project:** AI Inventory Decision Intelligence Platform

---

# Overview

This document defines the structure of every database table, including columns, data types, primary keys, foreign keys, constraints, and default values.

---

# 1. Roles

| Column | Data Type | Constraints |
|---------|-----------|------------|
| role_id | SERIAL | PRIMARY KEY |
| role_name | VARCHAR(50) | UNIQUE, NOT NULL |
| description | TEXT | NULL |

---

# 2. Users

| Column | Data Type | Constraints |
|---------|-----------|------------|
| user_id | SERIAL | PRIMARY KEY |
| role_id | INTEGER | FK → roles.role_id |
| first_name | VARCHAR(100) | NOT NULL |
| last_name | VARCHAR(100) | NOT NULL |
| email | VARCHAR(255) | UNIQUE, NOT NULL |
| password_hash | TEXT | NOT NULL |
| is_active | BOOLEAN | DEFAULT TRUE |
| created_at | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP |
| updated_at | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP |

---

# 3. Categories

| Column | Data Type | Constraints |
|---------|-----------|------------|
| category_id | SERIAL | PRIMARY KEY |
| category_name | VARCHAR(100) | UNIQUE, NOT NULL |
| description | TEXT | NULL |

---

# 4. Products

| Column | Data Type | Constraints |
|---------|-----------|------------|
| product_id | SERIAL | PRIMARY KEY |
| category_id | INTEGER | FK → categories.category_id |
| sku | VARCHAR(100) | UNIQUE, NOT NULL |
| product_name | VARCHAR(255) | NOT NULL |
| description | TEXT | NULL |
| unit_price | NUMERIC(10,2) | NOT NULL |
| is_active | BOOLEAN | DEFAULT TRUE |
| created_at | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP |

---

# 5. Warehouses

| Column | Data Type | Constraints |
|---------|-----------|------------|
| warehouse_id | SERIAL | PRIMARY KEY |
| warehouse_name | VARCHAR(150) | NOT NULL |
| city | VARCHAR(100) | NOT NULL |
| state | VARCHAR(100) | NOT NULL |
| country | VARCHAR(100) | NOT NULL |

---

# 6. Inventory

| Column | Data Type | Constraints |
|---------|-----------|------------|
| inventory_id | SERIAL | PRIMARY KEY |
| product_id | INTEGER | FK → products.product_id |
| warehouse_id | INTEGER | FK → warehouses.warehouse_id |
| quantity | INTEGER | NOT NULL |
| safety_stock | INTEGER | DEFAULT 0 |
| reorder_level | INTEGER | DEFAULT 0 |
| last_updated | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP |

---

# 7. Suppliers

| Column | Data Type | Constraints |
|---------|-----------|------------|
| supplier_id | SERIAL | PRIMARY KEY |
| supplier_name | VARCHAR(255) | NOT NULL |
| email | VARCHAR(255) | UNIQUE |
| phone | VARCHAR(20) | NULL |
| address | TEXT | NULL |

---

# 8. Purchase Orders

| Column | Data Type | Constraints |
|---------|-----------|------------|
| purchase_order_id | SERIAL | PRIMARY KEY |
| supplier_id | INTEGER | FK → suppliers.supplier_id |
| product_id | INTEGER | FK → products.product_id |
| quantity | INTEGER | NOT NULL |
| unit_cost | NUMERIC(10,2) | NOT NULL |
| order_date | DATE | NOT NULL |
| expected_delivery | DATE | NULL |
| status | VARCHAR(50) | NOT NULL |

---

# 9. Sales History

| Column | Data Type | Constraints |
|---------|-----------|------------|
| sales_id | SERIAL | PRIMARY KEY |
| product_id | INTEGER | FK → products.product_id |
| sales_date | DATE | NOT NULL |
| quantity_sold | INTEGER | NOT NULL |
| revenue | NUMERIC(12,2) | NOT NULL |

---

# 10. Demand Forecasts

| Column | Data Type | Constraints |
|---------|-----------|------------|
| forecast_id | SERIAL | PRIMARY KEY |
| product_id | INTEGER | FK → products.product_id |
| forecast_date | DATE | NOT NULL |
| predicted_demand | NUMERIC(10,2) | NOT NULL |
| confidence_score | NUMERIC(5,2) | NOT NULL |
| model_version | VARCHAR(50) | NOT NULL |

---

# 11. Recommendations

| Column | Data Type | Constraints |
|---------|-----------|------------|
| recommendation_id | SERIAL | PRIMARY KEY |
| product_id | INTEGER | FK → products.product_id |
| recommendation_type | VARCHAR(100) | NOT NULL |
| reorder_quantity | INTEGER | NOT NULL |
| priority | VARCHAR(30) | NOT NULL |
| generated_at | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP |

---

# 12. Audit Logs

| Column | Data Type | Constraints |
|---------|-----------|------------|
| log_id | SERIAL | PRIMARY KEY |
| user_id | INTEGER | FK → users.user_id |
| action | VARCHAR(255) | NOT NULL |
| entity_name | VARCHAR(100) | NOT NULL |
| entity_id | INTEGER | NOT NULL |
| timestamp | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP |
| ip_address | VARCHAR(50) | NULL |

---

# Summary

- Total Tables: **12**
- Primary Keys: **12**
- Foreign Keys: **10**
- Database: **PostgreSQL**
- ORM: **SQLAlchemy**
- Migration Tool: **Alembic**