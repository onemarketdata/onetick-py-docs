# otp.oqd.DescriptiveFields

### ``class DescriptiveFields(start=utils.adaptive, end=utils.adaptive, symbol=utils.adaptive)``

Bases: ``Source``

OneQuantData™ source to retrieve a time series of descriptive fields for a symbol.
There will only be ticks on days when some field in the descriptive data changes.
Output ticks will have fields:
OID, END_DATE, COUNTRY, EXCH, NAME,
ISSUE_DESC, ISSUE_CLASS, ISSUE_TYPE, ISSUE_STATUS,
SIC_CODE, IDSYM, TICKER, CALENDAR.

Note: currently actual fields have 9999 year in END_DATE, but it could not fit the
nanosecond timestamp, so it is replaced with 2035-01-01 date.

##### Examples

```
>>> src = otp.oqd.sources.DescriptiveFields()  
>>> otp.run(src,  
