# Naming Conventions

This document outlines the naming conventions used for schemas, tables, views, columns, and other objects in the data warehouse.

---

## Table of Contents

- General Principles
- Table Naming Conventions
  - Bronze Rules
  - Silver Rules
  - Gold Rules
- Column Naming Conventions
  - Surrogate Keys
  - Technical Columns
- Stored Procedures

---

# General Principles

- **Naming Convention:** Use `snake_case`, with lowercase letters and underscores (`_`) to separate words.
- **Language:** Use English for all names.
- **Avoid Reserved Words:** Do not use SQL reserved words as object names.

---

# Table Naming Conventions

## Bronze Rules

All table names must start with the source system name, and table names must match their original names without renaming.

**Pattern**

```text
<sourcesystem>_<entity>
```

| Component | Description |
|-----------|-------------|
| `<sourcesystem>` | Name of the source system (e.g., `crm`, `erp`). |
| `<entity>` | Exact table name from the source system. |

**Example**

```text
crm_customer_info
```

> Customer information from the CRM system.

---

## Silver Rules

All table names must start with the source system name, and table names must match their original names without renaming.

**Pattern**

```text
<sourcesystem>_<entity>
```

| Component | Description |
|-----------|-------------|
| `<sourcesystem>` | Name of the source system (e.g., `crm`, `erp`). |
| `<entity>` | Exact table name from the source system. |

**Example**

```text
crm_customer_info
```

> Customer information from the CRM system.

---

## Gold Rules

All table names must use meaningful, business-aligned names and start with the category prefix.

**Pattern**

```text
<category>_<entity>
```

| Component | Description |
|-----------|-------------|
| `<category>` | Role of the table such as `dim` or `fact`. |
| `<entity>` | Business entity (e.g., `customers`, `products`, `sales`). |

### Examples

```text
dim_customers
fact_sales
```

---

## Glossary of Category Patterns

| Pattern | Meaning | Example(s) |
|---------|---------|------------|
| `dim_` | Dimension table | `dim_customer`, `dim_product` |
| `fact_` | Fact table | `fact_sales` |
| `report_` | Report table | `report_customers`, `report_sales_monthly` |

---

# Column Naming Conventions

## Surrogate Keys

All primary keys in dimension tables must use the suffix `_key`.

**Pattern**

```text
<table_name>_key
```

| Component | Description |
|-----------|-------------|
| `<table_name>` | Name of the table or entity. |
| `_key` | Indicates that the column is a surrogate key. |

**Example**

```text
customer_key
```

> Surrogate key in the `dim_customers` table.

---

## Technical Columns

All technical columns must start with the prefix `dwh_`, followed by a descriptive name.

**Pattern**

```text
dwh_<column_name>
```

| Component | Description |
|-----------|-------------|
| `dwh` | Prefix reserved for system-generated metadata. |
| `<column_name>` | Descriptive name indicating the column's purpose. |

**Example**

```text
dwh_load_date
```

> Stores the date when the record was loaded into the data warehouse.

---

# Stored Procedures

All stored procedures used for loading data must follow the naming pattern below.

**Pattern**

```text
load_<layer>
```

| Component | Description |
|-----------|-------------|
| `<layer>` | The data warehouse layer (`bronze`, `silver`, or `gold`). |

### Examples

```text
load_bronze
load_silver
load_gold
```

| Procedure | Description |
|-----------|-------------|
| `load_bronze` | Loads data into the Bronze layer. |
| `load_silver` | Loads data into the Silver layer. |
| `load_gold` | Loads data into the Gold layer. |
