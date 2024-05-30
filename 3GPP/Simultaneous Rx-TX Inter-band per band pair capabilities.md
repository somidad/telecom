
There are two simultaneous Rx-Tx inter-band per band pair capabilities:

- simultaneousRxTxInterBandCAPerBandPair
- simultaneousRxTxInterBandENDCPerBandPair

The above capabilities are signaled as a bit string type. A value of each bit is determined as follows (according to 3GPP TS 38.306)

> Encoded as a bitmap with size $L \times (L – 1) / 2$, and bit N (leftmost bit is indexed as bit 0) is set to "1" if the UE supports simultaneous transmission and reception for band pair (x, y), where L is the number of band entries in the band combination, x and y are the indices of the band entry in the band combination (the first band entry is indexed as 0), x < y, and $N = x \times (2 \times L – x – 1)/2 + y – x – 1$.

The above statement can be visualized as follows:

| **x \ y**     | **band[0]** | **band[1]** | **...** | **bit[L-2]** | **band[L-1]** |
| ------------- | ----------- | ----------- | ------- | ------------ | ------------- |
| **band[0]**   | -           | bit[0]      | ...     | bit[L-3]     | bit[L-2]      |
| **band[1]**   |             | -           | ...     | bit[2L-5]    | bit[2L-4]     |
| **...**       |             |             | -       | ...          | ...           |
| **band[L-2]** |             |             |         | -            | bit[N-1]      |
| **band[L-1]** |             |             |         |              | -             |

Note that it is symmetric and the lower triangle mirrors the upper triangle.
