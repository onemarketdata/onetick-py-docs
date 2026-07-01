# Opportunity cost

OC – opportunity cost.

Formula for it:

```
OC := Direction * Unexecuted_QTY * (Arrival_Mid_Price - Exit_Mid_Price)
```

To calculate the Opportunity Cost (OC) for orders, we need to determine the direction of each order, the unexecuted quantity (Unexecuted_QTY), the arrival mid-price (Arrival_Mid_Price), and the exit mid-price (Exit_Mid_Price). The OC is then calculated using the provided formula. Here’s how you can do it using `onetick.py`:

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

# Add mid-price for every quote
quotes['MID_PRICE'] = (quotes['ASK_PRICE'] + quotes['BID_PRICE']) / 2

# Join quotes to orders without any filtration
joined_data = otp.join_by_time([orders, quotes])
