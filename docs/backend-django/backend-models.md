---
layout: default
title: Models (Database)
parent: Backend (Django)
nav_order: 1
---
# Backend

## Models (Database)

The information of each quote is stored in five different tables:

- `quote`: The main table storing basic infomation of the quotes.
- `quoteproducts`: The intermediate table storing the products of each quote.
- `contacts`: The table storing the contact information of the customers.
- `products`: The table storing the information of the products.
- `invoices`: The table storing the information of the invoices.

The following sections describe the schema for each table in the database.

### Contacts

The `Contacts` table stores contact information.

| Field     | Type          | Attributes                    |
|:---------:|:-------------:|:-----------------------------:|
| id        | AutoField     | Primary Key, Auto Increment   |
| email     | EmailField    | Max length: 200, Nullable     |
| first_name| CharField     | Max length: 200, Nullable     |
| last_name | CharField     | Max length: 200, Nullable     |
| mid       | CharField     | Max length: 20, Nullable, Unique |
| title     | CharField     | Max length: 10, Nullable     |
| company   | CharField     | Max length: 200, Nullable     |
| country   | CharField     | Max length: 200, Nullable     |

### Products

The `Products` table stores product information.

| Field      | Type          | Attributes                            |
|:----------:|:-------------:|:-------------------------------------:|
| id         | AutoField     | Primary Key, Auto Increment           |
| name       | CharField     | Max length: 200                       |
| cat_num    | CharField     | Max length: 200, Nullable             |
| price_chf  | DecimalField  | Max digits: 10, Decimal places: 2, Nullable |
| price_gbp  | DecimalField  | Max digits: 10, Decimal places: 2, Nullable |
| price_usd  | DecimalField  | Max digits: 10, Decimal places: 2, Nullable |
| price_eur  | DecimalField  | Max digits: 10, Decimal places: 2, Nullable |
| type       | CharField     | Max length: 200                       |
| mid        | CharField     | Max length: 20, Unique                |

### Quotes

The `Quotes` table stores quote information.

| Field           | Type          | Attributes                            |
|:---------------:|:-------------:|:-------------------------------------:|
| id              | AutoField     | Primary Key, Auto Increment           |
| contact         | ForeignKey    | References `Contacts.id`, Nullable    |
| mid             | CharField     | Max length: 20, Unique                |
| quote_id        | CharField     | Max length: 100, Nullable, Unique     |
| date            | DateField     | Auto add current date, Nullable       |
| custom_quote_to | CharField     | Max length: 200, Nullable             |
| validity_period | PositiveIntegerField | Nullable                        |
| deal_type       | CharField     | Max length: 10, Nullable              |
| product         | ManyToManyField | Through `QuoteProduct`, Nullable    |
| currency        | CharField     | Max length: 3, Nullable               |
| discount        | DecimalField  | Max digits: 10, Decimal places: 2, Nullable |
| shipment_cost   | DecimalField  | Max digits: 10, Decimal places: 2, Nullable |
| tax             | DecimalField  | Max digits: 10, Decimal places: 2, Nullable |
| price_total     | DecimalField  | Max digits: 10, Decimal places: 2, Nullable |

### QuoteProduct

The `QuoteProduct` table represents a many-to-many relationship between `Quotes` and `Products`.

| Field      | Type          | Attributes                            |
|:----------:|:-------------:|:-------------------------------------:|
| id         | AutoField     | Primary Key, Auto Increment           |
| quote      | ForeignKey    | References `Quotes.id`, Nullable      |
| quote_mid  | CharField     | Max length: 20, Nullable              |
| product    | ForeignKey    | References `Products.id`, Nullable    |
| product_mid| CharField     | Max length: 20, Nullable              |
| quantity   | PositiveIntegerField | Nullable                        |
| unit_price | DecimalField  | Max digits: 10, Decimal places: 2, Nullable |

### Invoices

The `Invoices` table stores invoice information.

| Field           | Type          | Attributes                            |
|:---------------:|:-------------:|:-------------------------------------:|
| id              | AutoField     | Primary Key, Auto Increment           |
| quote           | ForeignKey    | References `Quotes.id`, Nullable      |
| quote_mid       | CharField     | Max length: 20, Nullable, Unique      |
| quote_num       | CharField     | Max length: 100, Nullable, Unique     |
| invoice_date    | DateField     | Nullable                              |
| po_num          | CharField     | Max length: 100, Nullable             |
| validity_period | PositiveIntegerField | Nullable                        |
| bill_to         | TextField     | Nullable                              |