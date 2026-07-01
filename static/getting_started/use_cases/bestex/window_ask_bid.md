# Window ask and window bid

To find the windowed ask and bid prices for every order tick, where the window is defined as window_before seconds before an order and window_after seconds after an order, you can use the ``join_with_query`` method in `onetick.py`. This method allows you to join two data sources based on a time window.

Here’s a full code example that implements the function get_window_ask_bid to achieve this:

```python
import onetick.py as otp

# Define your symbols, orders, and quotes database
symbol = 'TSLA'
orders_db = 'ORDERS_DB'
quotes_db = 'US_COMP_SAMPLE'
date = otp.dt(2024, 2, 1)

# Define the time window parameters
window_before = 5.0  # seconds before the order
window_after = 7.0   # seconds after the order

# Load orders and quotes data
orders = otp.DataSource(orders_db, tick_type='ORDER', symbol=symbol)
quotes = otp.DataSource(quotes_db, tick_type='QTE', symbol=symbol)
