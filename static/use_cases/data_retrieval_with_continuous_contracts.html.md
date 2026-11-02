# Data Retrieval with Continuous Contracts

This section contains 6 examples for Data Retrieval with Continuous Contracts using the `onetick-py`.<br />
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

## DAY Retrieval Cont Contract by Max Open Interest

Retrieve the Front Month Continuous Contract based on Maximum Open Interest.<br />
\\\\
Using Symbol Syntax: `[Product Code]_r_oi`.

```
import onetick.py as otp

data = otp.DataSource(db='ICE_EU_COM_SAMPLE_DAILY', tick_type='DAY')
data = data.where(data['UPDATE_TYPE'] == 'Summary')
result = otp.run(data,
                 start=otp.dt(2024, 1, 1),
                 end=otp.dt(2024, 4, 1),
                 timezone='Europe/London',
                 symbols='BRN_r_oi',
                 symbol_date=otp.dt(2024, 4, 1))
result
```

## DAY Retrieval Cont Contract by Max Volume

Retrieve the Front Month Continuous Contract based on Maximum Volume.<br />
\\\\
Using Symbol Syntax: `[Product Code]_r_vol`.

```
import onetick.py as otp

data = otp.DataSource(db='ICE_EU_COM_SAMPLE_DAILY', tick_type='DAY')
data = data.where(data['UPDATE_TYPE'] == 'Summary')
result = otp.run(data,
                 start=otp.dt(2024, 1, 1),
                 end=otp.dt(2024, 4, 1),
                 timezone='Europe/London',
                 symbols='BRN_r_vol',
                 symbol_date=otp.dt(2024, 4, 1))
result
```

## DAY Retrieval Cont Contract by Max Volume with Bloomberg Symbology

Front Month Continous Contract by Max Volume can be specified with Bloomberg `BSYM` symbology:
`[Bloomberg Product code]A`.<br />
\\\\
For example Brent Crude (exchange symbol `BRN`), has Bloomberg Product code `CO`.<br />
\\\\
Instead of `BRN_r_vol`, `COA Comdty` can be specified.

```
import onetick.py as otp

data = otp.DataSource(db='ICE_EU_COM_SAMPLE_DAILY', tick_type='DAY')
data = data.where(data['UPDATE_TYPE'] == 'Summary')
result = otp.run(data,
                 start=otp.dt(2024, 1, 1),
                 end=otp.dt(2024, 4, 1),
                 timezone='Europe/London',
                 symbols='BSYM::::COA Comdty',
                 symbol_date=otp.dt(2024, 4, 1))
result
```

## ``DAY Retrieval Cont Contract by Month (1-12)``

Front Month to Twelve Month Continuous Contract can be specified
`[Product code]\1` to `[Product code]\12`.<br />
\\\\
Rolls based on contract expiry.

```
import onetick.py as otp

data = otp.DataSource(db='ICE_EU_COM_SAMPLE_DAILY', tick_type='DAY')
data = data.where(data['UPDATE_TYPE'] == 'Summary')
result = otp.run(data,
                 start=otp.dt(2024, 1, 1),
                 end=otp.dt(2024, 4, 1),
                 timezone='Europe/London',
                 symbols='BRN\\1',
                 symbol_date=otp.dt(2024, 4, 1))
result
```

## DAY Retrieval Cont Contract by Tick Data Method

Retrieve the Front Month Continuous Contract based on Tick Data Methology (only relevant for `TDI_FUT`).<br />
\\\\
Using Symbol Syntax: `[Product Code]_r_tdi`.

```
import onetick.py as otp

data = otp.DataSource(db='TDI_FUT_SAMPLE_DAILY', tick_type='DAY')
result = otp.run(data,
                 start=otp.dt(2024, 1, 1),
                 end=otp.dt(2024, 4, 1),
                 timezone='Europe/London',
                 symbols='CO_r_tdi',
                 symbol_date=otp.dt(2024, 4, 1))
result
```

## DAY Retrieval Cont Contract with Bloomberg Symbology

Front Month to Twelve Month Continuous Contract can be specified with Bloomberg `BSYM` symbology
`[Product code]1` to `[Product code]12`.<br />
\\\\
Rolls based on contract expiry.<br />
\\\\
For example Brent Crude (exchange symbol `BRN`), has Bloomberg Product code `CO`.

```
import onetick.py as otp

data = otp.DataSource(db='ICE_EU_COM_SAMPLE_DAILY', tick_type='DAY')
data = data.where(data['UPDATE_TYPE'] == 'Summary')
result = otp.run(data,
                 start=otp.dt(2024, 1, 1),
                 end=otp.dt(2024, 4, 1),
                 timezone='Europe/London',
                 symbols='BSYM::::CO1 Comdty',
                 symbol_date=otp.dt(2024, 4, 1))
result
```
