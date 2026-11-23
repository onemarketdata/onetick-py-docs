# otp.ops.tick_tostring

### ``tick_tostring(, separator_char='', represent_fractional_val_as_hex=False, sort_fields_by_name=False, include_field_names=False)``

Creates a string from the tick by concatenating all fields of the tick except the TIMESTAMP field.

* **Parameters:**
  * **separator_char** (*str*) – 

    Specifies the separator character to use between field values in the resulting string.
    If specified, it should be either an empty string
    or a string that consists of a single character.

    If separator_char is an empty string, and `include_field_names` is set to False, no separator is used.
    If separator_char is an empty string, and `include_field_names` is set to True,
    a comma will be used as a separator.

    Default - empty string.
  * **represent_fractional_val_as_hex** (*bool*) – 

    If set to True, results in all bytes of values of each decimal, double, and float tick field
    to be output in their hexadecimal form,
    with the hex representation of more significant bytes preceding hex representation of less significant bytes.

    If set to False, the usual string representations of these values are output.

    Default: False.
  * **sort_fields_by_name** (*bool*) – 

    If set to True, the values of the tick fields will be output
    according to the alphabetical order of the field names.

    Otherwise, the values of the tick fields will be output in the order
    in which the fields as specified in the tick descriptor.

    Default: False.
  * **include_field_names** (*bool*) – 

    If set to True, the names of the tick fields, along with “=”,
    will be printed in front of the corresponding values.

    Default: False.
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(B=2.2, A=1, C=otp.dt(2024, 1, 1), D='hello world')
>>> data['TOSTRING'] = otp.ops.tick_tostring(
...     separator_char=',',
...     sort_fields_by_name=True,
...     include_field_names=True,
... )
>>> otp.run(data)
        Time    B  A          C            D                                            TOSTRING
0 2003-12-01  2.2  1 2024-01-01  hello world  A=1,B=2.200000,C=1704085200000000000,D=hello world
```

##### SEE ALSO
**TICK_TOSTRING** OneTick function

