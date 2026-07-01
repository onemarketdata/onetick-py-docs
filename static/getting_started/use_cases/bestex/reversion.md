# Reversion

Rev – reversion, same as market impact but computed relative to the price at the end of order execution. Helps evaluate if order execution created an impact on the market that then disappeared (the market “reverted”). Large positive values imply a strong reversion.

Formula for reversion in basis points

```
Rev_bps := Direction * (Exit_Mid_Price - <RefPointAfterExit>_Mid_Price) * 10000 / Exit_Mid_Price
```

Example in `onetick.py`:

```python
import onetick.py as otp

# Define your symbols, orders, and quotes database
symbol = 'TSLA'
orders_db = 'ORDERS_DB'
quotes_db = 'US_COMP_SAMPLE'
date = otp.dt(2024, 2, 1)

# Load orders and quotes data
orders = otp.DataSource(orders_db, tick_type='ORDER', symbol=symbol)
quotes = otp.DataSource(quotes_db, tick_type='QTE', symbol=symbol)

# Add mid-price for every quote
quotes['MID_PRICE'] = (quotes['ASK_PRICE'] + quotes['BID_PRICE']) / 2
quotes = quotes[['MID_PRICE']]

# Points at with offsets after order execution
post_exec_markouts = [10, 30, 60]

# Prepare quotes by markout
qte_by_markout_post_exec = []
for m in post_exec_markouts:
    qte_shifted = quotes.deepcopy()
    qte_shifted = qte_shifted.rename({'MID_PRICE': f'MID_PRICE_{m}_post_exec'})
    qte_shifted = qte_shifted.time_interval_shift(m * 1000)
    qte_by_markout_post_exec.append(qte_shifted)

# Join orders with original and shifted quotes
joined_orders_with_quotes = otp.join_by_time([orders] + [quotes] + qte_by_markout_post_exec)

# Roll up order to calculate Executed_QTY, Exit_Mid_Price, and Direction
# Propagate MID_PRICE at each markout post-execution
agg_fields = {
    'EXIT_MID_PRICE': otp.agg.last('MID_PRICE'),
