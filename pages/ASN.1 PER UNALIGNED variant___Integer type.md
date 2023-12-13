## Encoding
	- ### Case 1: `INTEGER (lb..ub)` [🔗](((6579bd3a-2afc-4dba-94f1-acc8590b8064)))
	  id:: 6579bd3a-5387-405c-be69-af1024dc8dfd
		- *actual value - lb* is encoded as [non-negative-binary-integer]([[ITU-T X.691/11.3 Encoding as a non-negative-binary-integer]]) using the [minimum required number of bits](((6579bd3a-837a-4720-9866-09f86b0fa49a)))
		- ```
		  bits (msb) n-1        0 (lsb)
		            +------------+
		            | value - lb |
		            +------------+
		  ```
		  where n satisfies $2^{n-1} < ub - lb + 1 ≤ 2^n$.