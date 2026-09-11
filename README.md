# SQL Lecture Notes — Data Warehouse

## Advanced SQL: Data Transformation, ETL & Data Warehouse


## Main Topics

* Data Transformation from Different Sources
* ETL (Extract, Transform, Load)
* Data Warehouse Layers
* Staging Layer
* Bronze Layer
* Silver Layer
* Gold Layer
* Slowly Changing Dimensions (SCD)

---

## 1. Data Transformation, ETL & Data Warehouse

The lecture focuses on taking data from different sources, performing ETL, and storing the processed data in a Data Warehouse.

```text
Source → ETL → Data Warehouse
```

---

## 2. Staging Layer

The Staging Layer is a preparation area for incoming data.

* Data is loaded from different sources into a new database.
* The table has a structure similar to the source.
* Data types are usually stored as TEXT/String initially.
* It helps prevent data type errors during data movement.
* It safely receives raw data before further processing.

### Loading Strategies

**Truncate & Load**

* Deletes existing data.
* Loads the new data.
* Keeps only the latest data.
* Simple, but does not preserve history.

**Incremental Loading**

* Loads new or changed data.
* Keeps existing historical data.
* Preserves history, but requires more storage.

**Full Loading**

* Loads all source data every time.
* Ensures the target contains the complete source dataset.
* Requires more processing time and resources.

---

## 3. Bronze Layer

The Bronze Layer receives data from the Staging Layer.

* De-duplication is performed.
* Data is loaded incrementally.
* Historical data is preserved.
* The data remains relatively raw.

---

## 4. Silver Layer

The Silver Layer contains cleaned and historical data.

Main operations include:

* Changing data types.
* Checking missing values.
* Detecting invalid values.
* Cleaning and transforming data.
* Preserving historical data.
* Using incremental loading.

The Silver Layer is ready to be used for building the analytical data model.

---

## 5. Analysis & Data Modeling

Instead of working with one large table, the cleaned data is transformed into a suitable Data Model.

A common model for analysis is the **Star Schema**, which consists of multiple related tables.

---

## 6. Gold Layer

The Gold Layer contains the final Data Model used for analysis.

* Tables are organized according to the required model.
* Primary Keys (PK) are defined.
* Relationships between tables are established.
* The structure can follow a Star Schema.
* Data is prepared for analytical queries and reporting.

---

## 7. Slowly Changing Dimensions (SCD)

**SCD** is used to handle changes in dimension data while deciding whether old values should be kept as history or replaced.

### Replace the Old Value

The old value is replaced by the new value, so the previous value is not preserved.

```text
Before:
Employee | Address
1        | Alexandria

After:
Employee | Address
1        | Cairo
```

### Keep the History

A new row is created when the value changes, while the old row is kept.

```text
Employee | Address
1        | Alexandria
1        | Cairo
```

This allows the history of changes to be maintained.

---

## Data Warehouse Flow

```text
Source
  ↓
Staging
  ↓
Bronze
  ↓
Silver
  ↓
Gold
  ↓
Analysis
```

## Key Takeaways

* ETL moves and transforms data from different sources.
* Staging prepares incoming data.
* Bronze keeps relatively raw and historical data.
* Silver contains cleaned and transformed data.
* Gold contains the final analytical data model.
* Loading can be Truncate & Load, Incremental, or Full.
* SCD manages changes in dimension data and historical values.
