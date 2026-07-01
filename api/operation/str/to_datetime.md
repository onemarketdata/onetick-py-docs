# otp.Operation.str.to_datetime

### ``to_datetime(format='%Y/%m/%d %H:%M:%S.%J', timezone=None, unit=None)``

Converts the formatted time to the number of nanoseconds (datetime) since 1970/01/01 GMT.

* **Parameters:**
  * **format** (*str* *,* *Operation* *,* *Column*) – 

    The format might contain any characters, but the following combinations of
    characters have special meanings

    %Y - Year (4 digits)

    %y - Year (2 digits)

    %m - Month (2 digits)

    %d - Day of month (2 digits)

    %H - Hours (2 digits, 24-hour format)

    %I - Hours (2 digits, 12-hour format)

    %M - Minutes (2 digits)

    %S - Seconds (2 digits)

    %J - Nanoseconds (9 digits)

    %p - AM/PM (2 characters)
  * **timezone** (*str* *|* *Operation* *|* *Column*) – Timezone. The timezone of the query will be used if no `timezone` was passed.
  * **unit** (*str* *,* *optional*) – If set, format and timezone are ignored.
    If equals to ns, constructs a nanosecond-granularity timestamp from a millisecond-granularity
    string. It has the following format: < milliseconds since 1970/01/01 GMT >.< fraction of a millisecond >.
    The fraction might have at most six digits. If the fraction is equal to zero,
    .< fraction of a millisecond > is optional.
    If equals to ms, constructs a millisecond-granularity timestamp from a millisecond-granularity
    string. It has the following format: < milliseconds since 1970/01/01 GMT >.
* **Returns:**
  ``nsectime`` Operation obtained from the string
* **Return type:**
  `Operation`

##### Examples

```
>>> data = otp.Tick(X='5/17/22-11:10:56.123456789')
>>> data['Y'] = data['X'].str.to_datetime('%m/%d/%y-%H:%M:%S.%J', 'Europe/London')
