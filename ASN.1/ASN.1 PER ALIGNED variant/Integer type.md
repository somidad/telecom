
> [!note]
> It is assumed that *ub* is greater than *lb*.

## Case 1: `INTEGER(lb..ub)`

^9737b8

Let:

- *n* be a value to be encoded
- *range* be *ub* - *lb* + 1

### Case 1-1: *range* is less than or equal to 256

Encoding produces *m* bits, where $2^{m-1} \lt range \le 2^{m}$. And a value *n* - *lb* is encoded as an *unsigned integer*.

```
bits  m-1  0
    +--------+
    | n - lb |
    +--------+
```

### Case 1-2: *range* is equal to 256

Encoding produces 8 bits and it is octet-aligned, which begins on an octet boundary. And a value *n* - *lb* is encoded as an *unsigned integer*.

```
bits          7    0
    +-------+--------+
    | (pad) | n - lb |
    +-------+--------+
```

### Case 1-3: *range* is less than or equal to 64K (65536)

Encoding produces 16 bits and it is octet-aligned, which begins on an octet boundary, And a value *n* - *lb* is encoded as an *unsigned integer*.

```
bits          15         0
    +-------+--------------+
    | (pad) |    n - lb    |
    +-------+--------------+
```

### Case 1-4: *range* is greater than 64K (65536)

Let *l* be the number of octets, where $8^{l-1} \lt range \le 8^{l}$.

> [!note]
> It is assumed that *l* is less than 64K (65536).

#### Case 1-4-1: *l* is less than 255

Encoding produces:

- *k* bits, where $2^{k-1} \lt l \le 2^{k}$. And a value *l* -1 is encoded as an *unsigned integer*; and
- *l* octets and it is octet-aligned, which begins on an octet boundary. And a value *n* - *lb* is encoded as an *unsigned integer*

```
bits  k-1 0           8^{l}-1  0
    +-------+-------+------------+
    | l - 1 | (pad) |   n - lb   |
    +-------+-------+------------+
```

#### Case 1-4-2: *l* is equal to 256

Encoding produces:

- 8 bits and it is octet-aligned, which begins on an octet boundary. And a value *l* -1 is encoded as an *unsigned integer*; and
- *l* octets and it is octet-aligned. And a value *n* - *lb* is encoded as an *unsigned integer*

```
bits          7   0   8^{l}-1  0
    +-------+-------+------------+
    | (pad) | l - 1 |   n - lb   |
    +-------+-------+------------+
```

#### Case 1-4-3: *l* is less than or equal to 64K (65536)

Encoding produces:

- 16 bits and it is octet-aligned, which begins on an octet boundary, And a value *ㅣ* - 1 is encoded as an *unsigned integer*; and
- *l* octets and it is octet-aligned. And a value *n* - *lb* is encoded as an *unsigned integer*

```
bits          15         0   8^{l}-1  0
    +-------+--------------+------------+
    | (pad) |    l - 1     |   n - lb   |
    +-------+--------------+------------+
```

## Case 2: `INTEGER(lb..ub, ...)`

### Case 2-1: *n* is within the extension root

^9422c9

Encoding produces a single bit, which is set to zero. And a value *n* is encoded as if it is `INTEGER(lb..ub)`.

```
bits
    +---+-----------------+
    | 0 | INTEGER(lb..ub) |
    +---+-----------------+
```

### Case 2-2: *n* is not within the extension root

Encoding produces:

- a single bit, which is set to one; and
- a (unconstrained) length determinant, where $2^{length-1} \lt value \le 2^{length}$; and
- a value, encoded as an *unsigned integer*

```
bits
    +---+-------+--------+-------+
    | 1 | (pad) | length | value |
    +---+-------+--------+-------+
```

> [!note]
> Encoding the unconstrained length determinant is a bit complicated and the details will be updated in the future.
