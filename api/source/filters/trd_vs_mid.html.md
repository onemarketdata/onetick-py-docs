# otp.Source.trd_vs_mid

#### ``Source.trd_vs_mid(qte, relationship_to_mid='ge', , discard_on_match=False)``

Propagates trade ticks based on the comparison of their price to the prevailing mid-quote at the time.

Mid-quote is calculated as `(ASK_PRICE + BID_PRICE) / 2`.

This method expects two sources as its input: source of trades (`self`) and source of quotes (`qte`).
Ticks of trades source should have the **PRICE** field,
ticks of `qte` source should have the **ASK_PRICE** and **BID_PRICE** fields.

* **Parameters:**
  * **qte** (``Source``) – The source of quotes.
  * **relationship_to_mid** (*str*) – 

    Relationship to check between the price of the trade and the prevailing mid-quote.
    Supported values:
    * `lt` (less),
    * `le` (less or equal),
    * `eq` (equal),
    * `ne` (not equal),
    * `ge` (greater or equal),
    * `gt` (greater).

    Default: `ge`.
  * **discard_on_match** (*bool*) – If this parameter is `False` (default), only ticks that match the filter will be propagated.
    Otherwise ticks that match the filter will be discarded.
  * **self** (*Source*)
* **Return type:**
  ``Source``

##### Examples

Propagate only the trades with price greater or equal to the prevailing mid-quote:

```
>>> trd = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> trd = trd[['PRICE', 'SIZE']]
>>> qte = otp.DataSource('US_COMP_SAMPLE', tick_type='QTE', symbols='AAPL')
>>> qte = qte[['ASK_PRICE', 'BID_PRICE']]
>>> data = trd.trd_vs_mid(qte)
>>> data = data.limit(5)
>>> otp.run(data, date=otp.dt(2024, 2, 1), timezone='America/New_York')
                           Time   PRICE  SIZE
0 2024-02-01 04:00:00.008283417  186.50     6
1 2024-02-01 04:00:00.012928231  185.68    11
2 2024-02-01 04:00:00.012930606  185.68    10
3 2024-02-01 04:00:00.012947024  185.68    23
4 2024-02-01 04:00:00.012987210  185.72     5
```

Propagate only the trades with price below the prevailing mid-quote:

```
>>> trd = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> trd = trd[['PRICE', 'SIZE']]
>>> qte = otp.DataSource('US_COMP_SAMPLE', tick_type='QTE', symbols='AAPL')
>>> qte = qte[['ASK_PRICE', 'BID_PRICE']]
>>> data = trd.trd_vs_mid(qte, 'lt')
>>> data = data.limit(5)
>>> otp.run(data, date=otp.dt(2024, 2, 1), timezone='America/New_York')
                           Time   PRICE  SIZE
0 2024-02-01 04:00:00.008290927  185.59     1
1 2024-02-01 04:00:00.008291153  185.49   107
2 2024-02-01 04:00:00.010381671  185.49     1
3 2024-02-01 04:00:00.011224206  185.50     2
4 2024-02-01 04:00:00.011671193  185.50     1
```

##### SEE ALSO
**TRD_VS_MID** OneTick event processor
