
## 7.13 Activation and Deactivation of SCG

To enable reasonable UE battery consumption while having fast usage of SCG when (NG)EN-DC or NR-DC is configured, an activation/deactivation mechanism of SCG is supported. While the SCG is deactivated, there is no transmission via SCG RLC bearers. Only the NR SCG can be deactivated, and all SCG SCell(s) are in deactivated state while the SCG is deactivated.

Upon SCG deactivation and while the SCG is deactivated, the network ensures that there is no uplink control PDU transmission to the deactivated SCG (e.g. the network releases statusReportRequired from PDCP entities of SCG bearers if configured, the network does not perform QoS flow remapping from a DRB associated to the deactivated SCG to another DRB). The network ensures the SCG is activated while PDCP duplication is activated for SCG RLC entities associated with a PDCP entity.

NOTE: Upon SCG (de)activation, it is up to the network to ensure there is no pending SDUs or PDUs in SCG RLC entity (e.g. instructs the UE to perform PDCP data recovery and RLC re-establishment/release, if needed).

While the SCG is deactivated, the UE will not transmit PUSCH, SRS and CSI report on SCG, and the UE is not required to monitor PDCCH or receive DL-SCH on SCG. If configured by the network, the UE performs radio link monitoring on the SCG and beam failure detection on the SCG while SCG is deactivated. In case of SCG activation without performing random access, the network can indicate TCI states to UE for PDCCH/PDSCH reception on PSCell, if not provided, the UE uses the previously activated TCI states.

The MN can configure the SCG as activated or deactivated upon e.g. PSCell addition, PSCell change, RRC Resume or handover. In case the SCG is configured as deactivated, the UE does not perform random access towards the PSCell. The network can trigger SCG RRC reconfiguration (e.g. PSCell change, configuration update) when deactivating the SCG and while the SCG is in deactivated state.

SCG activation can be requested by the MN, by the SN and by the UE. SCG deactivation can be requested by the MN and by the SN. For UL data arrival on SCG bearer(s) while the SCG is deactivated, the UE indicates to the MN that it has UL data to transmit over SCG bearer. During handover procedure, the target MN can indicate the SCG state in the RRC reconfiguration message sent to the UE by the source MN.

Network can configure whether the UE is allowed to indicate a preference for SCG deactivation to the MN.