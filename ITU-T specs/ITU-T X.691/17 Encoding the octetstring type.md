
NOTE – Octet strings of fixed length less than or equal to two octets are not octet-aligned. All other octet strings are octet-aligned in the ALIGNED variant. Fixed length octet strings encode with no length octets if they are shorter than 64K. For unconstrained octet strings the length is explicitly encoded (with fragmentation if necessary).

**17.1** PER-visible constraints can only constrain the length of the octetstring.

**17.2** Let the maximum number of octets in the octetstring (as determined by PER-visible constraints on the length) be "ub" and the minimum number of octets be "lb". If there is no finite maximum, we say that "ub" is unset. If there is no constraint on the minimum, then "lb" has the value zero. Let the length of the actual octetstring value to be encoded be "n" octets.

**17.3** If the type is extensible for PER encodings (see 10.3.9), then a bit-field consisting of a single bit shall be added to the field-list. The bit shall be set to 1 if the length of this encoding is not within the range of the extension root, and zero otherwise. In the former case [17.8](17%20Encoding%20the%20octetstring%20type.md#user-content-^5c795c) shall be invoked to add the length as a [semi-constrained whole number](./11.7%20Encoding%20of%20a%20semi-constrained%20whole%20number.md) to the field-list, followed by the octetstring value. In the latter case the length and value shall be encoded as if no extension is present in the constraint.

**17.4** If an extension marker is not present in the constraint specification of the octetstring type, then [17.5](17%20Encoding%20the%20octetstring%20type.md#user-content-^d11abe) to [17.8](17%20Encoding%20the%20octetstring%20type.md#user-content-^5c795c) apply.

**17.5** If the octetstring is constrained to be of zero length ("ub" equals zero), then it shall not be encoded (no additions to the field-list), completing the procedures of this clause. <a id="^d11abe"></a>

**17.6** If all values of the octetstring are constrained to be of the same length ("ub" equals "lb") and that length is less than or equal to two octets, the octetstring shall be placed in a bit-field with a number of bits equal to the constrained length "ub" multiplied by eight which shall be appended to the field-list with no length determinant, completing the procedures of this clause.

**17.7** If all values of the octetstring are constrained to be of the same length ("ub" equals "lb") and that length is greater than two octets but less than 64K, then the octetstring shall be placed in a bit-field (octet-aligned in the ALIGNED variant) with the constrained length "ub" octets which shall be appended to the field-list with no length determinant, completing the procedures of this clause. <a id="^194ec4"></a>

**17.8** If [17.5](17%20Encoding%20the%20octetstring%20type.md#user-content-^d11abe) to [17.7](17%20Encoding%20the%20octetstring%20type.md#user-content-^194ec4) do not apply, the octetstring shall be placed in a bit-field (octet-aligned in the ALIGNED variant) of length "n" octets and the procedures of [11.9](./11.9%20General%20rules%20for%20encoding%20a%20length%20determinant.md) shall be invoked to add this bit-field (octet-aligned in the ALIGNED variant) of "n" octets to the field-list, preceded by a [length determinant](./11.9%20General%20rules%20for%20encoding%20a%20length%20determinant.md) equal to "n" octets as a constrained whole number if "ub" is set, and as a semi-constrained whole number if "ub" is unset. "lb" is as determined above. <a id="^5c795c"></a>

NOTE – The fragmentation procedures may apply after 16K, 32K, 48K, or 64K octets.
