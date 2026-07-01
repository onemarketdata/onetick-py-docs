# otp.Operation.float.eq

### ``eq(other, delta)``

Compare two double values between themselves according to `delta` relative difference.
Calculated as `abs(column - other) <= delta`.

* **Parameters:**
  * **other** (*Operation* *,* *float*) – column or value to compare with
  * **delta** (*Operation* *,* *float*) – column or value with relative difference
