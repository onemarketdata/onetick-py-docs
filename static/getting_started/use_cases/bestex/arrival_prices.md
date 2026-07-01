# Arrival ask / bid / mid prices for an order

To find the arrival mid-price (which is the average of the ask and bid prices at the time of order arrival) for every order, you need to join the order data with the quote data at the time when each order was initially placed. In trading, the “arrival” of an order typically refers to the time when the order is first submitted, usually indicated by an order state of ‘N’ (New).

```python
import onetick.py as otp

# Define the symbol, orders database, quotes database, and date
symbol = 'TSLA'
orders_db = 'ORDERS_DB'
quotes_db = 'US_COMP_SAMPLE'
