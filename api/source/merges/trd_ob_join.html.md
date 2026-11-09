# otp.Source.trd_ob_join

#### ``Source.trd_ob_join(ob, order_book_delay=0.0, max_levels=None, max_initialization_days=None)``

Joins trades with the prevailing order book statistics.

Appends each trade tick with size-weighted price and total size
computed over a specified number of order book levels prevailing at the time.

This method expects two sources as its input: source of trades (`self`) and source of order book ticks (`ob`).

* **Parameters:**
  * **ob** (``Source``) – The source of order book ticks.
  * **order_book_delay** (*int* *,* *float*) – The minimum number of seconds that needs to elapse between the trade and the order book state
    before the order book state can be considered for a join with the trade.
  * **max_levels** (*int*) – The number of levels of the prevailing order book to join to the trade tick.
    If not set, all levels are used.
  * **max_initialization_days** (*int*) – This parameter specifies how many days back the event processor should go in order to find
    the latest full state of the book.
    When set, this parameter takes precedence over the configuration parameter BOOKS.MAX_INITIALIZATION_DAYS.
  * **self** (*Source*)
* **Return type:**
  ``Source``

##### Examples

Add size-weighted price and total size of 5 levels of the prevailing order book to each trade:

```
>>> trd = otp.DataSource(db='CME_SAMPLE', tick_type='TRD', symbols=r'NQ\H24')
>>> trd = trd[['PRICE', 'SIZE']]
>>> ob = otp.DataSource(db='CME_SAMPLE', tick_type='PRL_FULL', symbols=r'NQ\H24')
>>> data = trd.trd_ob_join(ob, max_levels=5)
>>> data = data.limit(5)
>>> otp.run(data, date=otp.dt(2024, 2, 1))
                           Time     PRICE  SIZE  ASK_VWAP      BID_VWAP  ASK_SIZE  BID_SIZE
0 2024-02-01 00:00:01.201009991  17317.25     1   17315.0  17314.196429        20        14
1 2024-02-01 00:00:01.201009991  17317.25     1   17315.0  17314.196429        20        14
2 2024-02-01 00:00:01.201261213  17317.25     1   17315.0  17313.961538        20        13
3 2024-02-01 00:00:01.202871635  17317.25     1   17315.0  17314.275000        20        10
4 2024-02-01 00:00:02.331632419  17317.75     1   17315.0  17316.714286        20         7
```

Use parameter `order_book_delay` to join trades only with the order book state that is at least 1 second older:

```
>>> trd = otp.DataSource(db='CME_SAMPLE', tick_type='TRD', symbols=r'NQ\H24')
>>> trd = trd[['PRICE', 'SIZE']]
>>> ob = otp.DataSource(db='CME_SAMPLE', tick_type='PRL_FULL', symbols=r'NQ\H24')
>>> data = trd.trd_ob_join(ob, max_levels=5, order_book_delay=1)
>>> data = data.limit(6)
>>> otp.run(data, date=otp.dt(2024, 2, 1))
                           Time     PRICE  SIZE  ASK_VWAP   BID_VWAP  ASK_SIZE  BID_SIZE
0 2024-02-01 00:00:01.201009991  17317.25     1       NaN        NaN         0         0
1 2024-02-01 00:00:01.201009991  17317.25     1       NaN        NaN         0         0
2 2024-02-01 00:00:01.201261213  17317.25     1       NaN        NaN         0         0
3 2024-02-01 00:00:01.202871635  17317.25     1       NaN        NaN         0         0
4 2024-02-01 00:00:02.331632419  17317.75     1   17315.0  17314.475        20        10
5 2024-02-01 00:00:02.331632419  17317.75     1   17315.0  17314.475        20        10
```

##### SEE ALSO
**TRD_OB_JOIN** OneTick event processor
