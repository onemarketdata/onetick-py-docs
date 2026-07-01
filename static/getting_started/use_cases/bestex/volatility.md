# Volatility

To calculate the volatility of a financial instrument using `onetick.py`, you’ll need to retrieve trade data (typically with the ‘TRD’ tick type) from the US_COMP_SAMPLE database and then apply your defined function to calculate the volatility. The volatility is computed as the standard deviation of the trade prices divided by their average, multiplied by 100 (to get a percentage).

```python
import onetick.py as otp

# Define your symbol and the database
