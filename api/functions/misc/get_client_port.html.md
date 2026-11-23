# otp.ops.get_client_port

### ``get_client_port()``

Returns the port number of the client application that initiated the query.

If this function runs on the client, 0 is returned.

* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(CLIENT_PORT=otp.ops.get_client_port())
>>> otp.run(data)
        Time  CLIENT_PORT
0 2003-12-01        52642
```

##### SEE ALSO
**GET_CLIENT_PORT** OneTick function

