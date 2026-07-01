# otp.Source.transpose

#### ``Source.transpose(inplace=False, direction='rows', n=None)``

Data transposing.
The main idea is joining many ticks into one or splitting one tick to many.

* **Parameters:**
  * **inplace** (*bool* *,* *default=False*) – if True method will modify current object,
    otherwise it will return modified copy of the object.
  * **direction** ( *'rows'* *,*  *'columns'* *,* *default='rows'*) – 
    - rows: join certain input ticks (depending on other parameters) with preceding ones.
      : Fields of each tick will be added to the output tick and their names will be suffixed
        with **\_K** where **K** is the positional number of tick (starting from 1) in reverse order.
        So fields of current tick will be suffixed with **\_1**, fields of previous tick will be
        suffixed with **\_2** and so on.
    - columns: the operation is opposite to rows. It splits each input tick to several
      : output ticks. Each input tick must have fields with names suffixed with **\_K**
        where **K** is the positional number of tick (starting from 1) in reverse order.
  * **n** (*Optional* **[*int* *]* *,* *default=None*) – must be specified only if `direction` is ‘rows’.
    Joins every **n** number of ticks with **n-1** preceding ticks.
  * **self** (*Source*)
* **Returns:**
  * If `inplace` parameter is True method will return None,
  * *otherwise it will return modified copy of the object.*
* **Return type:**
  `Source` | None

##### Examples

Merging two ticks into one.

