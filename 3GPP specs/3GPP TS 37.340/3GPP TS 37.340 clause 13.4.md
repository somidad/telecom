
## 13.4 Application Layer Measurement Collection

TBU

### 13.4.2 SRB5

SRB5 is supported in NR-DC, but not in EN-DC, NGEN-DC and NE-DC.

The decision to establish SRB5 is taken by the SN, which provides the SRB5 configuration using an SN RRC message. SRB5 establishment and release can be done at Secondary Node Addition and Secondary Node Change. SRB5 reconfiguration can be done at Secondary Node Modification procedure.

SRB5 is used to send RRC messages (i.e., _MeasurementReportAppLayer_ message) including application layer measurement report information directly to the SN.

SRB5 is modelled as one of the SRBs defined in TS 38.331 [4] and uses the NR-DCCH logical channel type.

When the SCG is released, SRB5 is released.

### 14.3.3 QoE Measurement Configuration

#### 13.4.3.1 QoE Measurement Collection Activation and Reporting in NR-DC

TBU

When [SCG is deactivated](../../3GPP%20features/SCG%20deactivation.md), for QoE configurations configured to use [SRB5](3GPP%20TS%2037.340%20clause%2013.4.md#13.4.2%20SRB5) for QoE reporting, it is up to network implementation whether to reconfigure the reporting leg to SRB4, release the QoE configuration or pause the QoE reporting. For UL data arrival on [SRB5](3GPP%20TS%2037.340%20clause%2013.4.md#13.4.2%20SRB5) while the [SCG is deactivated](../../3GPP%20features/SCG%20deactivation.md), the UE does not indicate to the MN that it has QoE report to transmit over SRB5 for the purpose of [SCG activation](../../3GPP%20features/SCG%20deactivation.md).

TBU
