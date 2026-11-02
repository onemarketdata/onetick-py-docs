# otp.ops.declare_string_size

### ``declare_string_size(expression, size)``

This function is used to indicate the maximum `size` of the string returned by `expression`.

This function is especially useful in SQL queries in which some output fields are expressions that return strings.
In those SQL queries, use of ``declare_string_size()`` around such expressions is the only way to ensure
that output string fields will be sufficiently wide for the entire output value.

* **Parameters:**
  * **expression** (str, ``Operation``)
  * **size** (*int*)
* **Return type:**
  ``Operation``

##### Examples

Limit the length of the string expression:

```
>>> data = otp.Ticks(A=['hello', 'world!'])
>>> data['X'] = otp.ops.declare_string_size(data['A'].str.repeat(3), 10)
>>> otp.run(data)
                     Time       A           X
0 2003-12-01 00:00:00.000   hello  hellohello
1 2003-12-01 00:00:00.001  world!  world!worl
```

##### SEE ALSO
**DECLARE_STRING_SIZE** OneTick function

