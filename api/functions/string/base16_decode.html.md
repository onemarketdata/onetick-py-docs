# otp.ops.base16_decode

### ``base16_decode(value)``

Decodes the string `value` encoded with Base16 algorithm in accordance to RFC 4648.

* **Parameters:**
  **value** (str, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

Decoding string literal:

```
>>> data = otp.Tick(A=otp.ops.base16_decode('68656C6C6F'))
>>> otp.run(data)
        Time      A
0 2003-12-01  hello
```

Decoding each string in a column:

```
>>> data = otp.Ticks(A=['68656C6C6F', '776F726C64'])
>>> data['X'] = otp.ops.base16_decode(data['A'])
>>> otp.run(data)
                     Time           A      X
0 2003-12-01 00:00:00.000  68656C6C6F  hello
1 2003-12-01 00:00:00.001  776F726C64  world
```

##### SEE ALSO
**BASE16_DECODE** OneTick function

``base16_encode()``

