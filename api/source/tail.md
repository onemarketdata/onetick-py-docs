# otp.Source.tail (jupyter)

#### ``Source.tail(n=5, **kwargs)``

*Executes the query* and returns last `n` ticks as a pandas dataframe.

It is useful in the Jupyter case when you want to observe last `n` values.

* **Parameters:**
  * **n** (*int*) – number of ticks to return
  * **kwargs** – parameters will be passed to ``otp.run``
  * **self** (*Source*)
* **Return type:**
  `DataFrame`

##### Examples
