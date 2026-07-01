# Notional spread (quoted spread)

To calculate the notional spread for every client’s order in onetick.py, you first need to determine the Arrival_Ask_Price and Arrival_Bid_Price for each order at its arrival time, then calculate the notional spread using the formula:

```
Notional_Spread := Order_Executed_Qty * (Arrival_Ask_Price - Arrival_Bid_Price)
```

Example of code in `onetick.py`:

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

