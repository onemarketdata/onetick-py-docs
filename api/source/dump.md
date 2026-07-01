# otp.Source.dump

#### ``Source.dump(label=None, where=None, columns=None, callback=None)``

Dumps the `columns` from ticks into std::out in runtime if they fit the `where` condition.
Every dump has a corresponding header that always includes the TIMESTAMP field. Other fields
could be configured using the `columns` parameter. A header could be augmented with a `label` parameter;
this label is an addition column that helps to distinguish ticks
from multiple dumps with the same schema, because ticks from different dumps could be mixed.
It might happen because of the OneTick multithreading, and there is the operating system
buffer between the OneTick and the actual output.
