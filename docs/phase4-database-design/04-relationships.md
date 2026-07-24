# Phase 4.4.4 – Database Relationships

> **Project:** AI Inventory Decision Intelligence Platform

---

# Overview

This document defines all relationships between database entities. These relationships enforce referential integrity, support efficient queries, and ensure consistency across the application.

---

# Relationship Types

The database primarily uses **One-to-Many (1:N)** relationships. Each child record references a parent record using a Foreign Key.

---

# Relationship Matrix

| Parent Table | Child Table | Foreign Key | Relationship |
|--------------|-------------|-------------|--------------|
| roles | users | role_id | One Role → Many Users |
| categories | products | category_id | One Category → Many Products |
| products | inventory | product_id | One Product → Many Inventory Records |
| warehouses | inventory | warehouse_id | One Warehouse → Many Inventory Records |
| suppliers | purchase_orders | supplier_id | One Supplier → Many Purchase Orders |
| products | purchase_orders | product_id | One Product → Many Purchase Orders |
| products | sales_history | product_id | One Product → Many Sales Records |
| products | demand_forecasts | product_id | One Product → Many Forecasts |
| products | recommendations | product_id | One Product → Many Recommendations |
| users | audit_logs | user_id | One User → Many Audit Logs |

---

# Relationship Details

## Roles → Users

- One role can be assigned to many users.
- Every user must belong to one role.

Foreign Key:

```
users.role_id → roles.role_id
```

---

## Categories → Products

- One category can contain many products.
- Every product belongs to one category.

Foreign Key:

```
products.category_id → categories.category_id
```

---

## Products → Inventory

- A product can exist in multiple warehouses.
- Each inventory record belongs to one product.

Foreign Key:

```
inventory.product_id → products.product_id
```

---

## Warehouses → Inventory

- One warehouse stores many inventory records.
- Each inventory record belongs to one warehouse.

Foreign Key:

```
inventory.warehouse_id → warehouses.warehouse_id
```

---

## Suppliers → Purchase Orders

- One supplier can receive many purchase orders.

Foreign Key:

```
purchase_orders.supplier_id → suppliers.supplier_id
```

---

## Products → Purchase Orders

- One product can appear in many purchase orders.

Foreign Key:

```
purchase_orders.product_id → products.product_id
```

---

## Products → Sales History

- One product can have many historical sales records.

Foreign Key:

```
sales_history.product_id → products.product_id
```

---

## Products → Demand Forecasts

- One product can have multiple forecast versions over time.

Foreign Key:

```
demand_forecasts.product_id → products.product_id
```

---

## Products → Recommendations

- Multiple AI-generated recommendations can exist for one product.

Foreign Key:

```
recommendations.product_id → products.product_id
```

---

## Users → Audit Logs

- Every audit log is linked to the user who performed the action.

Foreign Key:

```
audit_logs.user_id → users.user_id
```

---

# Referential Integrity Rules

- Parent records must exist before child records are inserted.
- Foreign key constraints prevent orphan records.
- Updates should preserve integrity.
- Deletes should use appropriate cascade or restrict policies depending on business rules.

---

# Future Relationships

The database design allows future expansion with entities such as:

- Customers
- Sales Orders
- Inventory Transfers
- Shipments
- Notifications
- AI Models
- Forecast Versions
- Warehousing Zones
- Product Images

---

# Conclusion

The defined relationships provide a scalable and normalized relational structure for the AI Inventory Decision Intelligence Platform. They ensure data consistency while supporting transactional operations, analytics, and AI-driven decision making.