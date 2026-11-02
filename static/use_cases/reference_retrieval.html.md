# Reference Retrieval

This section contains 5 examples for Reference Retrieval using the `onetick-py`.<br />
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

## Full Stat Record

Retrieve the Static Records from the `LSE_SAMPLE` database for `VOD`, across the specified time range.

```
import onetick.py as otp

data = otp.DataSource(db='LSE_SAMPLE', tick_type='STAT')
result = otp.run(data,
                 start=otp.dt(2024, 1, 3),
                 end=otp.dt(2024, 1, 4),
                 timezone='Europe/London',
                 symbols='VOD')
result
```

## Futures Holiday Calendar

Retrieve the Holiday Calendar from the `OQD_MKTCAL` database, for Futures product `CL` (Crude Oil).

```
import onetick.py as otp

data = otp.DataSource(db='OQD_MKTCAL', tick_type='MKTCAL')
data = data.where(data['ACTIVITY_NAME'].str.like('%HOLIDAY%'))
result = otp.run(data,
                 start=otp.dt(2023, 1, 3),
                 end=otp.dt(2024, 1, 4),
                 timezone='UTC',
                 symbols='TDI_F_CL')
result
```

## Futures Trading Hours

Retrieve the Standard Trading Hours from the `OQD_MKTCAL` database, for Futures product `CL` (Crude Oil).

```
import onetick.py as otp

data = otp.DataSource(db='OQD_MKTCAL', tick_type='MKTCAL')
_, data = data[data['ACTIVITY_NAME'].str.like('%HOLIDAY%')]
result = otp.run(data,
                 start=otp.dt(1990, 1, 3),
                 end=otp.dt(2024, 1, 4),
                 timezone='UTC',
                 symbols='TDI_F_CL')
result
```

## Market Holiday Calendar

Retrieve the Holiday Calendar from the `OQD_MKTCAL` database, for Database `LSE`.

```
import onetick.py as otp

data = otp.DataSource(db='OQD_MKTCAL', tick_type='MKTCAL')
data = data.where(data['ACTIVITY_NAME'].str.like('%HOLIDAY%'))
result = otp.run(data,
                 start=otp.dt(2023, 1, 3),
                 end=otp.dt(2024, 1, 4),
                 timezone='UTC',
                 symbols='CLOUD_DB_LSE')
result
```

## Market Trading Hours

Retrieve the Standard Trading Hours from the `OQD_MKTCAL` database, for Database `LSE`.

```
import onetick.py as otp

data = otp.DataSource(db='OQD_MKTCAL', tick_type='MKTCAL')
_, data = data[data['ACTIVITY_NAME'].str.like('%HOLIDAY%')]
result = otp.run(data,
                 start=otp.dt(1990, 1, 3),
                 end=otp.dt(2024, 1, 4),
                 timezone='UTC',
                 symbols='CLOUD_DB_LSE')
result
```
