# otp.Source.schema

#### ``property Source.schema *: `Schema`*``

Represents actual python data schema in the column-name -> type format.
For example, could be used after the ``Source.sink()`` to adjust
the schema.

* **Return type:**
  `Schema`

##### Examples

```
>>> data = otp.Ticks([['X', 'Y',   'Z'],
...                   [  1, 0.5, 'abc']])
>>> data['T'] = data['Time']
>>> data.schema
{'X': <class 'int'>, 'Y': <class 'float'>, 'Z': <class 'str'>, 'T': <class 'onetick.py.types.nsectime'>}
```

```
>>> data.schema['X']
<class 'int'>
```

```
>>> data.schema['X'] = float
>>> data.schema['X']
<class 'float'>
```

```
>>> 'W' in data.schema
False
>>> data.schema['W'] = otp.nsectime
>>> 'W' in data.schema
True
>>> data.schema['W']
<class 'onetick.py.types.nsectime'>
```

##### SEE ALSO
``Source.sink``

### *class* Schema

Bases: ``Mapping``

A source data schema proxy. It allows to work with source schema in
a frozen-dict manner. It also allows to set using the `set`
and update a source schema using the `update` methods.

#### items() → a set-like object providing a view on D's items

#### keys() → a set-like object providing a view on D's keys
