# Data notes (Day 1)

## Source
Olist Brazilian E-Commerce dataset (Kaggle, olistbr)

## Row counts in raw files (before cleaning)
- orders: ____
- order_items: ____
- products: ____
- customers: ____
- reviews: ____

## Row counts after Power Query
- Orders: ____
- OrderItems: ____
- (and so on)

## Observations
- Orders with missing delivery dates: ____
- Order statuses found: ____
- Anything unusual: ____


# Day 2 notes

## Design decisions
- Grain of Fact_Orders: one row per order item (orders with no items kept via left join)
- Order Row flag: 1 row per order, used for order-level KPIs to avoid double counting
- Net Revenue excludes canceled and unavailable orders; Revenue is gross as booked
- Is Late compares dates (not timestamps) because estimated dates have no time component
- Currency: Brazilian real (R$)

## Reconciliation results
- Orders rows: ____
- OrderItems rows: ____
- Orders with no items: ____
- Fact_Orders rows: ____
- Distinct orders in Fact_Orders: ____
- OrderItems price total: ____
- Fact_Orders Revenue total: ____
- All three checks passed: yes / no