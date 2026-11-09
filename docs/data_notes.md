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



# Day 3 notes

## Design decisions
- Report date lives in Control!B1 (named range ReportDate); all reports reference it
- Daily KPIs: Net Revenue, Orders placed, Valid orders, AOV, Cancelled orders, Cancellation rate
- Weekly report: 8 rolling 7-day windows ending on the report date (Mon-Sun when the date is a Sunday)
- Order counts use Order Row = 1 so multi-item orders are counted once
- On-time % = on-time orders / delivered orders (undelivered excluded)
- Review score averaged once per order
- Conditional formatting uses ISNUMBER formulas so text dashes are never colored

## Known limitation
- The dataset is a full snapshot, so metrics for a past report date include deliveries
  that happened after that date. A live system would only know deliveries up to the report date.

## Checks
- Daily 7-day check difference: 0
- Weekly 56-day check difference: 0
- Week 8 of Weekly_Report equals Daily_Snapshot 7-day total: yes

## Observations (report date 01-Jul-2018, weeks ending 13-May to 01-Jul)
- Week 1 (7-13 May) peak: R$ 293,731, 1,987 orders (coincides with Mother's Day, 13 May)
- Week 3 (21-27 May): revenue -48.4% WoW, orders 1,837 -> 954 (coincides with the national
  truckers' strike that began 21 May 2018; not verified as the cause)
- Week 2 (14-20 May): lowest on-time delivery at 87.9%; recovers to 98-99% from week 4