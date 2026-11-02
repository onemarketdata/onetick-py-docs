# Data Retrieval - Book Depth

This section contains 11 examples for Data Retrieval - Book Depth using the `onetick-py`.<br />
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

## Book Depth at Quantity

Calculate Book Depth Metrics such as Bid and Ask VWAP to trade 1000 shares every 60 seconds.

```
import onetick.py as otp

data = otp.DataSource(db='LSE_SAMPLE', tick_type='PRL_FULL')
data = data.ob_summary(bucket_interval=60, max_depth_shares=1000)
result = otp.run(data,
                 start=otp.dt(2024, 1, 3, 8),
                 end=otp.dt(2024, 1, 3, 16),
                 timezone='Europe/London',
                 symbols='VOD')
result
```

## Book Depth at Time

Retrieving the Book to MBL (Market by Level) at a specified time.<br />
\\\\
`PRL_FULL` indicates that the table is actually a MBO (Market by Order) data set.

```
import onetick.py as otp

data = otp.DataSource(db='LSE_SAMPLE', tick_type='PRL_FULL')
data = data.ob_snapshot()
result = otp.run(data,
                 start=otp.dt(2024, 1, 3, 12),
                 end=otp.dt(2024, 1, 3, 12),
                 timezone='Europe/London',
                 symbols='VOD')
result
```

## Book Depth at Time to Max Levels

Retrieving the Book to MBO (Market by Order) at a specified time.<br />
\\\\
The returned book is limited to a maximum number of price levels.

```
import onetick.py as otp

data = otp.DataSource(db='LSE_SAMPLE', tick_type='PRL_FULL')
data = data.ob_snapshot(max_levels=5)
result = otp.run(data,
                 start=otp.dt(2024, 1, 3, 12),
                 end=otp.dt(2024, 1, 3, 12),
                 timezone='Europe/London',
                 symbols='VOD')
result
```

## Book Depth at Time to Max Price Skew

Retrieving the Book to MBO (Market by Order) at a specified time.<br />
\\\\
The returned book is limited to a maximum price skew `0.005 = 0.5%`.

```
import onetick.py as otp

data = otp.DataSource(db='LSE_SAMPLE', tick_type='PRL_FULL')
data = data.ob_snapshot(max_depth_for_price=0.005)
result = otp.run(data,
                 start=otp.dt(2024, 1, 3, 12),
                 end=otp.dt(2024, 1, 3, 12),
                 timezone='Europe/London',
                 symbols='VOD')
result
```

## Book Depth at Time to Max Shares

Retrieving the Book to MBO (Market by Order) at a specified time.<br />
\\\\
The returned book is limited to a maximum amount of accumulated size.

```
import onetick.py as otp

data = otp.DataSource(db='LSE_SAMPLE', tick_type='PRL_FULL')
data = data.ob_snapshot(max_depth_shares=10000)
result = otp.run(data,
                 start=otp.dt(2024, 1, 3, 12),
                 end=otp.dt(2024, 1, 3, 12),
                 timezone='Europe/London',
                 symbols='VOD')
result
```

## Book Depth at Time to Max Spread

Retrieving the Book to MBO (Market by Order) at a specified time.<br />
\\\\
The returned book is limited to a maximum absolute spread.

```
import onetick.py as otp

data = otp.DataSource(db='LSE_SAMPLE', tick_type='PRL_FULL')
data = data.ob_snapshot(max_spread=1)
result = otp.run(data,
                 start=otp.dt(2024, 1, 3, 12),
                 end=otp.dt(2024, 1, 3, 12),
                 timezone='Europe/London',
                 symbols='VOD')
result
```

## Book Depth to MBO at Time

Retrieving the Book to MBO (Market by Order) at a specified time.<br />
\\\\
Using parameter `show_full_detail=True`.

```
import onetick.py as otp

data = otp.DataSource(db='LSE_SAMPLE', tick_type='PRL_FULL')
data = data.ob_snapshot(show_full_detail=True)
result = otp.run(data,
                 start=otp.dt(2024, 1, 3, 12),
                 end=otp.dt(2024, 1, 3, 12),
                 timezone='Europe/London',
                 symbols='VOD')
result
```

## Order Book Bars

Calculate 1 minute bars for book depth down to 5 levels from the `LSE_SAMPLE` database, and `PRL_FULL` table.<br />
\\\\
Each output row showing a Book Level, Side and Time (Bid and Ask on different rows).

```
import onetick.py as otp

data = otp.DataSource(db='LSE_SAMPLE', tick_type='PRL_FULL')
data = data.ob_snapshot(bucket_interval=60, max_levels=5)
# Return first 100 Rows
data = data.limit(100)
result = otp.run(data,
                 start=otp.dt(2024, 1, 3, 8),
                 end=otp.dt(2024, 1, 3, 16),
                 timezone='Europe/London',
                 symbols='VOD')
result
```

## Order Book Flat Bars

Calculate 1 minute bars for book depth down to 5 levels from the `LSE_SAMPLE` database, and `PRL_FULL` table.<br />
\\\\
Each output row showing the book at a specific time (many output columns for bids and asks at selected levels).

```
import onetick.py as otp

data = otp.DataSource(db='LSE_SAMPLE', tick_type='PRL_FULL')
data = data.ob_snapshot_flat(bucket_interval=60, max_levels=5)
result = otp.run(data,
                 start=otp.dt(2024, 1, 3, 8),
                 end=otp.dt(2024, 1, 3, 16),
                 timezone='Europe/London',
                 symbols='VOD')
result
```

## Order Book Updates

Retrieve the changes in the Book across time.

```
import onetick.py as otp

data = otp.DataSource(db='LSE_SAMPLE', tick_type='PRL_FULL')
data = data.ob_snapshot(running=True, show_only_changes=True)
# Return first 100 Rows
data = data.limit(100)
result = otp.run(data,
                 start=otp.dt(2024, 1, 3, 8),
                 end=otp.dt(2024, 1, 3, 9),
                 timezone='Europe/London',
                 symbols='VOD')
result
```

## Order Book Wide Bars

Calculate 1 minute bars for book depth down to 5 levels from the `LSE_SAMPLE` database, and `PRL_FULL` table.<br />
\\\\
Each output row showing a Book Level and Time (Bid and Ask on same row).

```
import onetick.py as otp

data = otp.DataSource(db='LSE_SAMPLE', tick_type='PRL_FULL')
data = data.ob_snapshot_wide(bucket_interval=60, max_levels=5)
# Return first 100 Rows
data = data.limit(100)
result = otp.run(data,
                 start=otp.dt(2024, 1, 3, 8),
                 end=otp.dt(2024, 1, 3, 16),
                 timezone='Europe/London',
                 symbols='VOD')
result
```
