# Creating Bars

We create 1-minute bars (bucket_interval=60 seconds) below.

```python
import onetick.py as otp

trd = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')

trd = trd.character_present(trd['COND'], 'O6TUHILNRWZ47QMBCGPV', discard_on_match=True)

bars = trd.agg({'VOLUME': otp.agg.sum('SIZE'),
                'HIGH': otp.agg.max('PRICE'),
                'LOW': otp.agg.min('PRICE'),
                'OPEN': otp.agg.first('PRICE'),
                'COUNT': otp.agg.count(),
                'CLOSE': otp.agg.last('PRICE')},
                bucket_interval=otp.Minute(1))

otp.run(
    bars,
    symbols=['AAPL'],
    start=otp.dt(2024, 2, 1, 9, 30),
    end=otp.dt(2024, 2, 1, 10),
    timezone='EST5EDT'
)
