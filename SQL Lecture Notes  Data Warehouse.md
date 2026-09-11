# SQL Lecture Notes : Data Warehouse

| Field         | Value                                                   |
| ------------- | ------------------------------------------------------- |
| Session Date  | 2026-09-05                                              |
| Group Code    | ALX5-DAT3-S1                                            |
| Session Code  | SQL - S002                                              |
| Session Title | Advanced SQL: Data Transformation, ETL & Data Warehouse |
| Note-taker    | Doaa Abdelsattar                                        |

## Main Topics Discussed

* Data Transformation from Different Sources
* ETL (Extract, Transform, Load)
* Data Warehouse (DWH) Layers
* Staging Layer
* Bronze Layer
* Silver Layer
* Gold Layer
* Slowly Changing Dimensions (SCD)
* Data History and Incremental Loading

---

### 1. Data Transformation, ETL & Data Warehouse

The main idea of the lecture is to take data from different sources, perform ETL, and finally store the processed data in a Data Warehouse (DWH).

The data passes through several layers, where each layer has a specific purpose.

---

### 2. Staging Layer

The Staging Layer is a preparation area for incoming data.

* Data is taken from any source and loaded into a new database.
* A SQL table is created with approximately the same structure as the source data.
* In the staging table, data types are usually stored as TEXT/String, even for dates and numbers.
* This helps prevent data type errors while moving data through the pipeline.
* The main goal is to safely receive the raw data before further processing.
* **Loading Strategies in Staging**

When new data arrives every day, we need to decide whether to replace the old data or add the new data.

There are three main approaches:

**1. Truncate & Load**

- Delete all existing data from the table.
- Load the new version of the data.
- The table contains only the latest data.

**Advantage:**

- Simple and easy to manage.

**Disadvantage:**

- No historical data is preserved.

**2. Incremental Loading**

- Add only the new or changed data.
- Existing historical data is kept.

**Advantage:**

- Preserves data history.

**Disadvantage:**

- Requires more storage space over time.

**3. Full Loading**

* Load all the data from the source every time.
* The complete source dataset is loaded into the target table.
* It does not load only the new or changed records.

**Advantage:**

- Simple and ensures that the target contains the complete source data.

**Disadvantage:**

- Requires more processing time and resources, especially with large datasets.

---



### 3. Bronze Layer

The **Bronze Layer** receives data from the  **Staging Layer** .

Main operations:

* Data is taken from Staging.
* **De-duplication** is performed to remove duplicate records.
* Data is loaded using  **Incremental Loading** .
* Historical data is preserved.

The Bronze Layer therefore contains relatively raw data while maintaining its history.

---

### 4. Silver Layer

The **Silver Layer** contains  **cleaned and historical data** .

When moving data from Bronze to Silver, we perform data transformation and cleaning.

Main operations include:

* Changing the **data types** from the raw format to appropriate types.
* Checking for  **missing values** .
* Detecting  **invalid values** .
* Cleaning and transforming the data.
* Preserving historical data.
* Using  **Incremental Loading** .

The Silver Layer contains cleaned and historical data and is ready to be used for building the analytical data model.

---



### 5. Analysis & Data Modeling

For analysis, we usually do not want to work with one large table.

Instead, the goal is to create a Data Model, such as a Star Schema, consisting of multiple related tables.

The cleaned data in the Silver Layer is transformed into a suitable model for analysis.

---

### 6. Gold Layer

The **Gold Layer** contains the final **Data Model** used for analysis.

In this layer:

* Tables are organized according to the required data model.
* Primary Keys ( **PK** ) are defined.
* Relationships between tables are established.
* The final structure can follow a  **Star Schema** .
* The data is prepared for analytical queries and reporting.

---

### 7. Slowly Changing Dimension (SCD)

**Slowly Changing Dimension (SCD)** is used to handle changes in dimension data while deciding whether the old value should be kept as history or replaced.

For example, if an employee's address changes:

#### Option 1 — Replace the old value

* Delete/replace the old value.
* Store the new value in the same row.
* The previous value is not preserved.

Example:

```
Before:
Employee | Address
1        | Alexandria

After:
Employee | Address
1        | Cairo
```

The old address is lost.

#### Option 2 — Keep the history

* Create a new row when the value changes.
* Keep the old row with the old value.
* Add another row containing the new value.

Example:

```
Employee | Address
1        | Alexandria
1        | Cairo
```

This allows us to maintain the history of changes.

---

## Assignments

| Description                                                           | Due Date   | Notes/Link                                                                                          |
| --------------------------------------------------------------------- | ---------- | --------------------------------------------------------------------------------------------------- |
| Practical application of ETL and Data Warehouse concepts on a dataset | 2026-09-05 | Applied the Staging, Bronze, Silver, and Gold layers and practiced data loading and transformation. |

## Questions & Answers

| Question                                                                | Answer (from instructor)                                                                              |
| ----------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| What is the Staging Layer?                                              | A preparation area for data coming from different sources.                                            |
| What is the difference between Truncate & Load and Incremental Loading? | Truncate & Load replaces the old data, while Incremental Loading adds new data and keeps the history. |
| What happens in the Silver Layer?                                       | Data is cleaned, data types are changed, and missing or invalid values are handled.                   |
| What is SCD?                                                            | A way to handle changes in dimension data while keeping or replacing the old values.                  |

## Next Lecture's Agenda

* Continue working with ETL and Data Warehouse concepts.
* Continue Data Modeling and dimensional design.
* Work with historical data and Slowly Changing Dimensions.

## Resources & References

- Lecture notes and examples discussed during the SQL session.

## Miscellaneous

* The main lecture topic was  **Data Transformation from Different Sources, ETL, and Data Warehouse** .
* Focus on understanding the purpose of each DWH layer and the difference between the different loading strategies.
