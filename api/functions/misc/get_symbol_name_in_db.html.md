# otp.ops.get_symbol_name_in_db

### ``get_symbol_name_in_db()``

Returns the symbol name of the tick in the database.

This function is supported only in the **ADD_FIELD**, **ADD_FIELDS** and **WHERE_CLAUSE** event processors.

This function requires the event processor to have a single tick source.

* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')
>>> data = data.limit(1)
>>> data['SYMBOL_NAME'] = otp.ops.get_symbol_name_in_db()
>>> data = data[['PRICE', 'SIZE', 'SYMBOL_NAME']]
>>> result = otp.run(data, symbols=['AAPL', 'MSFT'],
...                  date=otp.dt(2024, 2, 1), timezone='America/New_York')
>>> result['AAPL']
                           Time  PRICE  SIZE SYMBOL_NAME
0 2024-02-01 04:00:00.008283417  186.5     6        AAPL
```

##### SEE ALSO
**GET_SYMBOL_NAME_IN_DB** OneTick function

