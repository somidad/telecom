---
publish-telecom: true
publish-title: 
publish-path: ITUT X.691
---


NOTE – (Tutorial) A sequence type begins with a preamble which is a bit-map. If the sequence type has no extension marker, then the bit-map merely records the presence or absence of default and optional components in the type, encoded as a fixed length bit-field. If the sequence type does have an extension marker, then the bit-map is preceded by a single bit that says whether values of extension additions are actually present in the encoding. The preamble is encoded without any length determinant provided it is less than 64K bits long, otherwise a [length determinant](ITU-T%20X.691___11.9%20General%20rules%20for%20encoding%20a%20length%20determinant.md) is encoded to obtain fragmentation. The preamble is followed by the fields that encode each of the components, taken in turn. If there are extension additions, then immediately before the first one is encoded there is the encoding (as a [normally small length](ITU-T%20X.691___11.9%20General%20rules%20for%20encoding%20a%20length%20determinant.md)) of a count of the number of extension additions in the type being encoded, followed by a bit-map equal in length to this count which records the presence or absence of values of each extension addition. This is followed by the encodings of the extension additions as if each one was the value of an [open type field](../ITU-T%20X.691/11.2%20Open%20type%20fields.md).

**19.1** If the sequence type has an extension marker in the "ComponentTypeLists" or in the "SequenceType" productions, then a single bit shall first be added to the field-list in a bit-field of length one. The bit shall be one if values of extension additions are present in this encoding, and zero otherwise. (This bit is called the "extension bit" in the following text.) If there is no extension marker in the "ComponentTypeLists" or in the "SequenceType" productions, there shall be no extension bit added.

**19.2** If the sequence type has "n" components in the extension root that are marked OPTIONAL or DEFAULT, then a single bit-field with "n" bits shall be produced for addition to the field-list. The bits of the bit-field shall, taken in order, encode the presence or absence of an encoding of each optional or default component in the sequence type. A bit value of 1 shall encode the presence of the encoding of the component, and a bit value of 0 shall encode the absence of the encoding of the component. The leading bit in the preamble shall encode the presence or absence of the first optional or default component, and the trailing bit shall encode the presence or absence of the last optional or default component. ^cd19a5

**19.3** If "n" is less than 64K, the bit-field shall be appended to the field-list. If "n" is greater than or equal to 64K, then the procedures of [11.9](ITU-T%20X.691___11.9%20General%20rules%20for%20encoding%20a%20length%20determinant.md) shall be invoked to add this bit-field of "n" bits to the field-list, preceded by a [length determinant](ITU-T%20X.691___11.9%20General%20rules%20for%20encoding%20a%20length%20determinant.md) equal to "n" bits as a constrained whole number with "ub" and "lb" both set to "n".

NOTE – In this case, "ub" and "lb" will be ignored by the length procedures. These procedures are invoked here in order to provide fragmentation of a large preamble. The situation is expected to arise only rarely.

**19.4** The preamble shall be followed by the field-lists of each of the components of the sequence value which are present, taken in turn.

**19.5** For CANONICAL-PER, encodings of components marked DEFAULT shall always be absent if the value to be encoded is the default value. For BASIC-PER, encodings of components marked DEFAULT shall always be absent if the value to be encoded is the default value of a simple type (see 3.7.25), otherwise it is a sender's option whether or not to encode it.

**19.6** This completes the encoding if the extension bit is absent or is zero. If the extension bit is present and set to one, then the following procedures apply. ^433786

**19.7** Let the number of extension additions in the type being encoded be "n", then a bit-field with "n" bits shall be produced for addition to the field-list. The bits of the bit-field shall, taken in order, encode the presence or absence of an encoding of each extension addition in the type being encoded. A bit value of 1 shall encode the presence of the encoding of the extension addition, and a bit value of 0 shall encode the absence of the encoding of the extension addition. The leading bit in the bit-field shall encode the presence or absence of the first extension addition, and the trailing bit shall encode the presence or absence of the last extension addition. ^019704

NOTE – If conformance is claimed to a particular version of a specification, then the value "n" is always equal to the number of extension additions in that version.

**19.8** The procedures of [11.9](ITU-T%20X.691___11.9%20General%20rules%20for%20encoding%20a%20length%20determinant.md) shall be invoked to add this bit-field of "n" bits to the field-list, preceded by a [length determinant](ITU-T%20X.691___11.9%20General%20rules%20for%20encoding%20a%20length%20determinant.md) equal to "n" as a normally small length.

NOTE – "n" cannot be zero, as this procedure is only invoked if there is at least one extension addition being encoded.

**19.9** This shall be followed by field-lists containing the encodings of each extension addition that is present, taken in turn. Each extension addition that is a "ComponentType" (i.e., not an "ExtensionAdditionGroup") shall be encoded as if it were the value of an [open type field](../ITU-T%20X.691/11.2%20Open%20type%20fields.md) as specified in [11.2.1](../ITU-T%20X.691/11.2%20Open%20type%20fields.md#ce0e75). Each extension addition that is an "ExtensionAdditionGroup" shall be encoded as a sequence type as specified in [19.2](19%20Encoding%20the%20sequence%20type.md#cd19a5) to [19.6](19%20Encoding%20the%20sequence%20type.md#433786), which is then encoded as if it were the value of an open type field as specified in [11.2.1](../ITU-T%20X.691/11.2%20Open%20type%20fields.md#ce0e75). If all components values of the "ExtensionAdditionGroup" are missing then, the "ExtensionAdditionGroup" shall be encoded as a missing extension addition (i.e., the corresponding bit in the bit-field described in [19.7](19%20Encoding%20the%20sequence%20type.md#019704) shall be set to 0).

NOTE 1 – If an "ExtensionAdditionGroup" contains components marked OPTIONAL or DEFAULT, then the "ExtensionAdditionGroup" is prefixed with a bit-map that indicates the presence/absence of values for each component marked OPTIONAL or DEFAULT.

NOTE 2 – "RootComponentTypeList" components that are defined after the extension marker pair are encoded as if they were defined immediately before the extension marker pair.