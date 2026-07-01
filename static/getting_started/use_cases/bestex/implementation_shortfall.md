# Implementation shortfall (slippage)

IS – implementation shortfall, or slippage.  Large positive values imply a good execution while large negative values imply a poor execution.

```
IS := Direction * Executed_QTY * (Arrival_Mid_Price - VWAP)
```

To calculate the Implementation Shortfall (IS) for each order, we need to determine the direction of the order, the executed quantity (sum of QTY_FILLED), the arrival mid-price, and the Volume Weighted Average Price (VWAP) of the order. We will then apply the provided formula to calculate the IS. Here’s how you can do it using `onetick.py`:

```python
import onetick.py as otp

# Define the symbol, orders database, quotes database, and date
symbol = 'TSLA'
orders_db = 'ORDERS_DB'
quotes_db = 'US_COMP_SAMPLE'
date = otp.dt(2024, 2, 1)

# Load orders and quotes data
orders = otp.DataSource(orders_db, tick_type='ORDER', symbol=symbol)
quotes = otp.DataSource(quotes_db, tick_type='QTE', symbol=symbol)

# Filter for new (arrival) orders
arrival_orders, other_orders = orders[(orders['STATE'] == 'N')]

# Join arrival orders with quotes based on timestamp
arrival_orders_with_quotes = otp.join_by_time([arrival_orders, quotes])

# Calculate current mid price for each quote tick
arrival_orders_with_quotes['MID_PRICE'] = (arrival_orders_with_quotes['ASK_PRICE'] + arrival_orders_with_quotes['BID_PRICE']) / 2

# Merge all ticks back to apply aggregation properly
merged_orders = arrival_orders_with_quotes + other_orders
