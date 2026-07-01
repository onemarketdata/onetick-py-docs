# otp.Operation.str.contains

### ``contains(substr)``

Check if the string contains `substr`.

* **Parameters:**
  **substr** (*str* *or* *Column* *or* *Operation*) – A substring to search for within the string.
* **Returns:**
  `True` if the string contains the substring, `False` otherwise.
  Note that boolean Operation is converted to float if added as a column.
* **Return type:**
  `Operation`

#### NOTE
This function does not support regular expressions.
Use ``match()`` for this purpose.

##### Examples

```
>>> data = otp.Ticks(X=['hello', 'world!'])
>>> data['CONTAINS'] = data['X'].str.contains('hel')
>>> otp.run(data)
                     Time       X  CONTAINS
0 2003-12-01 00:00:00.000   hello       1.0
1 2003-12-01 00:00:00.001  world!       0.0
```

Other columns can be used as parameter `substr` too:
