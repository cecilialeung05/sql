 Part 3 — Customer Address Architectures (Type 1 vs Type 2)
 Option 1: Overwrite (Type 1 Slowly Changing Dimension)

This design keeps only the current address.
Whenever a customer moves, the row is updated and previous values are lost.

CREATE TABLE customer_address (
  customer_id INTEGER PRIMARY KEY,
  street TEXT,
  city TEXT,
  province TEXT,
  postal_code TEXT
);


Pros:

Simple to maintain

Only one row per customer

Cons:

No historical tracking (old addresses are lost)

This is a Type 1 SCD because the old values are overwritten.

 Option 2: Retain History (Type 2 Slowly Changing Dimension)

This design keeps full historical records.
Each address change inserts a new row with start and end dates.

CREATE TABLE customer_address (
  address_id INTEGER PRIMARY KEY,
  customer_id INTEGER,
  street TEXT,
  city TEXT,
  province TEXT,
  postal_code TEXT,
  start_date TEXT,
  end_date TEXT,
  is_current BOOLEAN
);


Pros:

Complete history available

Supports analytics, auditing, customer lifecycle analysis

Cons:

More complex queries and ETL logic required

This is a Type 2 SCD because changes create new records with tracked time ranges.