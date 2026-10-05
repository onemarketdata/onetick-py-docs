# Data Retrieval with Symbology

This section contains 5 examples for Data Retrieval with Symbology using the `onetick-py`.<br />
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

## Tick Retrieval with Bloomberg Symbol

Retrieve Trades specifying the Bloomberg symbol, by prefixing the symbol with `BSYM::::`.

```
import onetick.py as otp

data = otp.DataSource(db='US_COMP_SAMPLE', tick_type='TRD')
# Return first 100 Rows
data = data.limit(100)
result = otp.run(data,
                 start=otp.dt(2024, 1, 3, 9, 30),
                 end=otp.dt(2024, 1, 3, 9, 40),
                 timezone='America/New_York',
                 symbols='BSYM::::CSCO US Equity',
                 symbol_date=otp.dt(2024, 1, 3))
result
```

## Tick Retrieval with CUSIP

Retrieve Trades specifying the CUSIP, by prefixing the symbol with `CUS::::`.

```
import onetick.py as otp

data = otp.DataSource(db='US_COMP_SAMPLE', tick_type='TRD')
# Return first 100 Rows
data = data.limit(100)
result = otp.run(data,
                 start=otp.dt(2024, 1, 3, 9, 30),
                 end=otp.dt(2024, 1, 3, 9, 40),
                 timezone='America/New_York',
                 symbols='CUS::::17275R102',
                 symbol_date=otp.dt(2024, 1, 3))
result
```

## Tick Retrieval with FIGI Composite Symbol

Retrieve Trades specifying the Composite FIGI, by prefixing the symbol with `FGC::::`.

```
import onetick.py as otp

data = otp.DataSource(db='US_COMP_SAMPLE', tick_type='TRD')
# Return first 100 Rows
data = data.limit(100)
result = otp.run(data,
                 start=otp.dt(2024, 1, 3, 9, 30),
                 end=otp.dt(2024, 1, 3, 9, 40),
                 timezone='America/New_York',
                 symbols='FGC::::BBG000C3J3C9',
                 symbol_date=otp.dt(2024, 1, 3))
result
```

## Tick Retrieval with ISIN

Retrieve Trades specifying the ISIN, by prefixing the symbol with `ISN::::`.

```
import onetick.py as otp

data = otp.DataSource(db='US_COMP_SAMPLE', tick_type='TRD')
# Return first 100 Rows
data = data.limit(100)
result = otp.run(data,
                 start=otp.dt(2024, 1, 3, 9, 30),
                 end=otp.dt(2024, 1, 3, 9, 40),
                 timezone='America/New_York',
                 symbols='ISN::::US17275R1023',
                 symbol_date=otp.dt(2024, 1, 3))
result
```

## Tick Retrieval with SEDOL

Retrieve Trades specifying the SEDOL, by prefixing the symbol with `SED::::`.

```
import onetick.py as otp

data = otp.DataSource(db='LSE_SAMPLE', tick_type='TRD')
result = otp.run(data,
                 start=otp.dt(2024, 1, 3, 8, 0),
                 end=otp.dt(2024, 1, 3, 9, 0),
                 timezone='Europe/London',
                 symbols='SED::::BH4HKS3',
                 symbol_date=otp.dt(2024, 1, 3))
result
```
