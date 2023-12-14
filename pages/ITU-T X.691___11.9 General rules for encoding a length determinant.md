---
+
---
------+-------------------+
		  | 0 | 0000100 | 4 character items |
		  +---+---------+-------------------+
		        Length    Value
		  ```
	- **11.9.3.7** If "n" is greater than 127 and less than 16K, then "n" shall be encoded as a non-negative-binary-integer (using the procedures of 11.3) into bit 6 of octet one (most significant) to bit 1 of octet two (least significant) of a two-octet bit-field (octet-aligned in the ALIGNED variant) with bit 8 of the first octet set to 1 and bit 7 of the first octet set to zero. This shall be appended to the field-list followed by the associated field or list of fields, completing these procedures.
		- NOTE – If in the example of 11.9.3.6 a value of A is 130 characters long, and a value of B is 130 items long, both values are encoded with the length component occupying 2 octets, and with the two most significant bits (bits 8 and 7) of the octet set to 10 to indicate that the length is greater than 127 but less than 16K.
		- ```
		  +----+-----------------+----------------------+
		  | 00 | 000000 10000010 | 130 characters/items |
		  +----+-----------------+----------------------+
		         Length            Value
		  ```
	- **11.9.3.8** If "n" is greater than or equal to 16K, then there shall be appended to the field-list a single octet in a bit-field (octet-aligned in the ALIGNED variant) with bit 8 set to 1 and bit 7 set to 1, and bits 6 to 1 encoding the value 1, 2, 3 or 4 as a non-negative-binary-integer (using the procedures of 11.8). This single octet shall be followed by part of the associated field or list of fields, as specified below.
		- NOTE – The value of bits 6 to 1 is restricted to 1-4 (instead of the theoretical limits of 0-63) so as to limit the number of items that an implementation has to have knowledge of to a more manageable number (64K instead of 1024K).
		- **11.9.3.8.1** The value of bits 6 to 1 (1 to 4) shall be multiplied by 16K giving a count ("m" say). The choice of the integer in bits 6 to 1 shall be the maximum allowed value such that the associated field or list of fields contains more than or exactly "m" octets, bits, components or characters, as appropriate.
			- NOTE 1 – The unfragmented form handles lengths up to 16K. The fragmentation therefore provides for lengths up to 64K with a granularity of 16K.
			- NOTE 2 – If in the example of 11.9.3.6 a value of "B" is 144K + 1 (i.e., 64K + 64K + 16K + 1) items long, the value is fragmented, with the two most significant bits (bits 8 and 7) of the first three fragments set to 11 to indicate that one to four blocks each of 16K items follow, and that another length component will follow the last block of each fragment:
			- ```
			  +----+--------+-----------+----+--------+-----------+----+--------+-----------+---+---------+--------+
			  | 11 | 000100 | 64K items | 11 | 000100 | 64K items | 11 | 000001 | 16K items | 0 | 0000001 | 1 item |
			  +----+--------+-----------+----+--------+-----------+----+--------+-----------+---+---------+--------+
			         Length   Value            Length   Value            Length   Value           Length    Value
			  ```
		- **11.9.3.8.2** That part of the contents specified by "m" shall then be appended to the field-list as either:
			- a)	a single bit-field (octet-aligned in the ALIGNED variant) of "m" octets containing the first "m" octets of the associated field, for units which are octets; or
			- b)	a single bit-field (octet-aligned in the ALIGNED variant) of "m" bits containing the first "m" bits of the associated field, for units which are bits; or
			- c)	the list of fields encoding the first "m" components in the associated list of fields, for units which are components of a set-of or sequence-of types; or
			- d)	a single bit-field (octet-aligned in the ALIGNED variant) of "m" characters containing the first "m" characters of the associated field, for units which are characters.
		- **11.9.3.8.3** The procedures of 11.9 shall then be reapplied to add the remaining part of the associated field or list of fields to the field-list with a length which is a semi-constrained whole number equal to ("n" – "m") with a lower bound of zero.
			- NOTE – If the last fragment that contains part of the encoded value has a length that is an exact multiple of 16K, it is followed by a final fragment that consists only of a single octet length component set to 0.
		- **11.9.3.8.4** The addition of only a part of the associated field(s) to the field-list with reapplication of these procedures is called the fragmentation procedure.
	- **11.9.4** (UNALIGNED variant) The procedures for the UNALIGNED variant are specified in 11.9.4.1 to 11.9.4.2 (the procedures for the ALIGNED variant are specified in 11.9.3).
		- **11.9.4.1** If the length determinant "n" to be encoded is a constrained whole number with "ub" less than 64K, then ("n"–"lb") shall be encoded as a non-negative-binary-integer (as specified in 11.3) using the minimum number of bits necessary to encode the "range" ("ub" – "lb" + 1), unless "range" is 1, in which case there shall be no length encoding. If "n" is non-zero this shall be followed by an associated field or list of fields, completing these procedures. If "n" is zero there shall be no further addition to the field-list, completing these procedures.
		  id:: 6579cc13-b470-4b90-ba6a-9fb959793541
			- NOTE – If "range" satisfies the inequality $2^m < "range" \le 2^{m + 1}$, then the number of bits in the length determinant is m + 1.
		- **11.9.4.2** If the length determinant "n" to be encoded is a normally small length, or a constrained whole number with "ub" greater than or equal to 64K, or is a semi-constrained whole number, then "n" shall be encoded as specified in 11.9.3.4 to 11.9.3.8.4.
		  id:: 6579cc13-23e3-40ae-9270-85f099d0157b
			- NOTE – Thus, if "ub" is greater than or equal to 64K, the encoding of the length determinant is the same as it would be if the length were unconstrained.