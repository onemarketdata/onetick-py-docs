# otp.Operation.float.str

### ``str(length=10, precision=6)``

Converts float to str.

Converts number to string with given `length` and `precision`.
The specified `length` should be greater than or equal
to the part of the number before the decimal point plus the number’s sign (if any).

If `length` is specified as an int, the method will return strings with `length` characters,
if `length` is specified as a column, the method will return string default (64 characters) length.

* **Parameters:**
  * **length** (*Operation* *or* *int*) – Length of the string.
  * **precision** (*Operation* *or* *int*) – Number of symbols after dot.
* **Returns:**
  **result** – String representation of float value.
* **Return type:**
  `Operation`

##### Examples

```
>>> data = otp.Ticks(X=[1, 2.17, 10.31861, 3.141593, otp.nan, otp.inf, -otp.inf])
>>> data["Y"] = data["X"].float.str(15, 3)
>>> otp.run(data)
                     Time          X       Y
0 2003-12-01 00:00:00.000   1.000000   1.000
1 2003-12-01 00:00:00.001   2.170000   2.170
