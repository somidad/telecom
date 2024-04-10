
# 6 Layer 2 related aspects

## 6.1 MAC Sublayer

In MR-DC, the UE is configured with two MAC entities: one MAC entity for the MCG and one MAC entity for the SCG. The serving cells other than the PCell can be activated/deactivated by [RRC](../../3GPP%20features/SCG%20deactivation.md) or MAC Control Element. For activation/deactivation by MAC Control Element, the serving cells of the MCG other than the PCell can only be activated/deactivated by the MAC Control Element received on MCG, and the serving cells of the SCG other than PSCell can only be activated/ deactivated by the MAC Control Element received on SCG. The MAC entity applies the bitmap for the associated cells of either MCG or SCG. When the [SCG is not deactivated](../../3GPP%20features/SCG%20deactivation.md), the PSCell is always activated like the PCell (i.e. deactivation timer is not applied to PSCell). With the exception of PUCCH SCell, one deactivation timer is configured per SCell by RRC.

TBU

In (NG)EN-DC and NR-DC, when [SCG is deactivated](../../3GPP%20features/SCG%20deactivation.md) as described in clause 7.13, the TA timer associated with SCG continues running, the UE considers the TA is valid as long as TA timer is running. In case of [SCG activation](../../3GPP%20features/SCG%20deactivation.md), the UE can be instructed by the network to perform random access towards PSCell even if the TA timer associated with PSCell is running and RLF and beam failure are not declared. Besides, the UE can be instructed by the network to perform [SCG activation](../../3GPP%20features/SCG%20deactivation.md) without performing random access, if the TA timer associated with PSCell is running and RLM and beam failure detection are configured but RLF or beam failure is not declared. In case of network-initiated [SCG activation](../../3GPP%20features/SCG%20deactivation.md), both CBRA and CFRA on PSCell are supported. For CFRA, the dedicated RACH resources can be provided in the RRC message used to [activate SCG](../../3GPP%20features/SCG%20deactivation.md).

TBU

In MR-DC, PHR is independently configured per cell group. Events in one cell group can trigger power headroom reporting in both MCG and SCG. Power headroom information for one cell group is also included in a PHR transmitted in the other cell group. While the [SCG is deactivated](../../3GPP%20features/SCG%20deactivation.md), PHR for SCG is not reported.

TBU
