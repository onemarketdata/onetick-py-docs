# otp.Operation.str.position

#### \_StrAccessor.position(substring, , , utf8=False)

Returns the position (0-based) of `substring` in this column.

If `substring` was not found, -1 is returned.

* **Parameters:**
  * **substring** (*str* *or* *Column* *or* *Operation*)
  * **utf8** (*bool*) – If set, then UTF-8 format is supported.

##### Examples

```
>>> data = otp.Ticks(X=['ananas', 'banana', 'potato'])
>>> data['Y'] = data['X'].str.position('ana')
>>> otp.run(data)
                     Time       X   Y
0 2003-12-01 00:00:00.000  ananas   0
1 2003-12-01 00:00:00.001  banana   1
2 2003-12-01 00:00:00.002  potato  -1
```

##### SEE ALSO
**POSITION** OneTick function

**POSITION_UTF8** OneTick function

``find()``

