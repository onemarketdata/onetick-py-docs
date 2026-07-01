# Participation weighted price (PWP)

The PWP is calculated as the market VWAP of trades starting from the order arrival time up to the trade that reaches the cumulative volume of y/x, where y is the order quantity and x is the participation percentage. Here’s how it’s done:

```python
import onetick.py as otp

# Define your symbols, orders database, and date
symbol = 'TSLA'
orders_db = 'ORDERS_DB'
trades_db = 'US_COMP_SAMPLE'
date = otp.dt(2024, 2, 1)

# Participation ratios
ratios = [0.01, 0.03, 0.07]

def pwp_query(volume):
    """ Function to find necessary VWAP based on the qty of the order."""
    # Get trades from the specified trades database
    trades = otp.DataSource(db=trades_db, tick_type='TRD')
    trades = trades.table(**{'PRICE': float, 'SIZE': int})

    # Aggregate trades to get VWAP using running aggregation
    trades = trades.agg({'VWAP': otp.agg.vwap(price_column='PRICE', size_column='SIZE'),
                         'VOLUME': otp.agg.sum('SIZE')},
                        running=True,
                        all_fields=True)

    # Calculate PWP for each ratio
    for ratio in ratios:
        state_name = str(ratio).replace('.', '')
        trades.state_vars[state_name] = otp.state.var(otp.nan, scope='all_outputs')

        trades = trades.update({
                trades.state_vars[state_name]: trades['VWAP'],
            }, where=(trades['VOLUME'] <= volume / ratio))

    # Get the last trade to save results from state variables
    res = trades.last(keep_timestamp=False)
    to_output = []
    for ratio in ratios:
        pwp_name = 'PWP_' + str(ratio).replace('.', '_')
        state_name = str(ratio).replace('.', '')

        # Put values from state variables into resulting tick
        res[pwp_name] = res.state_vars[state_name]
        to_output.append(pwp_name)

