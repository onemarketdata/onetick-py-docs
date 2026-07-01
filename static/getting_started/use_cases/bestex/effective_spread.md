# Effective spread

To calculate the effective spread of your orders, you’ll need to first calculate the Volume Weighted Average Price (VWAP) for each order and determine the prevailing mid-price (average of bid and ask prices) at the time of each order execution. Then, you can use the formula for the effective

```
Effective_Spread := Executed_QTY x (VWAP - Mid_Price) x 2 x Direction
```

Here’s a full code example to calculate the effective spread using `onetick.py`:

```python
import onetick.py as otp

# Define your symbol, orders database, and quotes database
symbol = 'TSLA'
orders_db = 'ORDERS_DB'
quotes_db = 'US_COMP_SAMPLE'
date = otp.dt(2024, 2, 1)

# Load orders and quotes data
orders = otp.DataSource(orders_db, tick_type='ORDER', symbol=symbol)
quotes = otp.DataSource(quotes_db, tick_type='QTE', symbol=symbol)

# Join orders with quotes based on timestamp
joined_data = otp.join_by_time([orders, quotes])

