
## Case 1: an extension marker is not present

^a4614e

Example:

```
CHOICE {
  alt0    Type0,
  alt1    Type1
}
```

Encoding produces:

- a choice index, whose encoding is equivalent to [INTEGER(0..ub)](./Integer%20type.md#user-content-^9737b8), where *ub* is equal to the number of alternatives minus one; and
- a value of chosen type

```
bits
    +-------+-------+
    | index | value |
    +-------+-------+
```

## Case 2: an extension marker is present

Example:

```
CHOICE {
  alt0    Type0,
  alt1    Type1,
  ...,
  altA    TypeA,
  altB    TypeB
}
```

### Case 2-1: a choice index is within the extension root

Encoding produces:

- a single bit, which is set to zero; and
- a choice index and a value of a chosen type, whose encoding is equivalent to [Choice type without an extension marker](Choice%20type.md#user-content-^a4614e)

```
bits
    +---+-------+-------+
    | 0 | index | value |
    +---+-------+-------+
```

### Case 2-2: a choice index is not within the extension root

#### Case 2-2-1: the number of alternative additions is less than or equal to 63

Encoding produces:

- a single bit, which is set to one; and
- a single bit; which is set to zero; and
- 6 bits. And a choice index is encoded as an *unsigned integer*; and
- a value of chosen type

```
bits          5   0
    +---+---+-------+-------+
    | 1 | 0 | index | value |
    +---+---+-------+-------+
```

#### Case 2-2-2: the number of alternative additions is greater than or equal to 64

Encoding produces:

- a single bit, which is set to one; and
- a single bit; which is set to one; and
- a (semi-constrained) length determinant; and
-  a choice index is encoded as an *unsigned integer*; and
- a value of chosen type as an open type

```
bits
    +---+---+-------+--------+-------+-------------------+
    | 1 | 1 | (pad) | length | index | value (open type) |
    +---+---+-------+--------+-------+-------------------+
```

> [!note1]
> Encoding the semi-constrained length determinant is a bit complicated and the details will be updated in the future.

> [!note2]
> Encoding the open type is a bit complicated and the details will be updated in the future.
