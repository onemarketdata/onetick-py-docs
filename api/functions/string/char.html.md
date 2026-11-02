# otp.ops.char

### ``char(value, utf8=False)``

Returns a 1-character string with the character
corresponding to the ASCII or UTF-8 code passed as a parameter `value`.

* **Parameters:**
  * **value** (int, ``Operation``)
  * **utf8** (*bool*)
* **Return type:**
  ``Operation``

##### Examples

Get the string by ASCII code:

```
>>> data = otp.Tick(A=otp.ops.char(78))
>>> otp.run(data)
        Time   A
0 2003-12-01   N
```

Get the string by ASCII code for each value in a column:

```
>>> data = otp.Ticks(A=list(range(65, 79)))
>>> data['CHAR'] = otp.ops.char(data['A'])
>>> otp.run(data)
                      Time   A  CHAR
0  2003-12-01 00:00:00.000  65     A
1  2003-12-01 00:00:00.001  66     B
2  2003-12-01 00:00:00.002  67     C
3  2003-12-01 00:00:00.003  68     D
4  2003-12-01 00:00:00.004  69     E
5  2003-12-01 00:00:00.005  70     F
6  2003-12-01 00:00:00.006  71     G
7  2003-12-01 00:00:00.007  72     H
8  2003-12-01 00:00:00.008  73     I
9  2003-12-01 00:00:00.009  74     J
10 2003-12-01 00:00:00.010  75     K
11 2003-12-01 00:00:00.011  76     L
12 2003-12-01 00:00:00.012  77     M
13 2003-12-01 00:00:00.013  78     N
```

Use parameter `utf8` to support UTF-8 codes:

```
>>> data = otp.Ticks(A=list(range(200, 210)))
>>> data['CHAR'] = otp.ops.char(data['A'], utf8=True)
>>> otp.run(data, encoding='utf-8')
                     Time    A  CHAR
0 2003-12-01 00:00:00.000  200     È
1 2003-12-01 00:00:00.001  201     É
2 2003-12-01 00:00:00.002  202     Ê
3 2003-12-01 00:00:00.003  203     Ë
4 2003-12-01 00:00:00.004  204     Ì
5 2003-12-01 00:00:00.005  205     Í
6 2003-12-01 00:00:00.006  206     Î
7 2003-12-01 00:00:00.007  207     Ï
8 2003-12-01 00:00:00.008  208     Ð
9 2003-12-01 00:00:00.009  209     Ñ
```

##### SEE ALSO
**CHAR** OneTick function

**CHAR_UTF8** OneTick function

