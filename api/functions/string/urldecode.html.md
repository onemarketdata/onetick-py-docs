# otp.ops.urldecode

### ``urldecode(value)``

Modifies the URI compliant string `value`,
replacing percent-encoded octets `%xx` within it with corresponding characters,
in accordance with RFC 3986.

* **Parameters:**
  **value** (str, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

Decoding string literal:

```
>>> data = otp.Tick(A=otp.ops.urldecode('hello%40gmail.com'))
>>> otp.run(data)
        Time                A
0 2003-12-01  hello@gmail.com
```

Decoding each string in a column:

```
>>> data = otp.Ticks(A=['hello%40gmail.com', 'world%40gmail.com'])
>>> data['X'] = otp.ops.urldecode(data['A'])
>>> otp.run(data)
                     Time                  A                X
0 2003-12-01 00:00:00.000  hello%40gmail.com  hello@gmail.com
1 2003-12-01 00:00:00.001  world%40gmail.com  world@gmail.com
```

##### SEE ALSO
**URLDECODE** OneTick function

``urlencode()``

