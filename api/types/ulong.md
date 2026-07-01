# otp.ulong

### ``class ulong(value, *args, **kwargs)``

OneTick data type representing unsigned long integer.

The size of the type is not specified and may vary across different systems.
Most commonly it’s a 8-byte type with allowed values from 0 to 2\*\*64 - 1.

Note that the value is checked to be valid in constructor,
but no overflow checking is done when arithmetic operations are performed.

##### Examples
