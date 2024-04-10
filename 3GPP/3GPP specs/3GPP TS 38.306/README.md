
### 4.2.7 Physical layer parameters

#### 4.2.7.2 BandNR parameters

***channelBWs-DL*** <a id="^86013d"></a>

- Per Band
- Mandatory: Yes
- FDD-TDD DIFF: N/A
- FR1-FR2 DIFF: N/A

Indicates for each subcarrier spacing the UE supported channel bandwidths. Absence of the *channelBWs-DL* (without suffix) for a band or absence of specific scs-XXkHz entry for a supported subcarrier spacing means that the UE supports the channel bandwidths among [5, 10, 15, 20, 25, 30, 40, 50, 60, 80, 100] and [50, 100, 200] that were defined in clause 5.3.5 of TS 38.101-1 version 15.7.0 and TS 38.101-2 version 15.7.0 for the given band or the specific SCS entry. For IAB-MT, to determine whether the IAB-MT supports a channel bandwidth of 100 MHz, the network checks *channelBW-DL-IAB-r16*.  
For FR1, the bits in *channelBWs-DL* (without suffix) starting from the leading / leftmost bits indicate 5, 10, 15, 20, 25, 30, 40, 50, 60 and 80MHz. For FR2, the bits in *channelBWs-DL* (without suffix) starting from the leading / leftmost bit indicate 50, 100 and 200MHz. The third /rightmost bit (for 200MHz) shall be set to 1. For IAB-MT the third / rightmost bit (for 200MHz) is ignored. To determine whether the IAB-MT supports a channel bandwidth of 200 MHz, the network checks *channelBW-DL-IAB-r16*.  
For FR1, the leading / leftmost bit in *channelBWs-DL-v1590* indicates 70MHz, the second leftmost bit indicates 45MHz, the third leftmost bit indicates 35MHz, the fourth leftmost bit indicates 100MHz and all the remaining bits in *channelBWs-DL-v1590* shall be set to 0. The fourth leftmost bit (for 100MHz) is not applicable for bands n41, n48, n77, n78, n79 and n90 as defined in TS 38.101-1. For each band, RedCap UEs shall indicate supporting the maximum of those channel bandwidths that are less than or equal to 20 MHz for FR1 and less than or equal to 100 Mhz for FR2, taking restrictions in TS 38.101-1 and TS 38.101-2 into consideration. For each band, NTN capable UEs shall indicate the supported channel bandwidths for FR1, taking restrictions in TS 38.101-5 into consideration.

This feature is applicable only for FR1 and FR2-1 band, otherwise it is absent.

NOTE: To determine whether the UE supports a specific SCS for a given band, the network validates the *supportedSubCarrierSpacingDL* and the *scs-60kHz*.  
To determine whether the UE supports a channel bandwidth of 90 MHz, the network may ignore this capability and validate instead the *[channelBW-90mhz](README.md#user-content-^5f5bf3)*, the *supportedBandwidthCombinationSet* and the *supportedBandwidthCombinationSetIntraENDC*. To determine whether the UE supports a channel bandwidth of 400 MHz, the network may ignore this capability and validate the *supportedBandwidthCombinationSet*, the *supportedBandwidthCombinationSetIntraENDC*, and the *[supportedBandwidthDL](README.md#user-content-^06439f)*. For serving cell(s) with other channel bandwidths the network validates the *channelBWs-DL*, the *supportedBandwidthCombinationSet*. the *supportedBandwidthCombinationSetIntraENDC*, the *asymmetricBandwidthCombinationSet* (for a band supporting asymmetric channel bandwidth as defined in clause 5.3.6 of TS 38.101-1), *[supporteBandwidthDL/supportedBandwidthDL-v1710](README.md#user-content-^06439f)* and *supportedMinBandwidthDL*.

#### 4.2.7.6 FeatureSetDownlinkPerCC parameters

***channelBW-90mhz*** <a id="^5f5bf3"></a>

- Per FSPC
- Mandatory: CY
- FDD-TDD DIFF: N/A
- FR1-FR2 DIFF: FR1 only

Indicates whether the UE supprots the channel bandwidth of 90 MHz. For FR1, the UE shall indicate support according to TS 38.101-1, Table 5.3.5-1.

***supportedBandwidthDL, supportedBandwidthDL-v1710*** <a id="^06439f"></a>

- Per FSPC
- Mandatory: CY
- FDD-TDD DIFF: N/A
- FR1-FR2 DIFF: N/A

Indicates maximum DL channel bandwidth supported for a given SCS that UE supports within a single CC (and in case of DAPS handover for the source or target cell), which is defined in Table 5.3.5-1 in TS 38.101-1 for FR1 and Table 5.3.5-1 in TS 38.101-2 for FR2.  
For FR1, all the bandwidths listed in TS38.101-1 Table 5.3.5-1 for each band shall be mandatory with a single CC unless indicated optional. For FR2, the set of mandatory CBW is 50, 100, 200 MHz. When this field is included in a band combination with a single band entry and a single CC entry (i.e. non-CA band combination), the UE shall indicate the maximum channel bandwdith for the band according to TS 38.101-1 and TS 38.101-2. For FR2, *supportedBandwidthDL-v1710* is included if the maximum DL channel bandwidth supported by the UE within a single CC is greater than 400MHz. When the *supportedBandwidthDL* and the *supportedBandwidthDL-v1710* are reported together for a CC, the network which is able to decode the *supportedBandwidthDL-v1710* ignores the *supportedBandwidthDL*.  
The UE may report a *supportedBandwidthDL* wider than the *channelBWs-DL*; this *supportedBandwidthDL* may not be included in the Table 5.3.5-1 of TS 38.101-1/TS 38.101-2 for the case that the UE is unable to report the actual supported bandwidth according to the Table 5.3.5-1 of TS 38.101-1/TS 38.101-2. For each band, RedCap UEs shall indicate its maximum channel bandwidth, which is the maximum of those channel bandwidths that are less than or equal to 20 MHz for FR1 and less than or equal to 100 Mhz for FR2, taking restrictions in TS 38.101-1 and TS 38.101-2 into consideration.

NOTE: To determine whether the UE supprots a channel bandwidth of 90 MHz, the network may ignore this capability and validate instead the *[channelBW-90mhz](README.md#user-content-^5f5bf3)*, the *supportedBandwidthCombinationSet* and the *supportedBandwidthCombinationSetIntraENDC*. To determine whether the UE supports a channel bandwidth of 400 MHz, the network validates this capability, the *supportedBandwidthCombinationSet*, and the *supportedBandwidthCombinationSetIntraENDC*. For serving cell(s) with other channel bandwidths the network validates the *[channelBWs-DL](README.md#user-content-^86013d)*, the *supportedBandwidthCombinationSet*, the *supportedBandwidthCombinationSetIntraENDC*, the *asymmetricBandwidthCombinationSet* (for a band supporting asymmetric channel bandwidth as defined in clause 5.3.6 of TS 38.101-1), *supportedBandwidthDL*/*supportedBandwidthDL-v1710* and *supportedMinBandwidthDL*.
