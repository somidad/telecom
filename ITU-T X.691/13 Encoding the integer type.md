---
publish-telecom: true
---


NOTE 1 – (Tutorial ALIGNED variant) Ranges which allow the encoding of all values into one octet or less go into a minimum-sized bit-field with no length count. Ranges which allow encoding of all values into two octets go into two octets in an octet aligned bit-field with no length count. Otherwise, the value is encoded into the minimum number of octets (using [non-negative-binary-integer](./11.3%20Encoding%20as%20a%20non-negative-binary-integer.md) or [2's complement-binary-integer](./11.4%20Encoding%20as%20a%202's-complement-binary-integer.md) encoding as appropriate) and a [length determinant](./11.9%20General%20rules%20for%20encoding%20a%20length%20determinant.md) is added. In this case, if the integer value can be encoded in less than 127 octets (as an offset from any lower bound that might be determined), and there is no finite upper and lower bound, there is a one-octet length determinant, else the length is encoded in the fewest number of bits needed. Other cases are not of any practical interest, but are specified for completeness. <a id="783559"></a>

NOTE 2 – (Tutorial UNALIGNED variant) Constrained integers are encoded in the fewest number of bits necessary to represent the range regardless of its size. Unconstrained integers are encoded as in [Note 1](13%20Encoding%20the%20integer%20type.md#783559).

**13.1** If an extension marker is present in the constraint specification of the integer type, then a single bit shall be added to the field-list in a bit-field of length one. The bit shall be set to 1 if the value to be encoded is not within the range of the extension root, and zero otherwise. In the former case, the value shall be added to the field-list as an unconstrained integer value, as specified in [13.2.4](13%20Encoding%20the%20integer%20type.md#d8f210) to [13.2.6](13%20Encoding%20the%20integer%20type.md#51fda7), completing this procedure. In the latter case, the value shall be encoded as if the extension marker is not present.

**13.2** If an extension marker is not present in the constraint specification of the integer type, then the following applies.

**13.2.1** If PER-visible constraints restrict the integer value to a single value, then there shall be no addition to the field-list, completing these procedures.

**13.2.2** If PER-visible constraints restrict the integer value to be a constrained whole number, then it shall be converted to a field according to the procedures of [11.5 (encoding of a constrained whole number)](./11.5%20Encoding%20of%20a%20constrained%20whole%20number.md), and the procedures of [13.2.5](13%20Encoding%20the%20integer%20type.md#58a8c0) to [13.2.6](13%20Encoding%20the%20integer%20type.md#51fda7) shall then be applied.

**13.2.3** If PER-visible constraints restrict the integer value to be a semi-constrained whole number, then it shall be converted to a field according to the procedures of [11.7 (encoding of a semi-constrained whole number)](./11.7%20Encoding%20of%20a%20semi-constrained%20whole%20number.md), and the procedures of [13.2.6](13%20Encoding%20the%20integer%20type.md#51fda7) shall then be applied.

**13.2.4** If PER-visible constraints do not restrict the integer to be either a constrained or a semi-constrained whole number, then it shall be converted to a field according to the procedures of [11.8 (encoding of an unconstrained whole number)](./11.8%20Encoding%20of%20an%20unconstrained%20whole%20number.md), and the procedures of [13.2.6](13%20Encoding%20the%20integer%20type.md#51fda7) shall then be applied. <a id="d8f210"></a>

**13.2.5** If the procedures invoked to encode the integer value into a field did not produce the indefinite length case (see [11.5.7.4](./11.5%20Encoding%20of%20a%20constrained%20whole%20number.md#74f748) and [11.8.2](./11.8%20Encoding%20of%20an%20unconstrained%20whole%20number.md#91684b)), then that field shall be appended to the field-list completing these procedures. <a id="58a8c0"></a>

**13.2.6** Otherwise, (the indefinite length case) the procedures of [11.9](./11.9%20General%20rules%20for%20encoding%20a%20length%20determinant.md) shall be invoked to append the field to the field-list preceded by one of the following: <a id="51fda7"></a>

- a) A constrained length determinant "len" (as determined by [11.5.7.4](./11.5%20Encoding%20of%20a%20constrained%20whole%20number.md#74f748)) if PER-visible constraints restrict the type with finite upper and lower bounds and, if the type is extensible, the value lies within the range of the extension root. The lower bound "lb" used in the length determinant shall be 1, and the upper bound "ub" shall be the count of the number of octets required to hold the range of the integer value.
- NOTE – The encoding of the value "`foo INTEGER (256..1234567) ::= 256`" would thus be encoded in the ALIGNED variant as 00xxxxxx00000000, where each 'x' represents a zero pad bit that may or may not be present depending on where within the octet the length occurs (e.g., the encoding is 00 xxxxxx 00000000 if the length starts on an octet boundary, and 00 00000000 if it starts with the two least significant bits (bits 2 and 1) of an octet).
- b) An unconstrained length determinant equal to "len" (as determined by [11.7](./11.7%20Encoding%20of%20a%20semi-constrained%20whole%20number.md) and [11.8](./11.8%20Encoding%20of%20an%20unconstrained%20whole%20number.md)) if PER-visible constraints do not restrict the type with finite upper and lower bounds, or if the type is extensible and the value does not lie within the range of the extension root.
