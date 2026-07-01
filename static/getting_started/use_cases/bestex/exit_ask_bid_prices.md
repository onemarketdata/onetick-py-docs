# Exit ask/bid prices for an order

To find the EXIT_ASK_PRICE and EXIT_BID_PRICE for each order in `onetick.py`, where ‘exit’ means the order was fully executed (`STATE='F'`) or canceled (`STATE='C'`)

```python
import onetick.py as otp

# Define the symbol, orders database, quotes database, and date
symbol = 'TSLA'
orders_db = 'ORDERS_DB'
quotes_db = 'US_COMP_SAMPLE'
