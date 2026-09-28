# Filtering

Here are covered the basics of different filtering operations.<br />
\\\\
More complex “business” use-cases can be found in `Filtering Use Cases`

Let’s start with an unfiltered time series:

```
import onetick.py as otp

data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')
data = data[['PRICE', 'SIZE', 'COND', 'EXCHANGE']]
otp.run(data,
        start=otp.dt(2024, 2, 1, 9, 30),
        end=otp.dt(2024, 2, 1, 9, 30, 1),
        timezone='America/New_York',
        symbols='AAPL')
```

## Columns and Operations

Simple filtering can be expressed by comparing the values of ``columns``
or the results of ``operations`` that use columns.

Method ``where()`` can be used to filter data
with operations that return boolean result (True or False).

For example, we can compare the value of the field
to some string literal or number with ``==`` operator:

```
data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')
data = data[['PRICE', 'SIZE', 'COND', 'EXCHANGE']]

# get only the ticks with EXCHANGE field equal to K
data = data.where(data['EXCHANGE'] == 'K')

otp.run(data,
        start=otp.dt(2024, 2, 1, 9, 30),
        end=otp.dt(2024, 2, 1, 9, 30, 1),
        timezone='America/New_York',
        symbols='AAPL')
```

Note that all of the filtering is done in OneTick not in Python,
which is much more efficient and lets us work with much bigger data sets.

### Binary operations

Filters can also include `and/or` binary logic
with ``&`` and ``|`` operators:

```
data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')
data = data[['PRICE', 'SIZE', 'COND', 'EXCHANGE']]

# get only the ticks which have both EXCHANGE field equal to K and the PRICE bigger than 183.950
data = data.where((data['EXCHANGE'] == 'K') & (data['PRICE'] > 183.950))

otp.run(data,
        start=otp.dt(2024, 2, 1, 9, 30),
        end=otp.dt(2024, 2, 1, 9, 30, 1),
        timezone='America/New_York',
        symbols='AAPL')
```

### String operations

Many methods are available on a string columns with ``.str`` accessor.

For example, string search can be performed with regular expressions using
``.str.match``
or with SQL like expressions using
``.str.ilike``.

Filtering for a specific trade condition can be done with
``.str.contains``:

```
data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')
data = data[['PRICE', 'SIZE', 'COND', 'EXCHANGE']]

# get only the ticks which have I character in the COND field
data = data.where(data['COND'].str.contains('I'))

otp.run(data,
        start=otp.dt(2024, 2, 1, 9, 30),
        end=otp.dt(2024, 2, 1, 9, 30, 1),
        timezone='America/New_York',
        symbols='AAPL')
```

Different sets of methods are available for ``.dt``
and ``.float`` accessors.

### Float comparison

Because of the way float values are stored in the memory,
you can have some unprecise results when comparing them with ``==`` operator.

Instead it’s recommended to use
``.float.cmp``
or ``.float.eq`` methods,
which allow to specify precision of comparison manually:

```
data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')
data = data[['PRICE', 'SIZE', 'COND', 'EXCHANGE']]

# get only the ticks where PRICE is bigger than 183.950 with 0.0000001 relative difference
data = data.where(data['PRICE'].float.cmp(183.950, 0.0000001) == 1)

otp.run(data,
        start=otp.dt(2024, 2, 1, 9, 30),
        end=otp.dt(2024, 2, 1, 9, 30, 1),
        timezone='America/New_York',
        symbols='AAPL')
```

Also there are ``otp.nan`` and ``otp.inf`` special objects in OneTick
that can be used to filter out NaN and Infinite values.<br />
\\\\
In OneTick they can be safely used with ``==`` operator,
unlike common implementations which treat comparison with NaN as always returning False.

```
data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')

# calculate hourly VWAP, then filter out NaN buckets
data = data.agg({'VWAP': otp.agg.vwap('PRICE', 'SIZE')}, bucket_interval=otp.Hour(1))
data = data.where(data['VWAP'] != otp.nan)

otp.run(data,
        start=otp.dt(2024, 2, 1, 0, 0),
        end=otp.dt(2024, 2, 1, 10, 0),
        timezone='America/New_York',
        symbols='AAPL')
```

## Filtering methods

``Source`` class also have many other `methods` that work as a filter.

For example, filter that limits attention to on-exchange continuous trading trades
can be implemented like this with ``character_present()`` method:

```
data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')
data = data[['PRICE', 'SIZE', 'COND', 'EXCHANGE']]

# get only the ticks where COND field doesn't contain specified characters
data = data.character_present(data['COND'], 'O6TUHILNRWZ47QMBCGPV', discard_on_match=True)

otp.run(data,
        start=otp.dt(2024, 2, 1, 9, 30),
        end=otp.dt(2024, 2, 1, 9, 30, 1),
        timezone='America/New_York',
        symbols='AAPL')
```

### Filtering out outliers or missing values

Method ``skip_bad_tick()`` can be used to filter out the ticks which have field values that
differ too much from the values of the same fields in the surrounding ticks.<br />
\\\\
Method ``dropna()`` can be used to filter out the ticks with NaN values in the fields,
similar to how we do it in the “Float comparison” section.

```
data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')
data = data[['PRICE', 'SIZE', 'COND', 'EXCHANGE']]

# skip bad PRICEs
data = data.skip_bad_tick('PRICE')
# drop all ticks with NaN values in any field
data = data.dropna()

otp.run(data,
        start=otp.dt(2024, 2, 1, 9, 30),
        end=otp.dt(2024, 2, 1, 9, 30, 1),
        timezone='America/New_York',
        symbols='AAPL')
```

## Time filtering

Ticks can be filtered in OneTick by setting the query time range or filtering the ticks by their timestamps.

### Setting the time range of the query

Query time range can be set in ``otp.run`` function with `start` and `end` parameters,
as was done in all previous examples.

Also these parameters can instead be set on
``otp.DataSource`` object (and some other sources):

```
data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD',
                      start=otp.dt(2024, 2, 1, 9, 30),
                      end=otp.dt(2024, 2, 1, 9, 30, 1))
data = data[['PRICE', 'SIZE', 'COND', 'EXCHANGE']]
otp.run(data,
        timezone='America/New_York',
        symbols='AAPL')
```

### Apply times daily

Parameter `apply_times_daily` in ``otp.run`` function can be used
to apply the same time range for each day when querying several days:

```
data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')
data = data[['PRICE', 'SIZE', 'COND', 'EXCHANGE']]

# in this case time range will be set from 09:30:00 to 09:30:00.002
# for days 2024-02-01 and 2024-02-02
otp.run(data,
        start=otp.dt(2024, 2, 1, 9, 30, 0),
        end=otp.dt(2024, 2, 2, 9, 30, 0, 2000),
        timezone='America/New_York',
        apply_times_daily=True,
        symbols='AAPL')
```

### Using time filtering methods and operations

Similar methods as in previous examples can be used to filter ticks by their timestamps:

* `TIMESTAMP` meta field comparison
* ``time_filter()`` method

```
data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')
data = data[['PRICE', 'SIZE', 'COND', 'EXCHANGE']]

# filter the ticks inside the 9:30-16:00 time range for each day
data = data.time_filter(start_time='093000000', end_time='160000000')

# filter ticks before 2024-02-01 09:30:01
# (note that this is a fixed datetime value
#  and won't work on a daily basis like apply_times_daily or time_filter)
data = data.where(data['TIMESTAMP'] < otp.dt(2024, 2, 1, 9, 30, 1))

otp.run(data,
        start=otp.dt(2024, 2, 1),
        end=otp.dt(2024, 2, 3),
        timezone='America/New_York',
        symbols='AAPL')
```

## Getting first and last ticks

We can limit the number of ticks returned with the help of ``limit()`` method<br />
\\\\
(or using ``first()`` and ``last()`` aggregations):

```
data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')
data = data[['PRICE', 'SIZE', 'COND', 'EXCHANGE']]

# get first 100 ticks
data = data.limit(100)

otp.run(data,
        start=otp.dt(2024, 2, 1, 9, 30),
        end=otp.dt(2024, 2, 1, 9, 30, 1),
        timezone='America/New_York',
        symbols='AAPL')
```

Getting last 5 ticks from the previous example:

```
# get last 5 ticks
data = data.last(5)

otp.run(data,
        start=otp.dt(2024, 2, 1, 9, 30),
        end=otp.dt(2024, 2, 1, 9, 30, 1),
        timezone='America/New_York',
        symbols='AAPL')
```

### Slice syntax

For limiting the ticks Python-like *slice* syntax is also supported with ``__getitem__()``:

```
data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')
data = data[['PRICE', 'SIZE', 'COND', 'EXCHANGE']]

# get last 100 ticks
data = data[-100:]

otp.run(data,
        start=otp.dt(2024, 2, 1, 9, 30),
        end=otp.dt(2024, 2, 1, 9, 30, 1),
        timezone='America/New_York',
        symbols='AAPL')
```

## Filtering with aggregations

Some aggregations can be used as filters too.

For example, using parameter `group_by` in ``first()`` aggregation
will output the first tick for each group:

```
data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')
data = data[['PRICE', 'SIZE', 'COND', 'EXCHANGE']]

# get first tick for each exchange
data = data.first(group_by='EXCHANGE')

otp.run(data,
        start=otp.dt(2024, 2, 1, 9, 30),
        end=otp.dt(2024, 2, 1, 9, 30, 1),
        timezone='America/New_York',
        symbols='AAPL')
```

## Splitting the data with filter

We can also return two branches after filtering with method ``where_clause()``
(or ``__getitem__()``).

The first branch contains all ticks that satisfy the condition:

```
data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')
data = data[['PRICE', 'SIZE', 'COND', 'EXCHANGE']]

# split the data flow into two branches
exchange_k, other = data[data['EXCHANGE'] == 'K']

otp.run(exchange_k,
        start=otp.dt(2024, 2, 1, 9, 30),
        end=otp.dt(2024, 2, 1, 9, 30, 1),
        timezone='America/New_York',
        symbols='AAPL')
```

And the other branch contains all ticks that do not satisfy the condition:

```
otp.run(other,
        start=otp.dt(2024, 2, 1, 9, 30),
        end=otp.dt(2024, 2, 1, 9, 30, 1),
        timezone='America/New_York',
        symbols='AAPL')
```

## Creating filters from another query

It is possible to construct filter expression dynamically
as a result of another query using ``otp.eval``.

For example, we can filter ticks with the PRICE bigger than the median price for the day:

```
data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')
data = data[['PRICE', 'SIZE', 'COND', 'EXCHANGE']]

# calculating median price for the day
median = data.agg({'MEDIAN': otp.agg.median('PRICE')})
median['WHERE'] = 'PRICE > ' + median['MEDIAN'].astype(str)

# and using it as a filter
data = data.where(otp.eval(median[['WHERE']]))

otp.run(data,
        start=otp.dt(2024, 2, 1, 9, 30),
        end=otp.dt(2024, 2, 1, 16, 0),
        timezone='America/New_York',
        symbols='AAPL')
```
