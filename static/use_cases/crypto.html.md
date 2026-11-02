# Crypto

This section contains 7 examples for Crypto using the `onetick-py`.<br />
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

## Crypto Trade Retrieval

Retrieving Trades from a Crypto Venue.<br />
\\\\
Unlike Equities and Futures, the Trade Size on a crypto venue is fractional.

```
import onetick.py as otp

data = otp.DataSource(db='BINANCE', tick_type='TRD')
data = data.limit(1000)
result = otp.run(data,
                 start=otp.dt(2026, 7, 28),
                 end=otp.dt(2026, 7, 29),
                 timezone='UTC',
                 symbols='BTCUSD')
result
```

## Crypto Quote Retrieval

Retrieving Quotes from a Crypto Venue.<br />
\\\\
Unlike Equities and Futures, the Bid and Ask Sizes on a crypto venue are fractional.

```
import onetick.py as otp

data = otp.DataSource(db='BINANCE', tick_type='QTE')
data = data.limit(1000)
result = otp.run(data,
                 start=otp.dt(2026, 7, 28),
                 end=otp.dt(2026, 7, 29),
                 timezone='UTC',
                 symbols='BTCUSD')
result
```

## Crypto Book Update Retrieval

Retrieving Book Updates from a Crypto Venue.<br />
\\\\
Book Updates are provided as an L2 dataset, providing updates to Price Levels.<br />
\\\\
Basic retrieval is useful for counting order book changes.<br />
\\\\
To reconstruct the order book, order book aggregations like ``ob_snapshot_wide()`` should be used.

```
import onetick.py as otp

data = otp.DataSource(db='BINANCE', tick_type='PRL')
data = data.limit(1000)
result = otp.run(data,
                 start=otp.dt(2026, 7, 28),
                 end=otp.dt(2026, 7, 29),
                 timezone='UTC',
                 symbols='BTCUSD')
result
```

## Crypto Book Snapshot Retrieval

Retrieving a Book Snapshot at a Specified Time from a Crypto Venue.<br />
\\\\
To reconstruct the order book, the ``ob_snapshot_wide()`` aggregation is used.<br />
\\\\
As this is a crypto book, the `size_max_fractional_digits` attribute is set, allowing the book
to be reconstructed with size stored with up to 9 fractional digits.<br />
\\\\
``ob_snapshot_wide()`` returns the book with Bid and Ask on the same row.

```
import onetick.py as otp

data = otp.DataSource(db='BINANCE', tick_type='PRL')
data = data.ob_snapshot_wide(size_max_fractional_digits=9)
data = data[['BID_PRICE', 'BID_SIZE', 'ASK_PRICE', 'ASK_SIZE', 'LEVEL']]
result = otp.run(data,
                 start=otp.dt(2026, 7, 28, 12),
                 end=otp.dt(2026, 7, 28, 12),
                 timezone='UTC',
                 symbols='BTCUSD')
result
```

## Crypto Book Snapshot Retrieval with Accumulative Values

Retrieving a Book Snapshot at a Specified Time from a Crypto Venue, outputting Accumulative Depth.<br />
\\\\
To reconstruct the order book, the ``ob_snapshot_wide()`` aggregation is used.<br />
\\\\
As this is a crypto book, the `size_max_fractional_digits` attribute is set.<br />
\\\\
``ob_snapshot_wide()`` returns the book in a format with Bid and Ask on the same row.<br />
\\\\
Bid and Ask Value is calculated using `PRICE * SIZE`.<br />
\\\\
The Bid and Ask Sizes are used to calculate accumulative sizes across the book depth, computed with a
running sum aggregation across the levels.

```
import onetick.py as otp

data = otp.DataSource(db='BINANCE', tick_type='PRL')
data = data.ob_snapshot_wide(size_max_fractional_digits=9)

# Value per level = PRICE * SIZE
data['BID_VALUE'] = data['BID_PRICE'] * data['BID_SIZE']
data['ASK_VALUE'] = data['ASK_PRICE'] * data['ASK_SIZE']

# Accumulative sizes across the book depth
data = data.agg({'ACCUM_BID_SIZE': otp.agg.sum('BID_SIZE'),
                 'ACCUM_ASK_SIZE': otp.agg.sum('ASK_SIZE')},
                running=True, all_fields=True)

data = data[['BID_PRICE', 'BID_SIZE', 'ASK_PRICE', 'ASK_SIZE', 'LEVEL',
             'BID_VALUE', 'ASK_VALUE', 'ACCUM_BID_SIZE', 'ACCUM_ASK_SIZE']]
result = otp.run(data,
                 start=otp.dt(2026, 7, 28, 12),
                 end=otp.dt(2026, 7, 28, 12),
                 timezone='UTC',
                 symbols='BTCUSD')
result
```

## Crypto Book Snapshot Retrieval with Accumulative Values and Best Prices

Retrieving a Book Snapshot at a Specified Time from a Crypto Venue, outputting Accumulative Depth and Best Prices.<br />
\\\\
To reconstruct the order book, the ``ob_snapshot_wide()`` aggregation is used.<br />
\\\\
As this is a crypto book, the `size_max_fractional_digits` attribute is set.<br />
\\\\
``ob_snapshot_wide()`` returns the book in a format with Bid and Ask on the same row.<br />
\\\\
Bid and Ask Value is calculated using `PRICE * SIZE`.<br />
\\\\
The Bid and Ask Sizes are used to calculate accumulative sizes across the book depth, computed with a
running sum aggregation across the levels.<br />
\\\\
The Bid and Ask Prices are used to return the Best Prices across the book depth, computed with a
running first aggregation across the levels.

```
import onetick.py as otp

data = otp.DataSource(db='BINANCE', tick_type='PRL')
data = data.ob_snapshot_wide(size_max_fractional_digits=9)

# Value per level = PRICE * SIZE
data['BID_VALUE'] = data['BID_PRICE'] * data['BID_SIZE']
data['ASK_VALUE'] = data['ASK_PRICE'] * data['ASK_SIZE']

# Accumulative sizes and best (first) prices across the book depth
data = data.agg({'ACCUM_BID_SIZE': otp.agg.sum('BID_SIZE'),
                 'ACCUM_ASK_SIZE': otp.agg.sum('ASK_SIZE'),
                 'BEST_BID_PRICE': otp.agg.first('BID_PRICE'),
                 'BEST_ASK_PRICE': otp.agg.first('ASK_PRICE')},
                running=True, all_fields=True)

data = data[['BID_PRICE', 'BID_SIZE', 'ASK_PRICE', 'ASK_SIZE', 'LEVEL',
             'BID_VALUE', 'ASK_VALUE', 'ACCUM_BID_SIZE', 'ACCUM_ASK_SIZE',
             'BEST_BID_PRICE', 'BEST_ASK_PRICE']]
result = otp.run(data,
                 start=otp.dt(2026, 7, 28, 12),
                 end=otp.dt(2026, 7, 28, 12),
                 timezone='UTC',
                 symbols='BTCUSD')
result
```

## Crypto Book Depth Statistics to Trade a Specified Amount Across Time

Calculating Bid and Ask VWAP and other Statistics across time from a Crypto Venue.<br />
\\\\
To calculate Bid and Ask VWAP, the ``ob_summary()`` aggregation is used.<br />
\\\\
As this is a crypto book, the `size_max_fractional_digits` attribute is set.<br />
\\\\
The `max_depth_shares` attribute determines how much should be traded.<br />
\\\\
The `bucket_interval` attribute determines how often to output the resulting book metrics.

The returned `BID_VWAP` and `ASK_VWAP` can be used to calculate Effective Spread.<br />
\\\\
The returned `BID_SIZE` and `ASK_SIZE` identify if the liquidity is present.<br />
\\\\
The returned `BEST_ASK_PRICE` and `BEST_BID_PRICE` can be used to calculate the Price Skew together
with the `BID_VWAP` and `ASK_VWAP`.

```
import onetick.py as otp

data = otp.DataSource(db='BINANCE', tick_type='PRL')
data = data.ob_summary(size_max_fractional_digits=9,
                       bucket_interval=60,
                       max_depth_shares=0.5)
result = otp.run(data,
                 start=otp.dt(2026, 7, 28),
                 end=otp.dt(2026, 7, 29),
                 timezone='UTC',
                 symbols='BTCUSD')
result
```
