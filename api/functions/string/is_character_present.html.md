# otp.ops.is_character_present

### ``is_character_present(value, characters)``

Returns True (1) if the `value` contains
at least one character from the character set specified by `characters`, otherwise False (0).

* **Parameters:**
  * **value** (str, ``Operation``)
  * **characters** (str, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

Check if characters are present in a string literal:

```
>>> data = otp.Tick(A=otp.ops.is_character_present('hello', 'abcd'))
>>> otp.run(data)
        Time  A
0 2003-12-01  0
```

Check if characters are present in each string of the column:

```
>>> data = otp.Ticks(A=['hello', 'world'])
>>> data['ABCD'] = otp.ops.is_character_present(data['A'], 'abcd')
>>> otp.run(data)
                     Time      A  ABCD
0 2003-12-01 00:00:00.000  hello     0
1 2003-12-01 00:00:00.001  world     1
```

##### SEE ALSO
**IS_CHARACTER_PRESENT** OneTick function

``character_present()``

