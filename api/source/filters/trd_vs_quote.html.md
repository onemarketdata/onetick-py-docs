# otp.Source.trd_vs_quote

#### ``Source.trd_vs_quote(qte, relationship_to_quote='ge', side='ask', , discard_on_match=False)``

Propagates trade ticks based on the comparison of their price
to either the prevailing bid price or the prevailing ask price at the time.

This method expects two sources as its input: source of trades (`self`) and source of quotes (`qte`).
Ticks of trades source should have the **PRICE** field,
ticks of `qte` source should have the **ASK_PRICE** and **BID_PRICE** fields.

* **Parameters:**
  * **qte** (``Source``) – The source of quotes.
  * **relationship_to_quote** (*str*) – 

    Relationship to check between the price of the trade and the prevailing quote price.
    Supported values:
    * `lt` (less),
    * `le` (less or equal),
    * `eq` (equal),
    * `ne` (not equal),
    * `ge` (greater or equal),
    * `gt` (greater).

    Default: `ge`.
  * **side** (*str*) – 

    Specifies whether the price of the trade is compared to the bid price (`bid`)
    or to the ask price (`ask`).

    Default: `ask`.
  * **discard_on_match** (*bool*) – If this parameter is False (default), only ticks that match the filter will be propagated.
    Otherwise ticks that match the filter will be discarded.
  * **self** (*Source*)
* **Return type:**
  ``Source``

##### Examples

Propagate only the trades that were done at the prevailing ask price:

```
>>> trd = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> trd = trd[['PRICE', 'SIZE']]
>>> qte = otp.DataSource('US_COMP_SAMPLE', tick_type='QTE', symbols='AAPL')
>>> qte = qte[['ASK_PRICE', 'BID_PRICE']]
>>> data = trd.trd_vs_quote(qte, 'eq')
>>> data = data.limit(5)
>>> otp.run(data, date=otp.dt(2024, 2, 1), timezone='America/New_York')
                           Time   PRICE  SIZE
0 2024-02-01 04:00:02.254772762  185.98    26
1 2024-02-01 04:03:25.351156225  185.89   122
2 2024-02-01 04:03:25.351157846  185.89   200
3 2024-02-01 04:03:25.351824270  185.90    17
4 2024-02-01 04:03:25.351876143  185.90    89
```

Propagate only the trades that were done at the prevailing bid price:

```
>>> trd = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> trd = trd[['PRICE', 'SIZE']]
>>> qte = otp.DataSource('US_COMP_SAMPLE', tick_type='QTE', symbols='AAPL')
>>> qte = qte[['ASK_PRICE', 'BID_PRICE']]
>>> data = trd.trd_vs_quote(qte, 'eq', side='bid')
>>> data = data.limit(5)
>>> otp.run(data, date=otp.dt(2024, 2, 1), timezone='America/New_York')
                           Time   PRICE  SIZE
0 2024-02-01 04:00:00.008291153  185.49   107
1 2024-02-01 04:03:25.351092936  185.88   100
2 2024-02-01 04:03:25.351109492  185.88    25
3 2024-02-01 04:03:25.351546823  185.88   648
4 2024-02-01 04:03:25.351553003  185.88   117
```

Use parameter `discard_on_match` to propagate only the trades
that were done at the price different from the prevailing ask price:

```
>>> trd = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> trd = trd[['PRICE', 'SIZE']]
>>> qte = otp.DataSource('US_COMP_SAMPLE', tick_type='QTE', symbols='AAPL')
>>> qte = qte[['ASK_PRICE', 'BID_PRICE']]
>>> data = trd.trd_vs_quote(qte, 'eq', discard_on_match=True)
>>> data = data.limit(5)
>>> otp.run(data, date=otp.dt(2024, 2, 1), timezone='America/New_York')
                           Time   PRICE  SIZE
0 2024-02-01 04:00:00.008283417  186.50     6
1 2024-02-01 04:00:00.008290927  185.59     1
2 2024-02-01 04:00:00.008291153  185.49   107
3 2024-02-01 04:00:00.010381671  185.49     1
4 2024-02-01 04:00:00.011224206  185.50     2
```

##### SEE ALSO
**TRD_VS_QUOTE** OneTick event processor
