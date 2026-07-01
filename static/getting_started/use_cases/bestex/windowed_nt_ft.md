# Windowed FT (far touch) and Windowed NT (far touch)

To calculate the Windowed Near Touch (Window_NT) and Windowed Far Touch (Window_FT) prices for every order, considering the side of the order (buy or sell) and using the windowed bid and ask prices, you need to first determine these windowed prices and then apply the logic based on the order side. Here’s how you can do it using `onetick.py`:

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

def get_window_ask_bid(orders: otp.Source, quotes: otp.Source, window_before: float, window_after: float) -> otp.Source:
    # Aggregate ask and bid prices
    quotes_agg = quotes.agg({'WINDOW_ASK': otp.agg.max('ASK_PRICE'),
                             'WINDOW_BID': otp.agg.min('BID_PRICE')})

    # Define the start and end of the window
