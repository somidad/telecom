
## Case 1: `SEQUENCE (SIZE(lb..ub)) OF Type`

> [!note]
> It is assumed that *lb* is less than *ub* and *ub* is less than 64K (65536).

Let *range* be *ub* - *lb* + 1.

### Case 1-1: *range* is less than or equal to 255

Encoding produces:

- *n* bits, where $2^{n-1} \lt range \le 2^{n}$. And a *length* - *lb* is encoded as an *unsigned integer*
- values of *length* items are encoded as its own type definition

```
bits  n-1       0
    +-------------+----------+-----+-----------------+
    | length - lb | value[0] | ... | value[length-1] |
    +-------------+----------+-----+-----------------+
```

### Case 1-2: *range* is equal to 256

Encoding produces:

- *8* bits and it is octet-aligned, which begins on an octet boundary. And a *length* - *lb* is encoded as an *unsigned integer*
- values of *length* items are encoded as its own type definition

```
bits          7         0
    +-------+-------------+----------+-----+-----------------+
    | (pad) | length - lb | value[0] | ... | value[length-1] |
    +-------+-------------+----------+-----+-----------------+
```

### Case 1-3: *range* is less than 64K (65536)

Encoding produces:

- *16* bits and it is octet-aligned, which begins on an octet boundary. And a *length* - *lb* is encoded as an *unsigned integer*
- values of *length* items are encoded as its own type definition

```
bits          15             0
    +-------+------------------+----------+-----+-----------------+
    | (pad) |   length - lb    | value[0] | ... | value[length-1] |
    +-------+------------------+----------+-----+-----------------+
```
