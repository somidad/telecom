
## Case 1: `OCTET STRING(SIZE(n))`

> [!note]
> The length *n* is less than 64K (65536).

### Case 1-1: *n* is less than or equal to 2

Encoding produces *n* octets. And an octet string value is written.

```
bits  0      8*n-1
    +--------------+
    | octet string |
    +--------------+
```

### Case 1-2: *n* is less than 64K (65536)

Encoding produces *n* octets and it is octet-aligned, which begins on an octet boundary. And an octet string value is written.

```
bits          0      8*n-1
    +-------+--------------+
    | (pad) | octet string |
    +-------+--------------+
```

## Case 2: `OCTET STRING(SIZE(lb..ub))`

> [!note]
> It is assumed that the lower bound *lb* is less than the upper bound *ub* and *ub* is less than 64K (65536).

Encoding produces:

- a (constrained) length determinant; and
- an octet string value

```
bits                                      0    8*len-1
    +-------+---------------------------+--------------+
    | (pad) | length (constrained) - lb | octet string |
    +-------+---------------------------+--------------+
```


## Case 3: `OCTET STRING`

Encoding produces:

- a (semi-constrained) length determinant; and
- an octet string value

```
bits
    +-------+---------------------------+--------------+
    | (pad) | length (semi-constrained) | octet string |
    +-------+---------------------------+--------------+
```

> [!note]
> Encoding the semi-constrained length determinant is a bit complicated and the details will be updated in the future.
