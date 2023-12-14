---
+
---
-----------+
	            | 0 | value (< 64) |
	            +---+--------------+
	  ```
- **11.6.2** If "n" is greater than or equal to 64, a single-bit bit-field with the bit set to 1 shall be appended to the field-list. The value "n" shall then be encoded as a [semi-constrained whole number]([[ITU-T X.691/11.7 Encoding of a semi-constrained whole number]]) with "lb" equal to 0 and the procedures of [11.9]([[ITU-T X.691/11.9 General rules for encoding a length determinant]]) shall be invoked to add it to the field-list preceded by a [length determinant](((6579cc13-23e3-40ae-9270-85f099d0157b))).
	- > Note: The following illustration is not present in the original specification.
	- ```
	  bits (msb)              len-1        0 (lsb)
	            +---+--------+--------------+
	            | 1 | length | value (> 63) |
	            +---+--------+--------------+
	  ```