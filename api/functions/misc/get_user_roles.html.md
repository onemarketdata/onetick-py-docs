# otp.ops.get_user_roles

### ``get_user_roles()``

Returns a comma-separated list of the roles of the user who is executing the query.

* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(USER_ROLES=otp.ops.get_user_roles())
>>> otp.run(data)
        Time USER_ROLES
0 2003-12-01      Admin
```

##### SEE ALSO
**GET_USER_ROLES** OneTick function

