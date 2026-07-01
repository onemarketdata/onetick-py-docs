# otp.oqd.SharesOutstanding

### ``class SharesOutstanding(start=otp.utils.adaptive, end=otp.utils.adaptive, symbol=otp.utils.adaptive)``

Bases: ``Source``

Logic is implemented in OQD_SOURCE_SHO EP to retrieve a time series of shares
outstanding for a stock.

The source retrieves a time series of shares outstanding
for a stock. This source only applies to stocks or securities that have
published shares outstanding data.

The series represents total shares outstanding and is not free float
adjusted.

Note: currently actual fields have 9999 year in END_DATE, but it could not fit the
nanosecond timestamp, so it is replaced with 2035-01-01 date.

##### Examples

```
>>> src = otp.oqd.sources.SharesOutstanding()  
>>> otp.run(src,  
