## Encoding
	- ### Case 1: `OCTET STRING (SIZE(len))` (len < 64K) [🔗](((6579c260-f939-4603-8e8d-42c726807ab2))), [🔗](((6579c260-46db-49b5-8831-fda51e0086c4)))
		- *len* octets are occupied.
		- ```
		  bits (msb) 8*len-1      0 (lsb)
		            +--------------+
		            | octet string |
		            +--------------+
		  ```
	- ### Case 2: All other cases [🔗](((6579c260-c662-4ab4-929b-13b6308cbbac)))
		- A length determinant indicating the number of octets precedes. Then a leading bit is added first.
		- ```
		  bits (msb)          8*len-1      0 (lsb)
		            +--------+--------------+
		            | length | octet string |
		            +--------+--------------+
		  ```