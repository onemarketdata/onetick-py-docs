# otp.Operation.str.lower

#### \_StrAccessor.lower(, utf8=False)

Convert a string to lower case.

* **Parameters:**
  **utf8** (*bool*) – If set, then UTF-8 format is supported.
* **Returns:**
  Lowercased string
* **Return type:**
  `Operation`

##### Examples

```
>>> data = otp.Ticks(X=['HeLlO', 'wOrLd!'])
>>> data['LOW'] = data['X'].str.lower()
>>> otp.run(data)
                     Time       X     LOW
0 2003-12-01 00:00:00.000   HeLlO   hello
1 2003-12-01 00:00:00.001  wOrLd!  world!
```

##### SEE ALSO
**LOWER** OneTick function

**LOWER_UTF8** OneTick function

