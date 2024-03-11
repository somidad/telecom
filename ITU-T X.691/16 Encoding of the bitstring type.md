---
publish-telecom: true
---

NOTE – (Tutorial) Bitstrings constrained to a fixed length less than or equal to 16 bits do not cause octet alignment. Larger bitstrings are octet-aligned in the ALIGNED variant. If the length is fixed by constraints and the upper bound is less than 64K, there is no explicit length encoding, otherwise a length encoding is included which can take any of the forms specified earlier for length encodings, including fragmentation for large bit strings.

**16.1** PER-visible constraints can only constrain the length of the bitstring.

**16.2** Where there are no PER visible constraints and Rec. ITU-T X.680 | ISO/IEC 8824-1, 22.7, applies the value shall be encoded with no trailing 0 bits (note that this means that a value with no 1 bits is always encoded as an empty bit string).

**16.3** Where there is a PER visible constraint and Rec. ITU-T X.680 | ISO/IEC 8824-1, 22.7, applies (i.e. the bitstring type is defined with a "NamedBitList"), the value shall be encoded with trailing 0 bits added or removed as necessary to ensure that the size of the transmitted value is the smallest size capable of carrying this value and satisfies the effective size constraint.

**16.4** Let the maximum number of bits in the bitstring (as determined by PER-visible constraints on the length) be "ub" and the minimum number of bits be "lb". If there is no finite maximum we say that "ub" is unset. If there is no constraint on the minimum, then "lb" has the value zero. Let the length of the actual bit string value to be encoded be "n" bits.

**16.5** When a bitstring value is placed in a bit-field as specified in [16.6](16%20Encoding%20of%20the%20bitstring%20type.md#^d4c8e9) to [16.11](16%20Encoding%20of%20the%20bitstring%20type.md#^e2e8bc), the leading bit of the bitstring value shall be placed in the leading bit of the bit-field, and the trailing bit of the bitstring value shall be placed in the trailing bit of the bit-field.

**16.6** If the type is extensible for PER encodings (see 10.3.9), then a bit-field consisting of a single bit shall be added to the field-list. The bit shall be set to 1 if the length of this encoding is not within the range of the extension root, and zero otherwise. In the former case, [16.11](16%20Encoding%20of%20the%20bitstring%20type.md#^e2e8bc) shall be invoked to add the length as a [semi-constrained whole number](./11.7%20Encoding%20of%20a%20semi-constrained%20whole%20number.md) to the field-list, followed by the bitstring value. In the latter case the length and value shall be encoded as if no extension is present in the constraint. <a id="d4c8e9"></a>

**16.7** If an extension marker is not present in the constraint specification of the bitstring type, then [16.8](16%20Encoding%20of%20the%20bitstring%20type.md#^3de1cb) to [16.11](16%20Encoding%20of%20the%20bitstring%20type.md#^16.11) apply.

**16.8** If the bitstring is constrained to be of zero length ("ub" equals zero), then it shall not be encoded (no additions to the field-list), completing the procedures of this clause. <a id="3de1cb"></a>

**16.9** If all values of the bitstring are constrained to be of the same length ("ub" equals "lb") and that length is less than or equal to sixteen bits, then the bitstring shall be placed in a bit-field of the constrained length "ub" which shall be appended to the field-list with no length determinant, completing the procedures of this clause.

**16.10** If all values of the bitstring are constrained to be of the same length ("ub" equals "lb") and that length is greater than sixteen bits but less than 64K bits, then the bitstring shall be placed in a bit-field (octet-aligned in the ALIGNED variant) of length "ub" (which is not necessarily a multiple of eight bits) and shall be appended to the field-list with no length determinant, completing the procedures of this clause. <a id="d9b95b"></a>

**16.11** If [16.8](16%20Encoding%20of%20the%20bitstring%20type.md#^3de1cb)-[16.10](16%20Encoding%20of%20the%20bitstring%20type.md#^d9b95b) do not apply, the bitstring shall be placed in a bit-field (octet-aligned in the ALIGNED variant) of length "n" bits and the procedures of [11.9](./11.9%20General%20rules%20for%20encoding%20a%20length%20determinant.md) shall be invoked to add this bit-field (octet-aligned in the ALIGNED variant) of "n" bits to the field-list, preceded by a [length determinant](./11.9%20General%20rules%20for%20encoding%20a%20length%20determinant.md) equal to "n" bits as a constrained whole number if "ub" is set and is less than 64K or as a semi-constrained whole number if "ub" is unset. "lb" is as determined above. <a id="e2e8bc"></a>

NOTE – Fragmentation applies for unconstrained or large "ub" after 16K, 32K, 48K or 64K bits.
