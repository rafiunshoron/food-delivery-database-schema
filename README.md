# Food Delivery Database Schema

Entity-relationship design for a food delivery platform (like Foodpanda / Uber Eats) — covers customers, restaurants, menus, orders, coupons, payments, and delivery.

## Workflow

Customer → browses menu → places order → applies coupon → pays → order delivered → leaves review

## Entities

| Table | Description |
|---|---|
| `Customer` | Registered users |
| `Address` | Saved delivery addresses (1 customer : many addresses) |
| `Restaurant` | Partner restaurants |
| `Menu` | A restaurant's menu |
| `Category` | Menu item categories |
| `Menu_Item` | Items available for order |
| `Order` | A placed order |
| `Order_Item` | Order line items (junction: Order ↔ Menu_Item) |
| `Coupon` | Discount codes |
| `Coupon_Usage` | Per-customer coupon usage (junction: Customer ↔ Coupon) |
| `Payment` | Payment for an order |
| `Delivery` | Delivery record for an order |
| `Delivery_Person` | Delivery staff |
| `Review` | Restaurant reviews (junction: Customer ↔ Restaurant) |

## Key decisions

- Money/percentage fields use `decimal`, not `int` (`Total_Amount`, `Price`, `Discount_Percentage`, `Rating`)
- Passwords stored as hashes (`Password_Hash`), never plaintext
- `Address` is one-to-many from `Customer` — multiple saved addresses, `Order.Address_ID` snapshots the one used
- Junction tables: `Order_Item`, `Coupon_Usage`, `Review`

## Files

- `erd.png` — ER diagram
- `schema.sql` — DDL for table creation
