# otp.ops.base16_encode

### ``base16_encode(value)``

Encodes the string `value` with Base16 algorithm in accordance to RFC 4648.

* **Parameters:**
  **value** (str, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

Encoding string literal:

```
>>> data = otp.Tick(A=otp.ops.base16_encode('hello'))
>>> otp.run(data)
        Time           A
0 2003-12-01  68656C6C6F
```

Encoding each string in a column:

```
>>> data = otp.Ticks(A=['hello', 'world'])
>>> data['X'] = otp.ops.base16_encode(data['A'])
>>> otp.run(data)
                     Time      A                                                                 X
0 2003-12-01 00:00:00.000  hello  68656C6C6F000000000000000000000000000000000000000000000000000000
1 2003-12-01 00:00:00.001  world  776F726C64000000000000000000000000000000000000000000000000000000
```

Note that all NULL-characters are also encoded by default,
they can be removed with
``rtrim()``:

```
>>> data = otp.Ticks(A=['hello', 'world'])
>>> data['X'] = otp.ops.base16_encode(data['A'].str.rtrim())
>>> otp.run(data)
                     Time      A           X
0 2003-12-01 00:00:00.000  hello  68656C6C6F
1 2003-12-01 00:00:00.001  world  776F726C64
```

##### SEE ALSO
**BASE16_ENCODE** OneTick function

``base16_decode()``

