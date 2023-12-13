- NOTE 1 – (Tutorial) The procedures of this subclause are invoked when an explicit length field is needed for some part of the encoding regardless of whether the length count is bounded above (by PER-visible constraints) or not. The part of the encoding to which the length applies may be a bit string (with the length count in bits), an octet string (with the length count in octets), a known-multiplier character string (with the length count in characters), or a list of fields (with the length count in components of a sequence-of or set-of).
- NOTE 2 – (Tutorial) In the case of the ALIGNED variant if the length count is bounded above by an upper bound that is less than 64K, then the constrained whole number encoding is used for the length. For sufficiently small ranges the result is a bit-field, otherwise the unconstrained length ("n" say) is encoded into an octet-aligned bit-field in one of three ways (in order of increasing size):
	- a) ("n" less than 128) a single octet containing "n" with bit 8 set to zero;
	- b) ("n" less than 16K) two octets containing "n" with bit 8 of the first octet set to 1 and bit 7 set to zero;
	- c) (large "n") a single octet containing a count "m" with bit 8 set to 1 and bit 7 set to 1. The count "m" is one to four, and the length indicates that a fragment of the material follows (a multiple "m" of 16K items). For all values of "m", the fragment is then followed by another length encoding for the remainder of the material.
- NOTE 3 – (Tutorial) In the UNALIGNED variant, if the length count is bounded above by an upper bound that is less than 64K, then the constrained whole number encoding is used to encode the length in the minimum number of bits necessary to represent the range. Otherwise, the unconstrained length ("n" say) is encoded into a bit-field in the manner described above in Note 2.
- **11.9.1** This subclause is not invoked if, in accordance with the specification of later clauses, the value of the length determinant, "n", is fixed by the type definition (constrained by PER-visible constraints) to a value less than 64K.
- **11.9.2** This subclause is invoked for addition to the field-list of a field, or list of fields, preceded by a length determinant "n" which determines either:
	- a) the length in octets of an associated field (units are octets); or
	- b) the length in bits of an associated field (units are bits); or
	- c) the number of component encodings in an associated list of fields (units are components of a set-of or sequence-of); or
	- d) the number of characters in the value of an associated known-multiplier character string type (units are characters).
- **11.9.3** (ALIGNED variant) The procedures for the ALIGNED variant are specified in 11.9.3.1 to 11.9.3.8.4. (The procedures for the UNALIGNED variant are specified in 11.9.4.)
	- **11.9.3.1** As a result of the analysis of the type definition (specified in later clauses) the length determinant (a whole number "n") will have been determined to be either:
		- a) a normally small length with a lower bound "lb" equal to one; or
		- b) a constrained whole number with a lower bound "lb" (greater than or equal to zero), and an upper bound "ub" less than 64K; or
		- c) a semi-constrained whole number with a lower bound "lb" (greater than or equal to zero), or a constrained whole number with a lower bound "lb" (greater than or equal to zero) and an upper bound "ub" greater than or equal to 64K.
	- **11.9.3.2** The subclauses invoking the procedures of this subclause will have determined a value for "lb", the lower bound of the length (this is zero if the length is unconstrained), and for "ub", the upper bound of the length. "ub" is unset if there is no upper bound determinable from PER-visible constraints.
	- **11.9.3.3** Where the length determinant is a constrained whole number with "ub" less than 64K, then the field-list shall have appended to it the encoding of the constrained whole number for the length determinant as specified in 11.5. If "n" is non-zero, this shall be followed by the associated field or list of fields, completing these procedures. If "n" is zero there shall be no further addition to the field-list, completing these procedures.
		- NOTE 1 – For example:
		  ```
		  A ::= IA5String (SIZE (3..6))	-- Length is encoded in a 2-bit bit-field.
		  B ::= IA5String (SIZE (40000..40254))	-- Length is encoded in an 8-bit bit-field.
		  C ::= IA5String (SIZE (0..32000))	-- Length is encoded in a 2-octet 
		  				-- bit-field (octet-aligned in the ALIGNED variant).
		  D ::= IA5String (SIZE (64000))	-- Length is not encoded.
		  ```
		- NOTE 2 – The effect of making no addition in the case of "n" equals zero is that padding to an octet boundary does not occur when these procedures are invoked to add an octet-aligned-bit-field of zero length, unless required by 11.5.
	- **11.9.3.4** Where the length determinant is a normally small length and "n" is less than or equal to 64, a single-bit bit-field shall be appended to the field-list with the bit set to 0, and the value "n–1" shall be encoded as a non-negative-binary-integer into a 6-bit bit-field. This shall be followed by the associated field, completing these procedures. If "n" is greater than 64, a single-bit bit-field shall be appended to the field-list with the bit set to 1, followed by the encoding of "n" as an unconstrained length determinant followed by the associated field, according to the procedures of 11.9.3.5 to 11.9.3.8.4.
		- NOTE – Normally small lengths are only used to indicate the length of the bitmap that prefixes the extension addition values of a set or sequence type.
	- **11.9.3.5** Otherwise (unconstrained length, or large "ub"), "n" is encoded and appended to the field-list followed by the associated fields as specified below.
		- NOTE – The lower bound, "lb", does not affect the length encodings specified in 11.9.3.6 to 11.9.3.8.4.
	- **11.9.3.6** If "n" is less than or equal to 127, then "n" shall be encoded as a non-negative-binary-integer (using the procedures of 11.3) into bits 7 (most significant) to 1 (least significant) of a single octet and bit 8 shall be set to zero. This shall be appended to the field-list as a bit-field (octet-aligned in the ALIGNED variant) followed by the associated field or list of fields, completing these procedures.
		- NOTE – For example, if in the following a value of A is 4 characters long, and that of B is 4 items long:
		- ```
		  A ::= IA5String
		  B ::= SEQUENCE (SIZE (4..123456)) OF INTEGER
		  ```
		- both values are encoded with the length octet occupying one octet, and with the most significant set to 0 to indicate that the length is less than or equal to 127:
-