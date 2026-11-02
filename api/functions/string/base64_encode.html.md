# otp.ops.base64_encode

### ``base64_encode(value)``

Encodes the string `value` with Base64 algorithm in accordance to RFC 4648.

* **Parameters:**
  **value** (str, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

Encoding string literal:

```
>>> data = otp.Tick(A=otp.ops.base64_encode('hello'))
>>> otp.run(data)
        Time         A
0 2003-12-01  aGVsbG8=
```

Encoding each string in a column:

```
>>> data = otp.Ticks(A=['hello', 'world'])
>>> data['X'] = otp.ops.base64_encode(data['A'])
>>> otp.run(data)
                     Time      A                                                                 X
0 2003-12-01 00:00:00.000  hello  aGVsbG8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
1 2003-12-01 00:00:00.001  world  d29ybGQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
```

Note that all NULL-characters are also encoded by default,
they can be removed with
``rtrim()``:

```
>>> data = otp.Ticks(A=['hello', 'world'])
>>> data['X'] = otp.ops.base64_encode(data['A'].str.rtrim())
>>> otp.run(data)
                     Time      A         X
0 2003-12-01 00:00:00.000  hello  aGVsbG8=
1 2003-12-01 00:00:00.001  world  d29ybGQ=
```

##### SEE ALSO
**BASE64_ENCODE** OneTick function

``base64_decode()``

