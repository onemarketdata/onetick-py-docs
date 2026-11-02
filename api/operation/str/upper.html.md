# otp.Operation.str.upper

#### \_StrAccessor.upper(, utf8=False)

Converts a string to upper case.

* **Parameters:**
  **utf8** (*bool*) – If set, then UTF-8 format is supported.
* **Returns:**
  Uppercased string
* **Return type:**
  `Operation`

##### Examples

```
>>> data = otp.Ticks(X=['HeLlO', 'wOrLd!'])
>>> data['UP'] = data['X'].str.upper()
>>> otp.run(data)
                     Time       X      UP
0 2003-12-01 00:00:00.000   HeLlO   HELLO
1 2003-12-01 00:00:00.001  wOrLd!  WORLD!
```

##### SEE ALSO
**UPPER** OneTick function

**UPPER_UTF8** OneTick function

