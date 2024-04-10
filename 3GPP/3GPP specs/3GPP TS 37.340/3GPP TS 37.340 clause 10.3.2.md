
### 10.3.2 MR-DC with 5GC

The SN Modification procedure may be initiated either by the MN or by the SN and be used to modify the current user plane resource configuration (e.g. related to PDU session, QoS flow or DRB) or to modify other properties of the UE context within the same SN. It may also be used to transfer an RRC message from the SN to the UE via the MN and the response from the UE via MN to the SN (e.g. when SRB3 is not used). In NGEN-DC and NR-DC, the RRC message is an NR message (i.e., _RRCReconfiguration_) whereas in NE-DC it is an E-UTRA message (i.e., _RRCConnectionReconfiguration_). In case of CPA, inter-SN CPC or inter-SN subsequent CPAC, this procedure is used to modify CPA, inter-SN CPC or inter-SN subsequent CPAC configuration within the same candidate SN. In case of CPA, inter-SN CPC or inter-SN subsequent CPAC, this procedure may also be triggered by the candidate SN to add some prepared PSCells from the suggested list or cancel part of the prepared PSCells. In case of intra-SN CPC or intra-SN subsequent CPAC, this procedure is used to configure, modify or release intra-SN CPC or intra-SN subsequent CPAC configuration. In case of intra-SN SCG LTM, this procedure is used to configure, modify or release intra-SN SCG LTM configuration. This procedure may be initiated by the MN or SN to request the SN or MN to [activate or deactivate the SCG](../../3GPP%20features/SCG%20deactivation.md). This procedure can also be used to support coordination between the MN and the SN for managing the configuration and reporting of QoE measurements and/or RAN visible QoE measurements in NR-DC.

The SN modification procedure does not necessarily need to involve signalling towards the UE.

#### **MN initiated SN Modification**

TBU

The MN uses the procedure to initiate configuration changes of the SCG within the same SN, including addition, modification or release of the user plane resource configuration. The MN uses this procedure to perform handover within the same MN while keeping the SN, when the SN needs to be involved (i.e. in NGEN-DC). The MN also uses the procedure to query the current SCG configuration, e.g. when delta configuration is applied in an MN initiated SN change. The MN also uses the procedure to provide the S-RLF related information to the SN or to provide additional available DRB IDs to be used for SN terminated bearers. The MN also uses this procedure to [activate or deactivate the SCG](../../3GPP%20features/SCG%20deactivation.md). The MN may not use the procedure to initiate the addition, modification or release of SCG SCells. The SN may reject the request, except if it concerns the release of the user plane resource configuration, or if it is used to perform handover within the same MN while keeping the SN. Figure 10.3.2-1 shows an example signalling flow for an MN initiated SN Modification procedure.

1. The MN sends the _SN Modification Request_ message, which may contain user plane resource configuration related or other UE context related information, PDU session level Network Slice info and the requested SCG configuration information, including the UE capabilities coordination result to be used as basis for the reconfiguration by the SN. In case a security key update in the SN is required, a new _SN Security Key_ is included. In case the PDCP data recovery in the SN is required, the _PDCP Change_ _Indication_ is included which indicates that PDCP data recovery is required in SN. In case of coordination between the MN and the SN on QoE and/or RAN visible QoE measurement configuration and reporting, the _SN Modification Request_ message may contain the _QMC Coordination Request_ IE.

2. The SN responds with the _SN Modification Request Acknowledge_ message, which may contain new SCG radio configuration information within an SN RRC reconfiguration message_,_ and data forwarding address information (if applicable). If the MN requested the [SCG to be activated or deactivated](../../3GPP%20features/SCG%20deactivation.md), the SN indicates whether the [SCG is activated or deactivated](../../3GPP%20features/SCG%20deactivation.md). In case of coordination between the MN and the SN on QoE and/or RAN visible QoE measurement configuration and reporting, the _SN Modification Request_ _Acknowledge_ message may contain the _QMC Coordination Response_ IE.

NOTE 1: For MN terminated bearers to be setup for which PDCP duplication with CA is configured in NR SCG side, the MN allocates up to 4 separate Xn-U bearers and the SN provides a logical channel ID for primary or split secondary path to the MN.

For SN terminated bearers to be setup for which PDCP duplication with CA is configured in NR MCG side, the SN allocates up to 4 separate Xn-U bearers and the MN provides a logical channel ID for primary or split secondary path to the SN via an additional MN-initiated SN modification procedure.

2a. When applicable, the MN provides data forwarding address information to the SN. For SN terminated bearers using MCG resources, the MN provides Xn-U DL TNL address information in the _Xn-U Address Indication_ message.

3/4. The MN initiates the RRC reconfiguration procedure, including an SN RRC reconfiguration message. The UE applies the new configuration, synchronizes to the MN (if instructed, in case of intra-MN handover) and replies with MN RRC reconfiguration complete message, including an SN RRC response message, if needed. In case the UE is unable to comply with (part of) the configuration included in the MN RRC reconfiguration message, it performs the reconfiguration failure procedure.

5. Upon successful completion of the reconfiguration, the success of the procedure is indicated in the _SN Reconfiguration Complete_ message.

6. If instructed, the UE performs synchronisation towards the PSCell of the SN as described in SN addition procedure. Otherwise, the UE may perform UL transmission after having applied the new configuration.

7. If PDCP termination point is changed for bearers using RLC AM, and when RRC full configuration is not used, the SN Status Transfer takes place between the MN and the SN (Figure 10.3.2-1 depicts the case where a bearer context is transferred from the MN to the SN).

8. If applicable, data forwarding between MN and the SN takes place (Figure 10.3.2-1 depicts the case where a user plane resource configuration related context is transferred from the MN to the SN).

9. The SN sends the _Secondary RAT Data Usage Report_ message to the MN and includes the data volumes delivered to and received from the UE as described in clause 10.11.2.

NOTE 2: The order the SN sends the _Secondary RAT Data Usage Report_ message and performs data forwarding with MN is not defined. The SN may send the report when the transmission of the related QoS flow is stopped.

10. If applicable, a PDU Session path update procedure is performed.

#### **SN initiated SN Modification with MN involvement**

TBU

The SN uses the procedure to perform configuration changes of the SCG within the same SN, e.g. to trigger the modification/release of the user plane resource configuration, to trigger the release of SCG resources (e.g., release SCG lower layer resources but keep SN), and to trigger PSCell changes (e.g. when a new security key is required or when the MN needs to perform PDCP data recovery). The MN cannot reject the release request of PDU session/QoS flows and the release request of SCG resources. The SN also uses the procedure to request the MN to provide more DRB IDs to be used for SN terminated bearers or to return DRB IDs used for SN terminated bearers that are not needed any longer. The SN also uses this procedure to [activate or deactivate the SCG](../../3GPP%20features/SCG%20deactivation.md). Figure 10.3.2-2 shows an example signalling flow for SN initiated SN Modification procedure.

1. The SN sends the _SN Modification Required_ message including an SN RRC reconfiguration message, which may contain user plane resource configuration related context, other UE context related information and the new radio resource configuration of SCG. The SN may request the [SCG to be activated or deactivated](../../3GPP%20features/SCG%20deactivation.md). In case of change of security key, the _PDCP Change_ _Indication_ indicates that an SN security key update is required. In case the MN needs to perform PDCP data recovery, the _PDCP Change_ _Indication_ indicates that PDCP data recovery is required. In case of coordination between the MN and the SN on QoE and/or RAN visible QoE measurement configuration and reporting, the _SN Modification Required_ message may contain the _QMC Coordination Request_ IE.

The SN can decide whether the change of security key is required.

NOTE 3a: In case that a MN initiated conditional reconfiguration (e.g. CHO, MN initiated inter-SN CPC or MN initiated inter-SN subsequent CPAC) is prepared, and if any execution of a prepared SN initiated intra-SN CPC or SN initiated intra-SN subsequent CPAC without MN involvement procedure or reconfiguration of the SCG, the SN notifies to the MN via the _SN Modification Required_ message. In this case, the steps 2 and 3 are skipped.

NOTE 3b: In case of SN initiated inter-SN CPC or SN initiated inter-SN subsequent CPAC and in case that a candidate SN triggered the SN Initiated SN Modification procedure to include some prepared PSCells (within the candidate cells suggested by the source SN in SN initiated inter-SN CPC or SN initiated inter-SN subsequent CPAC) or to remove some prepared PSCells, the MN may decide to trigger the step 2 towards the source SN.

2/3. The MN initiated SN Modification procedure may be triggered by _SN Modification Required_ message, e.g. when an SN security key change needs to be applied.

NOTE 3: For SN terminated bearers to be setup for which PDCP duplication with CA is configured in NR MCG side, the SN allocates up to 4 separate Xn-U bearers and the MN provides a logical channel ID for primary or split secondary path to the SN via the nested MN-initiated SN modification procedure.

4. The MN sends the MN RRC reconfiguration message to the UE including the SN RRC reconfiguration message with the new SCG radio resource configuration.

5. The UE applies the new configuration and sends the MN RRC reconfiguration complete message, including an SN RRC response message, if needed. In case the UE is unable to comply with (part of) the configuration included in the MN RRC reconfiguration message, it performs the reconfiguration failure procedure.

6. Upon successful completion of the reconfiguration, the success of the procedure is indicated in the _SN Modification Confirm_ message including the SN RRC response message, if received from the UE. In case of coordination between the MN and the SN on QoE and/or RAN visible QoE measurement configuration and reporting, the _SN Modification Confirm_ message may contain the _QMC Coordination Response_ IE.

7. If instructed, the UE performs synchronisation towards the PSCell configured by the SN as described in SN Addition procedure. Otherwise, the UE may perform UL transmission directly after having applied the new configuration.

8. If PDCP termination point is changed for bearers using RLC AM, and when RRC full configuration is not used, the SN Status Transfer takes place between the MN and the SN (Figure 10.3.2-2 depicts the case where a bearer context is transferred from the SN to the MN).

9. If applicable, data forwarding between MN and the SN takes place (Figure 10.3.2-2 depicts the case where a user plane resource configuration related context is transferred from the SN to the MN).

10. The SN sends the _Secondary RAT Data Usage Report_ message to the MN and includes the data volumes delivered to and received from the UE as described in clause 10.11.2.

NOTE 4: The order the SN sends the _Secondary RAT Data Usage Report_ message and performs data forwarding with MN is not defined. The SN may send the report when the transmission of the related QoS flow is stopped.

11. If applicable, a PDU Session path update procedure is performed.

#### **SN initiated SN Modification without MN involvement**

This procedure is not supported for NE-DC.

TBU

The SN initiated SN modification procedure without MN involvement is used to modify the configuration within SN in case no coordination with MN is required, including the addition/modification/release of SCG SCell and PSCell change (e.g. when the security key does not need to be changed and the MN does not need to be involved in PDCP recovery). The SN may initiate the procedure to configure, modify or release intra-SN CPC or intra-SN subsequent CPAC configuration within the same SN. The SN may initiate the procedure to configure, modify or release intra-SN SCG LTM configuration within the same SN. Figure 10.3.2-3 shows an example signalling flow for SN initiated SN modification procedure without MN involvement. The SN can decide whether the Random Access procedure is required.

1. The SN sends the SN RRC reconfiguration message to the UE through SRB3.

2. The UE applies the new configuration and replies with the SN RRC reconfiguration complete message. In case the UE is unable to comply with (part of) the configuration included in the SN RRC reconfiguration message, it performs the reconfiguration failure procedure.

3. If instructed, the UE performs synchronisation towards the PSCell of the SN as described in SN Addition procedure. Otherwise the UE may perform UL transmission after having applied the new configuration.

#### **SN initiated Conditional SN Modification without MN involvement (SRB3 is used)**

This procedure is not supported for NE-DC and NGEN-DC.

TBU

The SN initiates the procedure when it needs to transfer an NR RRC message to the UE and SRB3 is used to configure intra-SN CPC or intra-SN subsequent CPAC.

1. The SN sends the SN RRC reconfiguration including CPC configuration or subsequent CPAC configuration to the UE through SRB3.

2. The UE applies the new configuration. In case the UE is unable to comply with (part of) the configuration included in the SN RRC reconfiguration message, it performs the reconfiguration failure procedure. The UE starts evaluating the execution conditions for the candidate PSCell(s). The UE maintains connection with the source PSCell and replies with the _RRCReconfigurationComplete_ message to the SN via SRB3.

3. If at least one candidate PSCell satisfies the corresponding execution condition, the UE detaches from the source PSCell, applies the stored configuration corresponding to the selected candidate PSCell and synchronises to the candidate PSCell. In subsequent CPAC, the UE keeps the configured subsequent CPAC configuration and evaluates the execution conditions of other candidate PSCells after completion of the subsequent CPAC execution.

4. The UE completes the CPC execution procedure by sending an _RRCReconfigurationComplete_ message to the new PSCell.

NOTE 5: For a subsequent CPAC configuration, after a PSCell change, if the execution condition of one candidate PSCell is satisfied, the UE executes steps 3-4, e.g. based on the configuration provided in step 1.

#### **SN initiated SCG LTM without MN involvement (SRB3 is used)**

This procedure is not supported for NE-DC and NGEN-DC.

TBU

The SN initiates the procedure when it needs to transfer an NR RRC message to the UE and SRB3 is used to configure intra-SN SCG LTM.

1. The SN sends the SN _RRCReconfiguration_ including SCG LTM configuration to the UE through SRB3.

2. The UE stores the SCG LTM candidate cell configurations and transmits an _RRCReconfigurationComplete_ message to the SN.

3a. If indicated by the SN, the UE performs DL synchronization with candidate cell(s) before receiving the cell switch command.

3b. If indicated by the SN, the UE performs early TA acquisition with candidate cell(s) before receiving the cell switch command as specified in clause in 9.2.3.5.2 in TS 38.300 [3].

4. The UE performs L1 measurements on the configured candidate cell(s) and transmits L1 measurement reports to the SN, according to the L1 measurement configuration in _RRCReconfiguration_ received in step 1. The UE starts to perform L1 measurements once the L1 measurement configuration is applicable.

5. The SN decides to execute cell switch to a target cell and transmits a MAC CE triggering cell switch by including the candidate configuration index of the target cell. The UE switches to the target cell and applies the configuration indicated by candidate configuration index.

6. The UE performs the random access procedure towards the target cell, if the UE does not have valid TA of the target cell.

7. The UE completes the SCG LTM cell switch procedure by sending _RRCReconfigurationComplete_ message to target cell. If the UE has performed a RA procedure in step 6 the UE considers that LTM execution is successfully completed when the random access procedure is successfully completed. For RACH-less LTM, the UE considers that LTM execution is successfully completed when the UE determines that the target cell has successfully received its first UL data, as specified in clause in 9.2.3.5.2 in TS 38.300 [3].

NOTE 6: The steps 3-7 can be performed multiple times for subsequent SCG LTM using the SCG LTM candidate configuration(s) provided in step 1.

#### **Transfer of an NR RRC message to/from the UE (when SRB3 is not used)**

This procedure is supported for all the MR-DC options.

TBU

The SN initiates the procedure when it needs to transfer an NR RRC message to the UE and SRB3 is not used.

1. The SN initiates the procedure by sending the _SN Modification Required_ to the MN including the SN RRC reconfiguration message.

2. The MN forwards the SN RRC reconfiguration message to the UE including it in the RRC reconfiguration message.

3. The UE applies the new configuration and replies with the RRC reconfiguration complete message by including the SN RRC reconfiguration complete message. In case the UE is unable to comply with (part of) the configuration included in the SN RRC reconfiguration message, it performs the reconfiguration failure procedure.

4. The MN forwards the SN RRC response message, if received from the UE, to the SN by including it in the _SN Modification Confirm_ message.

5. If instructed, the UE performs synchronisation towards the PSCell of the SN as described in SN Addition procedure. Otherwise the UE may perform UL transmission after having applied the new configuration.

#### **SN initiated Conditional SN Modification without MN involvement (SRB3 is not used)**

This procedure is not supported for NE-DC and NGEN-DC.

TBU

The SN initiates the procedure when it needs to transfer an NR RRC message to the UE and SRB3 is not used to configure intra-SN CPC or intra-SN subsequent CPAC.

1. The SN initiates the procedure by sending the _SN Modification Required_ to the MN including the SN RRC reconfiguration message with CPC configuration or subsequent CPAC configuration.

2. The MN forwards the SN RRC reconfiguration message to the UE including it in the _RRCReconfiguration_ message.

3. The UE replies with the _RRCReconfigurationComplete_ message by including the SN RRC reconfiguration complete message. In case the UE is unable to comply with (part of) the configuration included in the SN RRC reconfiguration message, it performs the reconfiguration failure procedure. The UE maintains connection with source PSCell after receiving CPC configuration or subsequent CPAC configuration, and starts evaluating the execution conditions for the candidate PSCell(s).

4. The MN forwards the SN RRC response message, if received from the UE, to the SN by including it in the _SN Modification Confirm_ message.

5. If at least one candidate PSCell satisfies the corresponding execution condition, the UE completes the CPC execution procedure by an _ULInformationTransferMRDC_ message to the MN which includes an embedded _RRCReconfigurationComplete_ message to the selected target PSCell. In subsequent CPAC, the UE keeps the configured subsequent CPAC configuration and evaluates the execution conditions of other candidate PSCells after completion of the subsequent CPAC execution.

6. The _RRCReconfigurationComplete_ message is forwarded to the SN embedded in _RRC Transfer_ message.

7. The UE detaches from the source PSCell, applies the stored corresponding configuration and synchronises to the selected candidate PSCell.

NOTE 7: For a subsequent CPAC configuration, after a PSCell change, if the execution condition of one candidate PSCell is satisfied, the UE executes steps 5-7, e.g. based on the configuration provided in step 2.

#### **SN initiated SCG LTM without MN involvement (SRB3 is not used)**

This procedure is not supported for NE-DC and NGEN-DC.

TBU

The SN initiates the procedure when it needs to transfer an NR RRC message to the UE and SRB3 is not used to configure intra-SN SCG LTM.

1. The SN initiates the procedure by sending the _SN Modification Required_ to the MN including the SN _RRCReconfiguration_ message with SCG LTM configuration.

2. The MN forwards the SN _RRCReconfiguration_ message to the UE including it in the _RRCReconfiguration_ message.

3. The UE replies with the _RRCReconfigurationComplete_ message by including the SN _RRCReconfigurationComplete_ message.

4. The MN forwards the SN RRC response message, if received from the UE, to the SN by including it in the _SN Modification Confirm_ message.

5a. If indicated by the SN, the UE performs DL synchronization with candidate cell(s) before receiving the cell switch command.

5b. If indicated by the SN, the UE performs early TA acquisition with candidate cell(s) before receiving the cell switch command as specified in clause in 9.2.3.5.2 in TS 38.300 [3].

6. The UE performs L1 measurements on the configured candidate cell(s) and transmits L1 measurement reports to the SN, according to the L1 measurement configuration in _RRCReconfiguration_ received in step 2. The UE starts to perform L1 measurements once the L1 measurement configuration is applicable.

7. The SN decides to execute cell switch to a target cell and transmits a MAC CE triggering cell switch by including the candidate configuration index of the target cell. The UE switches to the target cell and applies the configuration indicated by candidate configuration index.

8. The UE sends an _ULInformationTransferMRDC_ message to the MN which includes an embedded _RRCReconfigurationComplete_ message to the target cell.

9. The _RRCReconfigurationComplete_ message is forwarded to the SN embedded in _RRC Transfer_ message.

10. The UE performs the random access procedure towards the target cell, if the UE does not have valid TA of the target cell.

11. The UE completes the SCG LTM cell switch procedure by sending an UL transmission to target cell. If the UE has performed a RA procedure in step 10 the UE considers that LTM execution is successfully completed when the random access procedure is successfully completed. For RACH-less LTM, the UE considers that LTM execution is successfully completed when the UE determines that the SN has successfully received its first UL transmission, as specified in clause in 9.2.3.5.2 in TS 38.300 [3].

NOTE 8: The steps 5-11 can be performed multiple times for subsequent SCG LTM using the SCG LTM candidate configuration(s) provided in step 2.
