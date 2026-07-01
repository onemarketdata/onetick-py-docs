# Interval Metrics (e.g., VWAP)

```python
import onetick.py as otp

query = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')
query = query.agg({'market_vwap': otp.agg.vwap('PRICE', 'SIZE')})

otp.run(
    query,
    symbols=['AAPL'],
    start=otp.dt(2024, 2, 1, 9, 30),
    end=otp.dt(2024, 2, 1, 9, 30, 1),
    timezone='EST5EDT',
)
```

## Computing market VWAP for every order’s arrival/exit interval

