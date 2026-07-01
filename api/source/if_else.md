# otp.Source.if_else

#### ``Source.if_else(condition, if_expr, else_expr)``

Shortcut for ``apply()`` with lambda if-else expression

* **Parameters:**
  * **condition** (``Operation``) – 
    - condition for matching ticks
  * **if_expr** (``Operation``, value) – 
    - value or Operation to set if condition is true
  * **else_expr** (``Operation``, value) – 
    - value or Operation to set if condition is false
  * **self** (*Source*)
* **Return type:**
  `Column`

##### Examples

Basic example of apply if-else to a tick flow:

```
>>> data = otp.Ticks(X=[1, 2, 3])
>>> data['Y'] = data.if_else(data['X'] > 2, 1, 0)
