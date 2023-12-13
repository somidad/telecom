## Encoding
	- ### Case 1: `BIT STRING (SIZE(len))` (len < 64K) [🔗](((6579c11a-282d-45ef-ade0-910e495b616d))), [🔗](((6579c11a-6476-4b14-b905-c2d66d2b74a4)))
		- *len* bits are occupied. A leading bit is added first.
		- ```
		  bits (msb) len-1      0 (lsb)
		            +------------+
		            | bit string |
		            +------------+
		  ```
	- ### Case 2: All other cases [🔗](((6579c11a-3b4a-4845-8c29-9b8b591f364f)))
		- Includes: `BIT STRING`, `BIT STRING (lb..ub)`, `BIT STRING (SIZE(len))`
		- A length determinant indicating the number of bits precedes. Then a leading bit is added first.
		- ```
		  bits (msb)          len-1      0 (lsb)
		            +--------+------------+
		            | length | bit string |
		            +--------+------------+
		  ```