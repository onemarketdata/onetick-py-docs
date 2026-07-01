# otp.Operation.str.replace

### ``replace(pat, repl)``

Search for occurrences (case dependent) of `pat` and replace with `repl`.

* **Parameters:**
  * **pat** (*str* *or* *Column* *or* *Operation*) – Pattern to replace.
  * **repl** (*str* *or* *Column* *or* *Operation*) – Replacement string.
* **Returns:**
  String with `pat` replaced by `repl`.
* **Return type:**
  `Operation`

##### Examples

```
>>> data = otp.Ticks(X=['A Table', 'A Chair', 'An Apple'])
