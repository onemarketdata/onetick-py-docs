# Corrections and Time Travel

This section contains 5 examples for Corrections and Time Travel using the `onetick-py`.<br />
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

## Corrected Trade Retrieval

Standard Trade Retrieval returns data adjusted for Trade Corrections.<br />
\\\\
Deleted Trades will not be visible.

```
import onetick.py as otp

data = otp.DataSource(db='LSE_SAMPLE', tick_type='TRD')
data = data[['TRADE_ID', 'PRICE', 'SIZE', 'TRADE_TYPE', 'TRADE_VENUE', 'TICK_STATUS', 'DELETED_TIME']]
data = data.limit(10)
result = otp.run(data,
                 start=otp.dt(2024, 1, 4, 11, 4, 0),
                 end=otp.dt(2024, 1, 6),
                 timezone='UTC',
                 symbols='VOD')
result
```

## Hidden Records Including Corrections

All Records including trade corrections can be retrieved by using ``show_hidden_ticks()``.<br />
\\\\
This propagates all ticks, even those with a `TICK_STATUS` not equal to 0, which are normally hidden.<br />
\\\\
Corrected Trades can be identified by their `DELETED_TIME` and `TICK_STATUS` fields.<br />
\\\\
`DELETED_TIME` corresponds to the time the record was corrected, which may be days after the original record.<br />
\\\\
`TICK_STATUS` refers to the type of change:

* 0 - Default
* 1 - Deleted record
* 2 - Updated record
* 3 - Insert Corrected
* 4 - Record that has been Canceled
* 5 - Record that has been Corrected
* 6 - New Correction record
* 7 - New Cancellation record

```
import onetick.py as otp

data = otp.DataSource(db='LSE_SAMPLE', tick_type='TRD')
data = data.show_hidden_ticks()
data = data[['TRADE_ID', 'PRICE', 'SIZE', 'TRADE_TYPE', 'TRADE_VENUE', 'TICK_STATUS', 'DELETED_TIME']]
data = data.limit(10)
result = otp.run(data,
                 start=otp.dt(2024, 1, 4, 11, 4, 0),
                 end=otp.dt(2024, 1, 6),
                 timezone='UTC',
                 symbols='VOD')
result
```

## Trade Corrections

Trade corrections can be retrieved by using ``show_corrected_ticks()``.<br />
\\\\
Only corrected and correction ticks will be propagated.<br />
\\\\
Corrected Trades can be identified by their `DELETED_TIME` and `TICK_STATUS` fields.<br />
\\\\
`DELETED_TIME` corresponds to the time the record was corrected, which may be days after the original record.<br />
\\\\
`TICK_STATUS` refers to the type of change, in the example below:

* 4 - Record that has been Canceled
* 7 - New Cancellation record

```
import onetick.py as otp

data = otp.DataSource(db='LSE_SAMPLE', tick_type='TRD')
data = data.show_corrected_ticks()
data = data[['TRADE_ID', 'PRICE', 'SIZE', 'TRADE_TYPE', 'TRADE_VENUE', 'TICK_STATUS', 'DELETED_TIME']]
data = data.limit(10)
result = otp.run(data,
                 start=otp.dt(2024, 1, 4, 11, 4, 0),
                 end=otp.dt(2024, 1, 6),
                 timezone='UTC',
                 symbols='VOD')
result
```

## Trades Before Correction

Trade data can be retrieved as it was at a specific point in time using ``correct_tick_filter()``.

* If the specified `as_of_time` is set before the trade corrections, uncorrected data is returned.
* If the specified `as_of_time` is set after the trade corrections, corrected data is returned.

This provides a Time Travel capability, returning data before and after changes to the data occur.<br />
\\\\
Here the `as_of_time` is set to a date before the trade corrections, so uncorrected data is returned.

```
import onetick.py as otp

data = otp.DataSource(db='LSE_SAMPLE', tick_type='TRD')
data = data.correct_tick_filter(discard_on_match=False, as_of_time=otp.dt(2024, 1, 4))
data = data[['TRADE_ID', 'PRICE', 'SIZE', 'TRADE_TYPE', 'TRADE_VENUE', 'TICK_STATUS', 'DELETED_TIME']]
data = data.limit(10)
result = otp.run(data,
                 start=otp.dt(2024, 1, 4, 11, 4, 0),
                 end=otp.dt(2024, 1, 6),
                 timezone='UTC',
                 symbols='VOD')
result
```

## Trades After Correction

Trade data can be retrieved as it was at a specific point in time using ``correct_tick_filter()``.

* If the specified `as_of_time` is set before the trade corrections, uncorrected data is returned.
* If the specified `as_of_time` is set after the trade corrections, corrected data is returned.

This provides a Time Travel capability, returning data before and after changes to the data occur.<br />
\\\\
Here the `as_of_time` is set to a date after the trade corrections, so corrected data is returned.

```
import onetick.py as otp

data = otp.DataSource(db='LSE_SAMPLE', tick_type='TRD')
data = data.correct_tick_filter(discard_on_match=False, as_of_time=otp.dt(2024, 1, 6))
data = data[['TRADE_ID', 'PRICE', 'SIZE', 'TRADE_TYPE', 'TRADE_VENUE', 'TICK_STATUS', 'DELETED_TIME']]
data = data.limit(10)
result = otp.run(data,
                 start=otp.dt(2024, 1, 4, 11, 4, 0),
                 end=otp.dt(2024, 1, 6),
                 timezone='UTC',
                 symbols='VOD')
result
```
