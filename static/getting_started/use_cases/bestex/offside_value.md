# Offside value

Offside value is a measure of the impact of an aggressive order. It is the distance in notional units that the impacted side moved from the best price prevailing at the time the order arrived.
The formula to get offside value

```
Offside_Value := Executed_QTY * (VWAP - FT) * Direction
```

To calculate the offside value for orders, you need to determine the executed quantity (sum of QTY_FILLED), the VWAP, the Far Touch (FT), and the direction of each order. Here’s how you can do it using `onetick.py`:

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

# Aggregate to carry forward arrival ask and bid prices, along with VWAP, 'SIDE' field, and sum of 'QTY_FILLED'
orders_agg = merged_orders.agg({
    'ARRIVAL_ASK_PRICE': otp.agg.first('ASK_PRICE'),
