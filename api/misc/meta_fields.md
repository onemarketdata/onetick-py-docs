# otp.meta_fields

### *class* MetaFields

Bases: ``object``

OneTick defines several pseudo-columns that can be treated as if they were columns of every tick.

These columns can be accessed directly via ``onetick.py.Source.__getitem__()`` method.

But in case they are used in ``Expr``
they can be accessed via `onetick.py.Source.meta_fields`.

##### Examples

Accessing pseudo-fields as columns or as class properties

