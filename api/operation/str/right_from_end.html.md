# otp.Operation.str.right_from_end

#### \_StrAccessor.right_from_end(count, , , utf8=False)

Returns last `count` characters, counted from the end of the string array (even after the NULL-character).

For getting last characters from the end of the string (before NULL-character), use ``last()``.

* **Parameters:**
  * **count** (*int* *or* *Column* *or* *Operation*) – Number of last characters to return.
  * **utf8** (*bool*) – If set, then UTF-8 format is supported.

##### Examples

This method returns the characters from the end of string array, not string itself, which may be unexpected.
Default string type in OneTick has size of 64,
so getting the last characters for short strings will give you nothing.

In this case we are using short strings and big offsets to get the result:

```
>>> data = otp.Ticks(X=['hello', 'everyone'])
>>> data['RIGHT_1'] = data['X'].str.right_from_end(1)
>>> data['RIGHT_59'] = data['X'].str.right_from_end(59)
>>> data['RIGHT_62'] = data['X'].str.right_from_end(62)
>>> otp.run(data)
                     Time         X  RIGHT_1  RIGHT_59  RIGHT_62
0 2003-12-01 00:00:00.000     hello                          llo
1 2003-12-01 00:00:00.001  everyone                one    eryone
```

Alternatively, method ``rtrim()`` can be used to trim the right part of the string before using this method,
to achieve result similar to method ``last()``:

```
>>> data = otp.Ticks(X=['hello', 'everyone'])
>>> data['RIGHT_1_RTRIM'] = data['X'].str.rtrim().str.right_from_end(1)
>>> data['RIGHT_5_RTRIM'] = data['X'].str.rtrim().str.right_from_end(5)
>>> otp.run(data)
                     Time         X  RIGHT_1_RTRIM  RIGHT_5_RTRIM
0 2003-12-01 00:00:00.000     hello              o          hello
1 2003-12-01 00:00:00.001  everyone              e          ryone
```

##### SEE ALSO
**RIGHT** OneTick function

**RIGHT_UTF8** OneTick function

``last()``

