
## Case 1: `ENUMERATED{item0, item1}`

It is equivalent to [ INTEGER(0..ub)](./Integer%20type.md#user-content-^9737b8) , where *ub* is equal to the number of enumerated items minus one.

## Case 2: `ENUMERATED{item0, item1, ..., itemA, itemB}`

### Case 2-1: an enumeration index is within the extension root

Encoding produces:

- a single bit, which is set to zero; and
- an enumeration index, whose encoding is equivalent to [INTEGER(0..ub, ...) with a value within the extension root](./Integer%20type.md#user-content-^9422c9).

```
bits
    +---+----------------+
    | 0 | INTEGER(0..ub) |
    +---+----------------+
```

### Case 2-2: an enumeration index is not within the extension root

#### Case 2-2-1: the number of enumeration additions is less than or equal to 63

Encoding produces:

- a single bit, which is set to one; and
- a single bit, which is set to zero; and
- 6 bits. And an enumeration index is encoded as an *unsigned integer*

```
bits          5   0
    +---+---+-------+
    | 1 | 0 | index | 
    +---+---+-------+
```

#### Case 2-2-2: the number of enumeration additions is greater than or equal to 64

Encoding produces:

- a single bit, which is set to one; and
- a single bit, which is set to one; and
- a (semi-constrained) length determinant
- an enumeration index, encoded as an *unsigned integer*

```
bits      
    +---+---+-------+--------+-------+
    | 1 | 1 | (pad) | length | index | 
    +---+---+-------+--------+-------+
```

> [!note]
> Encoding the semi-constrained length determinant is a bit complicated and the details will be updated in the future.
