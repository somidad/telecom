
# SCG deactivation

## Overview

Proposed in Rel-17 Work Item [Further Multi-RAT Dual-Connectivity enhancements](../3GPP%20Work%20Items/Release%2017/Further%20Multi-RAT%20Dual-Connectivity%20enhancements.md) (WID RP-201040)

### Motivation

- High NR UE power consumption
- Consume power for NR only high data rate is required

**SN release and add**

- PDCP/SDAP termination point change -> data forwarding -> interruption

**Bearer type change between MCG bearer <-> SCG/split bearer**

- Requires RRC signaling for new cell group config

**SCG deactivation and activation**

- No PDCP/SDAP termination point change
- No RRC signaling for cell group config update
- Just toggles activation state of SCG

## Scopes

- NR SCG only (EN-DC, NR-DC and NGEN-DC)
- No deactivated SCG in conditional configuration
- No CPC (or subsequenct CPAC) while SCG is deactivated
- No SCG deactivation while CPC (or subsequent CPAC) is configured

## Stage-2

### Control plane

#### Security

- Security key update is up to NW implementation upon SCG activation

#### SCG/MCG failure handling

- SCG failure can happen due to BFD on deactivated SCG
- RRE instead of fast MCG link recovery if SCG is deactivated

#### Measurements

- MN-/SN-configured RRM measurements are still supported

#### SRB3

- All SN RRC signaling is transferred via MN (SRB1)

#### UE assistance information

- If MN allows, UE can indicate it prefers SCG to be deactivated
- SCG UAI is transferred via MN (SRB1)

### User plane

#### SDAP/PDCP

- NW ensures no uplink control PDU transmission, e.g.
	- NW releases statusReportRequired
	- No QoS flow remapping
- Not interoperable with PDCP duplication

#### RLC

- NW ensures no pending RLC SDU/PDU, e.g.
	- NW instructs PDCP data recovery and RLC reestablish/release upon SCG (de)activation, if needed

### L1/L2

- SCG TA timer continues running
- No PUSCH, SRS and CSI
- No PDCCH monitoring
- No DL-SCH receive
- No PHR
- Perform RLM/BFD (with/without relaxation), if configured by NW

### Operation

#### SCG deactivation

- MN can request SCG deactivation upon PSCell addition, change, RRC Resume or handover
- MN and SN can request SCG deactivation
- No random access
- SCG RRC reconfiguration is still possible as well as PSCell change

#### SCG activation

- MN, SN and UE can request SCG activation
- UE can indicate UL data arrival on SCG
- NW can indicate TCI states for PDCCH/PDSCH reception
- Otherwise, previously activated TCI states are used
- NW can instruct CBRA/CFRA regardless of TA timer, RLF and BFD


## Stage-3

### UE capabilities

- scg-ActivationDeactivationENDC-r17, scg-ActivationDeactivationResumeENDC-r17
- scg-ActivationDeactivationNRDC-r17, scg-ActivationDeactivationResumeNRDC-r17

### NR RRC

- scg-DeactivationPreferenceConfig-r17 in OtherConfig
- scg-DeactivationPreference-r17, uplinkData in UEAssistanceInformation
- scg-State in RRCReconfiguration, RRCResune

### XnAP

- SCG Activation Request, SCG Activation Status in S-NODE ADDITION REQUEST, REQUEST ACKNOWLEDGE
- SCG Activation Request, SCG Activation Status in S-NODE MODIFICATION REQUEST, REQUEST ACKNOWLEDGE
- SCG Activation Request in S-NODE MODIFICATION REQUIRED

### E1AP

- SCG Activation Status in BEARER CONTEXT SETUP REQUEST, BEARER CONTEXT MODIFICATION REQUEST

### F1AP

- SCG Activation Request, SCG Activation Status in UE CONTEXT SETUP REQUEST, UE CONTEXT MODIFICATION REQUEST
- SCG Activation Request, SCG Activation Status in UE CONTEXT MODIFICATION REQUEST, UE CONTEXT MODIFICATION RESPONSE
