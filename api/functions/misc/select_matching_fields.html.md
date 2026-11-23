# otp.ops.select_matching_fields

### ``select_matching_fields(regex, , field_types=None)``

Returns a comma-separated list of tick descriptor field names.

A field is included in the resulting comma-separated field list if:

* Its name in the tick descriptor fully matches the `regex` parameter,
* If `field_types` parameter is specified, and the type of the field is one of the specified types.

* **Parameters:**
  * **regex** (*str*) – A regular expression to match field names with.
  * **field_types** (*type* *|* *str* *|* *list* **[*str* *|* *type* *]*  *|* *None*) – 

    One of the python classes specified in `Types` or a list of them.
    Or a comma separated string of OneTick data types string names or list of such strings.

    By default all field types are returned.
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(ASK_PRICE=1.1, BID_PRICE=2.2, ASK_SIZE=3, BID_SIZE=4)
>>> data['ASK_FIELDS'] = otp.ops.select_matching_fields('ASK.*')
>>> data['ASK_FLOATS'] = otp.ops.select_matching_fields('ASK.*', float)
>>> otp.run(data)
        Time  ASK_PRICE  BID_PRICE  ASK_SIZE  BID_SIZE          ASK_FIELDS  ASK_FLOATS
0 2003-12-01        1.1        2.2         3         4  ASK_PRICE,ASK_SIZE   ASK_PRICE
```

##### SEE ALSO
**SELECT_MATCHING_FIELDS** OneTick function

