# otp.adaptive

### *class* adaptive

Bases: ``object``

This class is mostly used as the default value for the functions’ parameters
when the value of `None` has some other meaning
or when the meaning of the parameter depends on the other parameter’s values,
`otp.config` options or the context.

##### Examples

For example, setting ``DataSource`` `symbols` parameter
to `otp.adaptive` allows to set symbols when running the query later.

