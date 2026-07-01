# otp.Operation.round

#### ``Operation.round(precision=0)``

Rounds input column with specified `precision`.

Rounding ``otp.nan`` returns NaN
and rounding ``otp.inf`` returns Infinity.

For values that are exactly half-way between two integers (when the fraction part of value is exactly 0.5),
the rounding method used here is *upwards*, which returns the bigger number.
For other rounding methods see ``otp.math.round`` function.

