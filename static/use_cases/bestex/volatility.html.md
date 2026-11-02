# Volatility

Each example is a self-contained script that can be run against the OneTick Cloud sample databases.

```
# onetick-py WebAPI configuration for OneTick Cloud
import os
os.environ['OTP_WEBAPI'] = '1'
os.environ['OTP_HTTP_ADDRESS'] = 'https://rest.cloud.onetick.com'
os.environ['OTP_ACCESS_TOKEN_URL'] = 'https://cloud-auth.parent.onetick.com/realms/OMD/protocol/openid-connect/token'
os.environ['OTP_CLIENT_ID'] = '__FILL_IN__'
os.environ['OTP_CLIENT_SECRET'] = '__FILL_IN__'
```

A simple realized volatility proxy for an instrument over the interval,
computed as the standard deviation of trade prices divided by their average, in percent.

```
VOLATILITY = STDDEV(PRICE) / AVERAGE(PRICE) * 100
```

```
import onetick.py as otp

data = otp.DataSource(db='LSE_SAMPLE', tick_type='TRD')
data = data[['PRICE']]

data = data.agg({
    'STDDEV_PRICE': otp.agg.stddev('PRICE'),
    'AVERAGE_PRICE': otp.agg.average('PRICE'),
})
data['VOLATILITY'] = data['STDDEV_PRICE'] / data['AVERAGE_PRICE'] * 100

result = otp.run(data,
                 start=otp.dt(2024, 1, 3, 8, 0),
                 end=otp.dt(2024, 1, 3, 16, 30),
                 timezone='Europe/London',
                 symbols='VOD')
result
```
