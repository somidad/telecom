
> [!note]
> It is assumed that the number of fields marked *OPTIONAL* or *DEFAULT* is less than 64K (65536).

## Case 1: an extension marker is not present

Example

```
SEQUENCE {
  field0    Type0,
  field1    Type1    OPTIONAL,
  field2    Type2    DEFAULT    defaultValue
}
```

Encoding produces:

- *n* bits, where *n* is equal to the number of fields marked *OPTIONAL* or *DEFAULT*. *i*th bit is set to 1 if a value is explicitly set and to be encoded. Otherwise, it is set to 0; and
- Values of each field is added and encoded as its own type definition

```
bits  0  n-1
    +--------+--------+----------+----------+
    |  mask  | field0 | (field1) | (field2) |
    +--------+--------+----------+----------+
                        (mask[0])  (mask[1])
```

## Case 2: an extension marker is present

Example

```
SEQUENCE {
  field0    Type0,
  field1    Type1    OPTIONAL,
  field2    Type2    DEFAULT    defaultValue,
  ...,
  fieldA    TypeA    OPTIONAL,
  fieldB    TypeB    OPTIONAL,
  fieldC    TypeC    DEFAULT    defaultValue,
  [[
    fieldD  TypeD
    -- Omitted
  ]]
}
```

> [!note]
> It can be considered that *ExtensionAdditionGroup* represented by `[[ ... ]]` is equivalent to: `anonymousField    SEQUENCE { ... }    OPTIONAL`. Therefore, the last part of the above example is equivalent to:
> ```
> anonymousField    SEQUENCE {
>   fieldD    TypeD
>   -- Omitted
> }
> ```

Encoding produces:

- a single bit, which is set to 1 if at least one extension addition is present. Otherwise, it is set to 0; and
- *n* bits, where *n* is equal to the number of fields marked *OPTIONAL* or *DEFAULT*. *i*th bit is set to 1 if a value is explicitly set and to be encoded. Otherwise, it is set to 0; and
- Values of each field of the extension root is added and encoded as its own type definition; and
- a (normally small) length determinant, which represent *m*, the number of extension additions; and
- *m* bits. *i*th bit is set to 1 if a value is explicitly set and to be encoded. Otherwise, it is set to 0; and
- Values of each field of the extension root is added and encoded as its own type definition as an open type

```
bits        0  n-1                                           0  m-1
    +-----+--------+--------+----------+----------+--------+--------+----------+---------+----------+---------+
    | ext |  mask  | field0 | (field1) | (field2) | length |  mask  | (fieldA) |(fieldB) | (fieldC) | (group) |
    +-----+--------+--------+----------+----------+--------+--------+----------+---------+----------+---------+
```

> [!note]
> Encoding the open type is a bit complicated and the details will be updated in the future.
