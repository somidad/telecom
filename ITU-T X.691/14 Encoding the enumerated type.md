---
publish-telecom: true
---


NOTE – (Tutorial) An enumerated type without an extension marker is encoded as if it were a constrained integer whose subtype constraint does not contain an extension marker. This means that an enumerated type will almost always in practice be encoded as a bit-field in the smallest number of bits needed to express every enumeration. In the presence of an extension marker, it is encoded as a [normally small non-negative whole number](./11.6%20Encoding%20of%20a%20normally%20small%20non-negative%20whole%20number.md) if the value is not in the extension root.

**14.1** The enumerations in the enumeration root shall be sorted into ascending order by their enumeration value, and shall then be assigned an enumeration index starting with zero for the first enumeration, one for the second, and so on up to the last enumeration in the sorted list. The extension additions (which are always defined in ascending order) shall be assigned an enumeration index starting with zero for the first enumeration, one for the second, and so on up to the last enumeration in the extension additions. ^50d51a

NOTE – Rec. ITU-T X.680 | ISO/IEC 8824-1 requires that each successive extension addition shall have a greater enumeration value than the last.

**14.2** If the extension marker is absent in the definition of the enumerated type, then the enumeration index shall be encoded. Its encoding shall be as though it were a value of a [constrained integer type](./11.5%20Encoding%20of%20a%20constrained%20whole%20number.md) for which there is no extension marker present, where the lower bound is 0 and the upper bound is the largest enumeration index associated with the type, completing this procedure.

**14.3** If the extension marker is present, then a single bit shall be added to the field-list in a bit-field of length one. The bit shall be set to 1 if the value to be encoded is not within the extension root, and zero otherwise. In the former case, the enumeration additions shall be sorted according to [14.1](14%20Encoding%20the%20enumerated%20type.md#50d51a) and the value shall be added to the field-list as a [normally small non-negative whole number](./11.6%20Encoding%20of%20a%20normally%20small%20non-negative%20whole%20number.md) whose value is the enumeration index of the additional enumeration and with "lb" set to 0, completing this procedure. In the latter case, the value shall be encoded as if the extension marker is not present, as specified in 14.2.

NOTE – There are no PER-visible constraints that can be applied to an enumerated type that are visible to these encoding rules.