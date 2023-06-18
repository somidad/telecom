## 7.2 Measurements
	- (Omitted)
	- Both MN-configured and SN-configured RRM measurements are supported while the SCG is deactivated. The PSCell measurement cycle when in deactivated SCG state is configured by RRC.
	- When SRB3 is not configured or the SCG is deactivated, reports for measurements configured by the SN are sent on SRB1. When SRB3 is configured and SCG transmission of radio bearers is not suspended and the SCG is not deactivated, reports for measurements configured by the SN are sent on SRB3.
	- (Omitted)
## 7.7 SCG/MCG failure handling
	- (Omitted)
	- If radio link failure is detected for MCG, fast MCG link recovery is configured and the SCG is not deactivated, the UE triggers fast MCG link recovery. Otherwise, the UE initiates the RRC connection re-establishment procedure. During the execution of PSCell addition or PSCell change, if radio link failure is detected for MCG, the UE initiates the RRC connection re-establishment procedure.
	- (Omitted)
	- The following SCG failure cases are supported:
		- SCG RLF;
		- SCG beam failure while the SCG is deactivated;
		- SN addition/change failure;
		- For EN-DC, NGEN-DC and NR-DC, SCG configuration failure or CPC configuration failure (only for messages on SRB3);
		- For EN-DC, NGEN-DC and NR-DC, SCG RRC integrity check failure (on SRB3);
		- For EN-DC, NGEN-DC and NR-DC, consistent UL LBT failure on PSCell;
		- For IAB-MT, reception of a BH RLF indication from SCG;
		- CPA/CPC execution failure.
	- (Omitted)
## 7.10 UE assistance information
	- In MR-DC, the UE can be configured to report MCG specific UE assistance information if the MN is a gNB and/or SCG specific UE assistance information if the SN is a gNB, if it prefers an adjustment on the connected mode DRX parameters, the maximum aggregated bandwidth, the maximum number of secondary component carriers, the maximum number of MIMO layers, whether the UE prefers the SCG to be deactivated, the minimum scheduling offset for cross-slot scheduling cycle length, and/or whether the UE is applying RLM/BFD measurements relaxation for power saving. In these cases, it is up to the network whether to accommodate the preference or how to use the relaxation status indications. SCG specific UE assistance information for power saving can be configured by the network via SRB1 or SRB3. SCG specific UE assistance information for power saving is directly transmitted to the SN via SRB3, if SRB3 is configured and the SCG is activated, otherwise UE transmits SCG specific UE assistance information for power saving in a transparent container to the MN. When network simultaneously configures the UE to perform radio link monitoring on the SCG and beam failure detection on the SCG while the SCG is deactivated, UE assistance information for the relaxation state report of RLM/BFD measurements for SCG is reported over MCG. UE can implicitly indicate a preference for NR SCG release by indicating zero number of carriers and zero aggregated maximum bandwidth in both FR1 and FR2.
## 7.13 Activation and Deactivation of SCG
	- To enable reasonable UE battery consumption while having fast usage of SCG when (NG)EN-DC or NR-DC is configured, an activation/deactivation mechanism of SCG is supported. While the SCG is deactivated, there is no transmission via SCG RLC bearers. Only the NR SCG can be deactivated, and all SCG SCell(s) are in deactivated state while the SCG is deactivated.
	- Upon SCG deactivation and while the SCG is deactivated, the network ensures that there is no uplink control PDU transmission to the deactivated SCG (e.g. the network releases statusReportRequired from PDCP entities of SCG bearers if configured, the network does not perform QoS flow remapping from a DRB associated to the deactivated SCG to another DRB). The network ensures the SCG is activated while PDCP duplication is activated for SCG RLC entities associated with a PDCP entity.
		- NOTE:	Upon SCG (de)activation, it is up to the network to ensure there is no pending SDUs or PDUs in SCG RLC entity (e.g. instructs the UE to perform PDCP data recovery and RLC re-establishment/release, if needed).
	- While the SCG is deactivated, the UE will not transmit PUSCH, SRS and CSI report on SCG, and the UE is not required to monitor PDCCH or receive DL-SCH on SCG. If configured by the network, the UE performs radio link monitoring on the SCG and beam failure detection on the SCG while SCG is deactivated. In case of SCG activation without performing random access, the network can indicate TCI states to UE for PDCCH/PDSCH reception on PSCell, if not provided, the UE uses the previously activated TCI states.
	- The MN can configure the SCG as activated or deactivated upon e.g. PSCell addition, PSCell change, RRC Resume or handover. In case the SCG is configured as deactivated, the UE does not perform random access towards the PSCell. The network can trigger SCG RRC reconfiguration (e.g. PSCell change, configuration update) when deactivating the SCG and while the SCG is in deactivated state.
	- SCG activation can be requested by the MN, by the SN and by the UE. SCG deactivation can be requested by the MN and by the SN. For UL data arrival on SCG bearer(s) while the SCG is deactivated, the UE indicates to the MN that it has UL data to transmit over SCG bearer. During handover procedure, the target MN can indicate the SCG state in the RRC reconfiguration message sent to the UE by the source MN.
	- Network can configure whether the UE is allowed to indicate a preference for SCG deactivation to the MN.
## 7.14 RLM/BFD relaxation
	- (Omitted)
	- For RLM/BFD relaxation, network may simultaneously configure the UE to perform radio link monitoring on the SCG and beam failure detection on the SCG while SCG is deactivated. In such case, UE initiates UE assistance information for the relaxation state report of RLM/BFD measurements for SCG.
	- For RLM/BFD relaxation, network may simultaneously configure the UE not to perform radio link monitoring on the SCG and beam failure detection on the SCG while SCG is deactivated. In such case, UE assistance information for the relaxation state report of RLM/BFD measurements for SCG will not be initiated.