# otp.ops.urlencode

### ``urlencode(value)``

Modifies the string `value` to be URI compliant,
replacing most non-alphanumeric characters with `%xx` within it,
in accordance with RFC 3986.

* **Parameters:**
  **value** (str, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

Encoding string literal:

```
>>> data = otp.Tick(A=otp.ops.urlencode('hello@gmail.com'))
>>> otp.run(data)
        Time                  A
0 2003-12-01  hello%40gmail.com
```

Encoding each string in a column:

```
>>> data = otp.Ticks(A=['hello@gmail.com', 'world@gmail.com'])
>>> data['X'] = otp.ops.urlencode(data['A'])
>>> otp.run(data)
                     Time                A                  X
0 2003-12-01 00:00:00.000  hello@gmail.com  hello%40gmail.com
1 2003-12-01 00:00:00.001  world@gmail.com  world%40gmail.com
```

##### SEE ALSO
**URLENCODE** OneTick function

``urldecode()``

