# otp.Source.trd_quote_join

#### ``Source.trd_quote_join(qte, quote_delay=0.0, go_back_to_first_quote=0.0)``

Joins trades with prevailing quotes.

Appends each trade tick with all fields of the prevailing quote tick.

This method expects two sources as its input: source of trades (`self`) and source of quotes (`qte`).

Fields in the output ticks are prefixed with the name of the source they came from:
fields from trades source are prefixed with `TRD.`, fields from `qte` source are prefixed with `QTE.`.
Also field **QTE.TIMESTAMP** with the timestamp of the joined quote is added.

* **Parameters:**
  * **qte** (``Source``) – The source of quotes.
  * **quote_delay** (*int* *,* *float*) – The minimum number of seconds that needs to elapse between the trade and the quote
    before the quote can be considered for a join with the trade.
  * **go_back_to_first_quote** (*int* *,* *float*) – Specifies how far back (in seconds) to look for an existing quote
    when the first trade precedes the first quote.
  * **self** (*Source*)
* **Return type:**
  ``Source``

##### Examples

Add fields of the prevailing quote to each trade:

```
>>> trd = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> trd = trd[['PRICE', 'SIZE']]
>>> qte = otp.DataSource('US_COMP_SAMPLE', tick_type='QTE', symbols='AAPL')
>>> qte = qte[['ASK_PRICE', 'BID_PRICE']]
>>> data = trd.trd_quote_join(qte)
>>> data = data.limit(5)
>>> otp.run(data, date=otp.dt(2024, 2, 1), timezone='America/New_York')
                           Time  TRD.PRICE  TRD.SIZE                 QTE.TIMESTAMP  QTE.ASK_PRICE  QTE.BID_PRICE
0 2024-02-01 04:00:00.008283417     186.50         6 2024-02-01 04:00:00.007607483         187.02         185.49
1 2024-02-01 04:00:00.008290927     185.59         1 2024-02-01 04:00:00.007607483         187.02         185.49
2 2024-02-01 04:00:00.008291153     185.49       107 2024-02-01 04:00:00.007607483         187.02         185.49
3 2024-02-01 04:00:00.010381671     185.49         1 2024-02-01 04:00:00.010349268         185.80         185.45
4 2024-02-01 04:00:00.011224206     185.50         2 2024-02-01 04:00:00.010686602         185.80         185.45
```

Use parameter `quote_delay` to join trades only with the quotes that are at least 1 millisecond older:

```
>>> trd = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> trd = trd[['PRICE', 'SIZE']]
>>> qte = otp.DataSource('US_COMP_SAMPLE', tick_type='QTE', symbols='AAPL')
>>> qte = qte[['ASK_PRICE', 'BID_PRICE']]
>>> data = trd.trd_quote_join(qte, quote_delay=0.001)
>>> data = data.limit(5)
>>> otp.run(data, date=otp.dt(2024, 2, 1), timezone='America/New_York')
                           Time  TRD.PRICE  TRD.SIZE                 QTE.TIMESTAMP  QTE.ASK_PRICE  QTE.BID_PRICE
0 2024-02-01 04:00:00.008283417     186.50         6 2024-02-01 04:00:00.006738266         187.02         185.45
1 2024-02-01 04:00:00.008290927     185.59         1 2024-02-01 04:00:00.006738266         187.02         185.45
2 2024-02-01 04:00:00.008291153     185.49       107 2024-02-01 04:00:00.006738266         187.02         185.45
3 2024-02-01 04:00:00.010381671     185.49         1 2024-02-01 04:00:00.008713028         185.80         185.45
4 2024-02-01 04:00:00.011224206     185.50         2 2024-02-01 04:00:00.008713028         185.80         185.45
```

##### SEE ALSO
**TRD_QUOTE_JOIN** OneTick event processor
