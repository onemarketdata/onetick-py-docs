# Data Retrieval - Bars

This section contains 3 examples for Data Retrieval - Bars using the `onetick-py`.<br />
\\\\
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

## Daily Trade Bars

Retrieve Daily OHLC Records from the `US_COMP_SAMPLE_DAILY` database, and `DAY` table.

```
import onetick.py as otp

data = otp.DataSource(db='US_COMP_SAMPLE_DAILY', tick_type='DAY')
result = otp.run(data,
                 start=otp.dt(2024, 1, 1),
                 end=otp.dt(2024, 2, 1),
                 timezone='America/New_York',
                 symbols='CSCO')
result
```

## Minute Trade Bars

Retrieve pre-calculated 1 minute Trade Bars from the `US_COMP_SAMPLE_BARS` database, and `TRD_1M` table.<br />
\\\\
Bars are calculated at the end of each minute, so setting time range from 09:31 to 16:01.

```
import onetick.py as otp

data = otp.DataSource(db='US_COMP_SAMPLE_BARS', tick_type='TRD_1M')
result = otp.run(data,
                 start=otp.dt(2024, 1, 3, 9, 31),
                 end=otp.dt(2024, 1, 3, 16, 1),
                 timezone='America/New_York',
                 symbols='CSCO')
result
```

## Minute Quote Bars

Retrieve pre-calculated 1 minute Quote Bars from the `US_COMP_SAMPLE_BARS` database, and `QTE_1M` table.
Bars are calculated at the end of each minute, so setting time range from 09:31 to 16:01.

```
import onetick.py as otp

data = otp.DataSource(db='US_COMP_SAMPLE_BARS', tick_type='QTE_1M')
result = otp.run(data,
                 start=otp.dt(2024, 1, 3, 9, 31),
                 end=otp.dt(2024, 1, 3, 16, 1),
                 timezone='America/New_York',
                 symbols='CSCO')
result
```
