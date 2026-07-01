# Price improvement

Price improvement – distance to the far touch (FT) in bps (basis points). Measures the improvement over the aggressive touch at the time the order is placed. Positive values indicate a good execution, negative - a poor one.
Formula to get price improvement:

```
PriceImprovements_bps := Direction * 10000 * (FT - VWAP) /  (FT)
```

Where the VWAP is order execution VWAP, FT – far touch.

To calculate PriceImprovements_bps for each order, you need to determine the VWAP and Far Touch (FT) for each order and then apply the given formula. The formula measures the price improvement in basis points (bps), considering the order direction.

Here’s the `onetick.py` code:

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

# Merge all ticks back to apply aggregation properly
merged_orders = arrival_orders_with_quotes + other_orders

# Aggregate to carry forward arrival ask and bid prices, along with VWAP and 'SIDE' field
orders_agg = merged_orders.agg({
