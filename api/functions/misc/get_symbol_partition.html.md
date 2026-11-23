# otp.ops.get_symbol_partition

### ``get_symbol_partition(symbol_name, timestamp)``

Returns the physical database to which the `symbol_name` belongs, for the `timestamp` specified.

For physical databases returns the database name itself.

For partitioned databases returns the partition to which the symbol resolves based on the underlying partitioner.
It returns an empty string if the partition cannot be determined.

* **Parameters:**
  * **symbol_name** (str | ``Operation``) – Full symbol name in the form `<dbname>::<symbol>`.
  * **timestamp** (``otp.datetime`` | ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Symbols('US_COMP_SAMPLE', for_tick_type='TRD', keep_db=True).limit(5)
>>> data['SYMBOL_PARTITION'] = otp.ops.get_symbol_partition(data['SYMBOL_NAME'], otp.dt(2024, 3, 1, 12))
>>> otp.run(data, date=otp.dt(2024, 2, 1))
          Time           SYMBOL_NAME SYMBOL_PARTITION
0   2024-02-01     US_COMP_SAMPLE::A   US_COMP_SAMPLE
1   2024-02-01   US_COMP_SAMPLE::AAL   US_COMP_SAMPLE
2   2024-02-01  US_COMP_SAMPLE::AAPL   US_COMP_SAMPLE
3   2024-02-01  US_COMP_SAMPLE::ABBV   US_COMP_SAMPLE
4   2024-02-01  US_COMP_SAMPLE::ABNB   US_COMP_SAMPLE
```

##### SEE ALSO
**GET_SYMBOL_PARTITION** OneTick function

