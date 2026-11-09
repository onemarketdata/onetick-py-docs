# otp.ops.utf8_to_str

### ``utf8_to_str(value, encoding)``

Returns the specified string `value` re-encoded from UTF-8 to `encoding`.

* **Parameters:**
  * **value** (str, ``Operation``)
  * **encoding** (str, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

Encoding string literal:

```
>>> data = otp.Tick(A=otp.ops.utf8_to_str('español', encoding='ascii'))
>>> otp.run(data, encoding='utf-8')
        Time        A
0 2003-12-01  espaol
```

Encoding each string in a column:

```
>>> data = otp.Ticks(A=['hello', 'español'])
>>> data['X'] = otp.ops.utf8_to_str(data['A'], encoding='ascii')
>>> otp.run(data, encoding='utf-8')
                     Time        A        X
0 2003-12-01 00:00:00.000    hello    hello
1 2003-12-01 00:00:00.001  español  espaol
```

##### SEE ALSO
**UTF8_TO_STR** OneTick function

``str_to_utf8()``

``encoding_converter()``

