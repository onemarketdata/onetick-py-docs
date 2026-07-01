# otp.oqd.OHLCV

### ``class OHLCV(exch='all', start=utils.adaptive, end=utils.adaptive, symbol=utils.adaptive)``

Bases: ``Source``

OneQuantData™ source to retrieve a time series of unadjusted
prices for a symbol for one particular pricing exchange of daily OHLCV data.
Output ticks have fields: OPEN, HIGH, LOW, CLOSE, VOLUME, CURRENCY, EXCH.

* **Parameters:**
  * **exch** (*str* *,*  *'all'* *,*  *'main'* *,* *default=all*) – 

    The OneQuantData exchange code for the desired price series. Possible values:
    - ’all’
      : return data for all exchanges;
    - ’main’
      : return data main pricing exchange;
    - any other string value will treated as exchange name to filter data.

    Default: ‘all’.
