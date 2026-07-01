# otp.oqd.CorporateActions

### ``class CorporateActions(start=utils.adaptive, end=utils.adaptive, symbol=utils.adaptive)``

Bases: ``Source``

OneQuantData™ source EP to retrieve a time series of corporate
actions for a symbol.

This source will return all corporate action fields available for a symbol
with EX-Dates between the query start time and end time (end time is not inclusive).  The
timestamp of the series is equal to the EX-Date of the corporate
action with a time of 0:00:00 GMT.

##### Examples

