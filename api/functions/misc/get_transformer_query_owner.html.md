# otp.ops.get_transformer_query_owner

### ``get_transformer_query_owner()``

Returns an integer indicator of the owner of the transformer query.

* 0 - not a transformer
* 1 - memory loader transformer
* 2 - daily loader transformer
* 3 - CEP transformer
* 4 - tick dump writer transformer

* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(TRANSFORMER_QUERY_OWNER=otp.ops.get_transformer_query_owner())
>>> otp.run(data)
        Time  TRANSFORMER_QUERY_OWNER
0 2003-12-01                        0
```

##### SEE ALSO
**GET_TRANSFORMER_QUERY_OWNER** OneTick function

