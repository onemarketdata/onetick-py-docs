# Takeout success

Takeout success based on capturing the available size in the market for an order at a certain level takeout success flag:

```
Takeout_Success := SizeFilled >= min(Size, Ask_Size), when Side = 'BUY', and
Takeout_Success := SizeFilled >= min(Size, Bid_Size), otherwise
```

Calculate takeout success for orders and US_COMP_SAMPLE databases using for the `TSLA` ticker in `onetick.py`

```python
import onetick.py as otp

orders = otp.DataSource('ORDERS_DB', tick_type='ORDER')

