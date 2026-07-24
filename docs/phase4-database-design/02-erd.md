# Phase 4.4.2 – Entity Relationship Diagram (ERD)

> **Project:** AI Inventory Decision Intelligence Platform

---

# Overview

The Entity Relationship Diagram (ERD) defines the logical relationships between the core entities of the AI Inventory Decision Intelligence Platform.

The database follows a normalized relational model designed to support inventory management, procurement, demand forecasting, recommendation generation, and enterprise reporting.

---

# Core Entities

- Users
- Roles
- Categories
- Products
- Warehouses
- Inventory
- Suppliers
- Purchase Orders
- Sales History
- Demand Forecasts
- Recommendations
- Audit Logs

---

# Entity Relationship Diagram

```mermaid
erDiagram

    ROLES ||--o{ USERS : has

    CATEGORIES ||--o{ PRODUCTS : categorizes

    PRODUCTS ||--o{ INVENTORY : stored_as

    WAREHOUSES ||--o{ INVENTORY : contains

    SUPPLIERS ||--o{ PURCHASE_ORDERS : receives

    PRODUCTS ||--o{ PURCHASE_ORDERS : ordered_for

    PRODUCTS ||--o{ SALES_HISTORY : sold

    PRODUCTS ||--o{ DEMAND_FORECASTS : predicted_for

    PRODUCTS ||--o{ RECOMMENDATIONS : recommends

    USERS ||--o{ AUDIT_LOGS : performs

    USERS {
        int user_id PK
        int role_id FK
        string first_name
        string last_name
        string email
        string password_hash
        boolean is_active
        datetime created_at
    }

    ROLES {
        int role_id PK
        string role_name
        string description
    }

    CATEGORIES {
        int category_id PK
        string category_name
        string description
    }

    PRODUCTS {
        int product_id PK
        int category_id FK
        string sku
        string product_name
        decimal unit_price
        boolean is_active
    }

    WAREHOUSES {
        int warehouse_id PK
        string warehouse_name
        string city
        string state
        string country
    }

    INVENTORY {
        int inventory_id PK
        int product_id FK
        int warehouse_id FK
        int quantity
        int safety_stock
        int reorder_level
    }

    SUPPLIERS {
        int supplier_id PK
        string supplier_name
        string email
        string phone
    }

    PURCHASE_ORDERS {
        int purchase_order_id PK
        int supplier_id FK
        int product_id FK
        int quantity
        datetime order_date
        string status
    }

    SALES_HISTORY {
        int sales_id PK
        int product_id FK
        date sales_date
        int quantity_sold
    }

    DEMAND_FORECASTS {
        int forecast_id PK
        int product_id FK
        date forecast_date
        decimal predicted_demand
        decimal confidence_score
    }

    RECOMMENDATIONS {
        int recommendation_id PK
        int product_id FK
        string recommendation_type
        int reorder_quantity
        datetime generated_at
    }

    AUDIT_LOGS {
        int log_id PK
        int user_id FK
        string action
        datetime timestamp
    }
```

---

# Relationship Summary

| Parent Entity | Child Entity | Relationship |
|---------------|-------------|--------------|
| Roles | Users | One-to-Many |
| Categories | Products | One-to-Many |
| Products | Inventory | One-to-Many |
| Warehouses | Inventory | One-to-Many |
| Suppliers | Purchase Orders | One-to-Many |
| Products | Purchase Orders | One-to-Many |
| Products | Sales History | One-to-Many |
| Products | Demand Forecasts | One-to-Many |
| Products | Recommendations | One-to-Many |
| Users | Audit Logs | One-to-Many |

---

# Database Design Notes

- Every table has a Primary Key.
- Foreign Keys enforce referential integrity.
- Business entities are normalized to Third Normal Form (3NF).
- Timestamp fields are included where operational tracking is required.
- The design supports future extensions such as multi-warehouse management, multi-tenant deployments, and advanced analytics.

---

# Conclusion

This ER Diagram represents the logical data model of the AI Inventory Decision Intelligence Platform. It defines the relationships among business entities and serves as the blueprint for SQL schema creation, SQLAlchemy models, REST API implementation, and Machine Learning data pipelines.