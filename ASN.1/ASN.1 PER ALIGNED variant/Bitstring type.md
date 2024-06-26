
## Case 1: `BIT STRING(SIZE(n))`

> [!note]
> The length *n* is less than 64K (65536).

### Case 1-1: *n* is less than or equal to 16

Encoding produces *n* bits. And a bit string value is written with the leading bit first.

```
bits  0      n-1
    +------------+
    | bit string |
    +------------+
```

### Case 1-2: *n* is less than 64K (65536)

Encoding produces *n* bits and it is octet-aligned, which begins on an octet boundary. And a bit string value is written with the leading bit first.

```
bits          0      n-1
    +-------+------------+
    | (pad) | bit string |
    +-------+------------+
```

## Case 2: `BIT STRING(SIZE(lb..ub))`

> [!note]
> It is assumed that the lower bound *lb* is less than the upper bound *ub* and *ub* is less than 64K (65536).

Encoding produces:

- a (constrained) length determinant; and
- a bit string value with the leading bit first

```
bits                                      0    len-1
    +-------+---------------------------+------------+
    | (pad) | length (constrained) - lb | bit string |
    +-------+---------------------------+------------+
```


## Case 3: `BIT STRING`

Encoding produces:

- a (semi-constrained) length determinant; and
- a bit string value with the leading bit first

```
bits
    +-------+---------------------------+------------+
    | (pad) | length (semi-constrained) | bit string |
    +-------+---------------------------+------------+
```

> [!note]
> Encoding the semi-constrained length determinant is a bit complicated and the details will be updated in the future.
