# otp.ops.base64_decode

### ``base64_decode(value)``

Decodes the string `value` encoded with Base64 algorithm in accordance to RFC 4648.

* **Parameters:**
  **value** (str, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

Decoding string literal:

```
>>> data = otp.Tick(A=otp.ops.base64_decode('aGVsbG8='))
>>> otp.run(data)
        Time      A
0 2003-12-01  hello
```

Decoding each string in a column:

```
>>> data = otp.Ticks(A=['aGVsbG8=', 'd29ybGQ='])
>>> data['X'] = otp.ops.base64_decode(data['A'])
>>> otp.run(data)
                     Time         A      X
0 2003-12-01 00:00:00.000  aGVsbG8=  hello
1 2003-12-01 00:00:00.001  d29ybGQ=  world
```

##### SEE ALSO
**BASE64_DECODE** OneTick function

``base64_encode()``

