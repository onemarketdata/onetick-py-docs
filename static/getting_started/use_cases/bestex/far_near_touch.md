# FT (far touch) and NT (near touch)

To find the Near Touch (NT) and Far Touch (FT) prices for every order, considering the definitions for buy and sell orders, you’ll need to process the order data to determine the arrival bid and ask prices, and then calculate NT and FT based on the side of the order. Here’s how you can do it using `onetick.py`

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
