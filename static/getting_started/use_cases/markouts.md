# Point-in-time benchmarks: BBO at different markouts

Find the prevailing quote at different time intervals (markouts) before/after each trade.

```python
import onetick.py as otp

markouts = [-1, 0, 1, 5, 60, 600]

trd = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')
trd = trd[['PRICE', 'SIZE']]

qte_by_markout = []
for m in markouts:
    mr = str(m).replace('-', 'm')
