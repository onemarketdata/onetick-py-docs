# otp.ops.get_otq_parameters

### ``get_otq_parameters()``

Returns a list of the otq parameters in the function’s query as a string, separated with `;`.

* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(OTQ_PARAMETERS=otp.ops.get_otq_parameters())
>>> otp.run(data, query_params={'A': 1, 'B': 'hello'})
        Time  OTQ_PARAMETERS
0 2003-12-01     A=1;B=hello
```

##### SEE ALSO
**GET_OTQ_PARAMETERS** OneTick function

