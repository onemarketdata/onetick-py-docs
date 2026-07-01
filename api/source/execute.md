# otp.Source.execute

#### ``Source.execute(*operations, inplace=False)``

Execute operations without returning their values.
Some operations in onetick.py can be used to modify the state of some object
(tick sequences mostly) and in that case user may not want to save the result of the
