# otp.default_by_type

### ``default_by_type(dtype)``

Get default value by OneTick type.

* **Parameters:**
  **dtype** – one of onetick-py base types

##### Examples

```
>>> otp.default_by_type(float)
nan
>>> otp.default_by_type(otp.decimal)
decimal(0)
>>> otp.default_by_type(int)
0
