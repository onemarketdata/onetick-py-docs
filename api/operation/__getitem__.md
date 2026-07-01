# otp.Column._\_getitem_\_

#### Column.\_\_getitem_\_(item)

Provides an ability to get values from future or past ticks.

- Negative values refer to past ticks
- Zero to current tick
- Positive - future ticks

Boundary values will be defaulted. For instance for `item=-1` first tick value will be defaulted
