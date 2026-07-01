# otp.qcut

### ``qcut(column, q, labels=None)``

Quantile-based discretization function (mimics `pandas.qcut`).

* **Parameters:**
  * **column** (``Column``) – Column with numeric data used to build bins.
  * **q** (*int* *or* *list* **[*float* *]*) – 

    When list[float] - array of quantiles, e.g. [0, .25, .5, .75, 1.] for quartiles.
