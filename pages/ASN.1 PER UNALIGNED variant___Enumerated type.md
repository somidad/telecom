## Encoding
	- ### Case 1: `ENUMERATED {item0, item1}` [🔗](((6579c507-e67f-4b7e-b3ee-6ac792e1d804)))
	  id:: 6579c40f-6545-497e-9f78-5f21f5e02132
		- It is encoded as if it were `INTEGER (0..ub)` [🔗](((6579bd3a-5387-405c-be69-af1024dc8dfd))), where *ub* is the largest enumeration index.
		- ```
		  bits (msb) n-1               0 (lsb)
		            +-------------------+
		            | enumeration index |
		            +-------------------+
		  ```
	- ### Case 2: `ENUMERATED {item0, ..., itemA, itemB}` [🔗](((6579c507-7bda-42b7-bc01-4d574fd0044f)))
		- A single bit precedes, which indicates whether a value to be encoded is within the extension root or not.
		- If the bit is set to 0, then the value is within the extension root and encoded according to [case 1](((6579c40f-6545-497e-9f78-5f21f5e02132))).
		- ```
		  bits (msb)     n-1               0 (lsb)
		            +---+-------------------+
		            | 0 | enumeration index |
		            +---+-------------------+
		  ```
		- If the bit is set to 1, the value is encoded as a [normally small non-negative whole number]([[ITU-T X.691/11.6 normally small non-negative whole number]])
			- If the value is less than 64, a bit 0 precedes and the value is encoded into 6 bits
			- ```
			  bits (msb)         5           0 (lsb)
			            +---+---+--------------+
			            | 1 | 0 | value (< 64) |
			            +---+---+--------------+
			  ```
			- Otherwise, the [length determinant](((6579cc13-23e3-40ae-9270-85f099d0157b))) precedes and the value is encoded as [semi-constrained whole number]([[ITU-T X.691/11.7 Encoding of a semi-constrained whole number]])
			- ```
			  bits (msb)                                     len-1        0 (lsb)
			            +---+---+---------------------------+--------------+
			            | 1 | 1 | length (semi-constrained) | value (> 63) |
			            +---+---+---------------------------+--------------+
			  ```