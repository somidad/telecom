---
publish-telecom: true
publish-title: 
publish-path: ITU-T X.691
---


NOTE – (Tutorial) A choice type is encoded by encoding an index specifying the chosen alternative. This is encoded as for a [constrained integer](./11.5%20Encoding%20of%20a%20constrained%20whole%20number.md) (unless the extension marker is present in the choice type, in which case it is a [normally small non-negative whole number](./11.6%20Encoding%20of%20a%20normally%20small%20non-negative%20whole%20number.md)) and would therefore typically occupy a fixed length bit-field of the minimum number of bits needed to encode the index. (Although it could in principle be arbitrarily large.) This is followed by the encoding of the chosen alternative, with alternatives that are extension additions encoded as if they were the value of an [open type field](./11.2%20Open%20type%20fields.md). Where the choice has only one alternative, there is no encoding for the index.

**23.1** Encoding of choice types are not affected by PER-visible constraints.

**23.2** Each component of a choice has an index associated with it which has the value zero for the first alternative in the root of the choice (taking the alternatives in the canonical order specified in Rec. ITU-T X.680 | ISO/IEC 8824-1, 8.6), one for the second, and so on up to the last component in the extension root of the choice. An index value is similarly assigned to each "NamedType" within the "ExtensionAdditionAlternativesList", starting with 0 just as with the components of the extension root. Let "n" be the value of the largest index in the root.

NOTE – Rec. ITU-T X.680 | ISO/IEC 8824-1, 29.7, requires that each successive extension addition shall have a greater tag value than the last added to the "ExtensionAdditionAlternativesList".

**23.3** For the purposes of canonical ordering of choice alternatives that contain an untagged choice, each untagged choice type shall be ordered as though it has a tag equal to that of the smallest tag in the extension root of either that choice type or any untagged choice types nested within.

**23.4** If the choice has only one alternative in the extension root, there shall be no encoding for the index if that alternative is chosen.

**23.5** If the choice type has an extension marker in the "AlternativeTypeLists" production, then a single bit shall first be added to the field-list in a bit-field of length one. The bit shall be 1 if a value of an extension addition is present in the encoding, and zero otherwise. (This bit is called the "extension bit" in the following text.) If there is no extension marker in the "AlternativeTypeLists" production, there shall be no extension bit added.

**23.6** If the extension bit is absent, then the choice index of the chosen alternative shall be encoded into a field according to the procedures of [clause 13](./13%20Encoding%20the%20integer%20type.md) as if it were a value of an integer type (with no extension marker in its subtype constraint) constrained to the range 0 to "n", and that field shall be appended to the field-list. This shall then be followed by the fields of the chosen alternative, completing the procedures of this clause.

**23.7** If the extension bit is present and the chosen alternative lies within the extension root, the choice index of the chosen alternative shall be encoded as if the extension marker is absent, according to the procedure of [clause 13](./13%20Encoding%20the%20integer%20type.md).  This shall then be followed by the fields of the chosen alternative, completing the procedures of this clause.

**23.8** If the extension bit is present and the chosen alternative does not lie within the extension root, the choice index of the chosen alternative shall be encoded as a [normally small non-negative whole number](./11.6%20Encoding%20of%20a%20normally%20small%20non-negative%20whole%20number.md) with "lb" set to 0 and that field shall be appended to the field-list. This shall then be followed by a field-list containing the encoding of the chosen alternative encoded as if it were the value of an [open type field](./11.2%20Open%20type%20fields.md) as specified in [11.2](./11.2%20Open%20type%20fields.md), completing the procedures of this clause.

NOTE – Version brackets in the definition of choice extension additions have no effect on how "ExtensionAdditionAlternatives" are encoded.

