# otp.ops.get_client_ip_address

### ``get_client_ip_address()``

Returns the IP address of the client application that initiated the query.

If this function runs on the client, an empty string is returned.

* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(CLIENT_IP_ADDRESS=otp.ops.get_client_ip_address())
>>> otp.run(data)
        Time  CLIENT_IP_ADDRESS
0 2003-12-01        10.36.0.231
```

##### SEE ALSO
**GET_CLIENT_IP_ADDRESS** OneTick function

