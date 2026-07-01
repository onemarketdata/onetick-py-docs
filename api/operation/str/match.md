# otp.Operation.str.match

### ``match(pat, case=True)``

Match the text against a regular expression specified in the `pat` parameter.

* **Parameters:**
  * **pat** (*str* *or* *Column* *or* *Operation*) – A pattern specified via the POSIX extended regular expression syntax.
  * **case** (*bool*) – If `True`, then regular expression is case-sensitive.
* **Returns:**
  `True` if the match was successful, `False` otherwise.
  Note that boolean Operation is converted to float if added as a column.
* **Return type:**
  `Operation`

##### Examples

```
>>> data = otp.Ticks(X=['hello', 'there were 77 ticks'])
>>> data['Y'] = data['X'].str.match(r'\d\d')
>>> otp.run(data)
                     Time                    X    Y
0 2003-12-01 00:00:00.000                hello  0.0
1 2003-12-01 00:00:00.001  there were 77 ticks  1.0
```

Other columns can be used as parameter `pat` too:

