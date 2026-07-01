# otp.uint

### ``class uint(value, *args, **kwargs)``

OneTick data type representing unsigned integer.

The size of the type is not specified and may vary across different systems.
Most commonly it’s a 4-byte type with allowed values from 0 to 2\*\*32 - 1.

Note that the value is checked to be valid in constructor,
but no overflow checking is done when arithmetic operations are performed.

##### Examples
