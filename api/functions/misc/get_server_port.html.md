# otp.ops.get_server_port

### ``get_server_port()``

Returns the port number of the tick server, where this function is executing.

If this function runs on the client, 0 is returned.

* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(SERVER_PORT=otp.ops.get_server_port())
>>> otp.run(data)
        Time  SERVER_PORT
0 2003-12-01        40001
```

##### SEE ALSO
**GET_SERVER_PORT** OneTick function

