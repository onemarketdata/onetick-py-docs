# otp.Operation.float.cmp

### ``cmp(other, eps)``

Compare two double values between themselves according to `eps` relative difference.

This function returns 0 if column == other, 1 if column > other, and -1 if column < other.

If both values are NaN, the result is 0.
If only one value is NaN, NaN is treated as less than any non-NaN value.

Two numbers are considered to be equal if:

* `abs(column - other) <= 1e-12` (absolute tolerance; useful near zero)
* or `abs(column - other) / max(1, max(abs(column), abs(other))) <= eps` (relative tolerance).

`eps` is a relative epsilon (scale-dependent), not an absolute difference.

* **Parameters:**
  * **other** (*Operation* *or* *float*) – column or value to compare with
  * **eps** (*Operation* *or* *float*) – column or value with relative difference
* **Returns:**
  **result** – 0 if column == other, 1 if column > other, and -1 if column < other.
