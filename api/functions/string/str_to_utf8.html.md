# otp.ops.str_to_utf8

### ``str_to_utf8(value, encoding)``

Returns the specified string `value` re-encoded from `encoding` to UTF-8.

* **Parameters:**
  * **value** (str, ``Operation``)
  * **encoding** (str, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

Encoding string literal:

```
>>> data = otp.Tick(A=otp.ops.str_to_utf8('hello', encoding='ascii'))
>>> otp.run(data)
        Time      A
0 2003-12-01  hello
```

Encoding each string in a column:

```
>>> data = otp.Ticks(A=['hello', 'world'])
>>> data['X'] = otp.ops.str_to_utf8(data['A'], encoding='ascii')
>>> otp.run(data)
                     Time      A      X
0 2003-12-01 00:00:00.000  hello  hello
1 2003-12-01 00:00:00.001  world  world
```

##### SEE ALSO
**STR_TO_UTF8** OneTick function

``utf8_to_str()``

``encoding_converter()``

