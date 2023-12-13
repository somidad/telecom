## Encoding
	- ### Case 1: `OCTET STRING (SIZE(len))` (len < 64K) [🔗](((6579c260-f939-4603-8e8d-42c726807ab2))), [🔗](((6579c260-46db-49b5-8831-fda51e0086c4)))
		- *len* octets are occupied.
		- ```
		  bits (msb) 8*len-1      0 (lsb)
		            +--------------+
		            | octet string |
		            +--------------+
		  ```
	- ### Case 2: `OCTET STRING (lb..ub)` (ub < 64K) [🔗](((6579c260-c662-4ab4-929b-13b6308cbbac)))
		- A [length constrained (constrained whole number)](((6579cc13-b470-4b90-ba6a-9fb959793541))) indicating the number of octets precedes.
		- ```
		  bits (msb)                        8*len-1      0 (lsb)
		            +----------------------+--------------+
		            | length (constrained) | octet string |
		            +----------------------+--------------+
		  ```
	- ### Case 2: All other cases [🔗](((6579c260-c662-4ab4-929b-13b6308cbbac)))
		- Includes: `OCTET STRING`, `OCTET STRING (lb..ub)` (ub ≥ 64K), `OCTET STRING (SIZE(len))` (len ≥ 64K)
		- A [length determinant (semi-constrained whole number)](((6579d00e-653f-4cc2-bf2f-c4521f123e96))) indicating the number of octets precedes.
		- ```
		  bits (msb)                             8*len-1      0 (lsb)
		            +---------------------------+--------------+
		            | length (semi-constrained) | octet string |
		            +---------------------------+--------------+
		  ```