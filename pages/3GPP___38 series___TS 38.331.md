alias:: 🏷 NR RRC protocol specification
repository:: https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3197

- #### 5.3.5.3 Reception of an RRCReconfiguration by the UE
	- (Omitted)
	- 1>	if the UE is configured with E-UTRA nr-SecondaryCellGroupConfig (UE in (NG)EN-DC):
		- 2>	if the RRCReconfiguration message was received via E-UTRA SRB1 as specified in TS 36.331 [10]; or
		- 2>	if the RRCReconfiguration message was received via E-UTRA RRC message RRCConnectionReconfiguration within MobilityFromNRCommand (handover from NR standalone to (NG)EN-DC);
			- (Omitted)
			- 3>	if the [scg-State](((648eff70-610a-4b5c-a08f-31c0be7672b9))) is not included in the E-UTRA message (RRCConnectionReconfiguration or RRCConnectionResume) containing the RRCReconfiguration message:
				- 4>	perform [SCG activation]([[3GPP/SCG (de)activation]]) as specified in [5.3.5.13a](((648ef4c8-12ce-4d8f-9022-c0097c73c912)));
				- 4>	if reconfigurationWithSync was included in spCellConfig of an SCG:
					- 5>	initiate the Random Access procedure on the PSCell, as specified in TS 38.321 [3];
				- 4>	else if the [SCG was deactivated]([[3GPP/SCG (de)activation]]) before the reception of the E-UTRA RRC message containing the RRCReconfiguration message:
					- 5>	if bfd-and-RLM was not configured to true before the reception of the E-UTRA RRCConnectionReconfiguration or RRCConnectionResume message containing the RRCReconfiguration message or if lower layers indicate that a Random Access procedure is needed for [SCG activation]([[3GPP/SCG (de)activation]]):
						- 6>	initiate the Random Access procedure on the SpCell, as specified in TS 38.321 [3];
					- 5>	else the procedure ends;
				- 4>	else the procedure ends;
			- 3>	else:
				- 4>	perform [SCG deactivation]([[3GPP/SCG (de)activation]]) as specified in [5.3.5.13b](((648ef58e-93b8-44a2-a32c-2acf2e1a83d4)));
				- 4>	the procedure ends;
		- 2>	if the RRCReconfiguration message was received within nr-SecondaryCellGroupConfig in RRCConnectionReconfiguration message received via SRB3 within DLInformationTransferMRDC:
			- 3>	submit the RRCReconfigurationComplete via E-UTRA embedded in E-UTRA RRC message RRCConnectionReconfigurationComplete as specified in TS 36.331 [10], clause 5.3.5.3/5.3.5.4;
			- 3>	if the [scg-State](((648eff70-610a-4b5c-a08f-31c0be7672b9))) is not included in the RRCConnectionReconfiguration:
				- 4>	if reconfigurationWithSync was included in spCellConfig of an SCG:
					- 5>	initiate the Random Access procedure on the SpCell, as specified in TS 38.321 [3];
				- 4>	else the procedure ends;
			- 3>	else:
				- 4>	perform [SCG deactivation]([[3GPP/SCG (de)activation]]) as specified in [5.3.5.13b](((648ef58e-93b8-44a2-a32c-2acf2e1a83d4)));
				- 4>	the procedure ends;
		- NOTE 1:	The order the UE sends the RRCConnectionReconfigurationComplete message and performs the Random Access procedure towards the SCG is left to UE implementation.
		- (Omitted)
	- 1>	else if the RRCReconfiguration message was received via SRB1 within the nr-SCG within mrdc-SecondaryCellGroup (UE in NR-DC, mrdc-SecondaryCellGroup was received in RRCReconfiguration or RRCResume via SRB1):
		- 2>	if the RRCReconfiguration is applied due to a conditional reconfiguration execution for CPC which is configured via conditionalReconfiguration contained in nr-SCG within mrdc-SecondaryCellGroup:
			- 3>	submit the RRCReconfigurationComplete message via the NR MCG embedded in NR RRC message ULInformationTransferMRDC as specified in clause 5.7.2a.3.
		- 2>	if the [scg-State](((648efffd-2d95-45be-a424-19d273bc88be))) is not included in the RRCReconfiguration or RRCResume message containing the RRCReconfiguration message:
			- 3>	perform [SCG activation]([[3GPP/SCG (de)activation]]) as specified in [5.3.5.13a](((648ef4c8-12ce-4d8f-9022-c0097c73c912)));
			- 3>	if reconfigurationWithSync was included in spCellConfig in nr-SCG:
				- 4>	initiate the Random Access procedure on the PSCell, as specified in TS 38.321 [3];
			- 3>	else if the [SCG was deactivated]([[3GPP/SCG (de)activation]]) before the reception of the NR RRC message containing the RRCReconfiguration message:
				- 4>	if bfd-and-RLM was not configured to true before the reception of the RRCReconfiguration or RRCResume message containing the RRCReconfiguration message; or
				- 4>	if lower layers indicate that a Random Access procedure is needed for [SCG activation]([[3GPP/SCG (de)activation]]):
					- 5>	initiate the Random Access procedure on the PSCell, as specified in TS 38.321 [3];
				- 4>	else the procedure ends;
			- 3>	else the procedure ends;
		- 2>	else
			- 3>	perform [SCG deactivation]([[3GPP/SCG (de)activation]]) as specified in [5.3.5.13b](((648ef58e-93b8-44a2-a32c-2acf2e1a83d4)));
			- 3>	the procedure ends;
		- NOTE 2a:	The order in which the UE sends the RRCReconfigurationComplete message and performs the Random Access procedure towards the SCG is left to UE implementation.
	- 1>	else if the RRCReconfiguration message was received via SRB3 (UE in NR-DC):
		- 2>	if the RRCReconfiguration message was received within DLInformationTransferMRDC:
			- 3>	if the RRCReconfiguration message was received within the nr-SCG within mrdc-SecondaryCellGroup (NR SCG RRC Reconfiguration):
				- 4>	if the [scg-State](((648eff70-610a-4b5c-a08f-31c0be7672b9))) is not included in the RRCReconfiguration message containing the RRCReconfiguration message:
					- 5>	if reconfigurationWithSync was included in spCellConfig in nr-SCG:
						- 6>	initiate the Random Access procedure on the PSCell, as specified in TS 38.321 [3];
					- 5>	else:
						- 6>	the procedure ends;
				- 4>	else:
					- 5>	perform [SCG deactivation]([[3GPP/SCG (de)activation]]) as specified in [5.3.5.13b](((648ef58e-93b8-44a2-a32c-2acf2e1a83d4)));
					- 5>	the procedure ends;
			- 3>	else:
				- 4>	if the RRCReconfiguration does not include the mrdc-SecondaryCellGroupConfig:
					- 5>	if the RRCReconfiguration includes the [scg-State](((648eff70-610a-4b5c-a08f-31c0be7672b9))):
						- 6>	perform [SCG deactivation]([[3GPP/SCG (de)activation]]) as specified in [5.3.5.13b](((648ef58e-93b8-44a2-a32c-2acf2e1a83d4)));
				- 4>	submit the RRCReconfigurationComplete message via SRB1 to lower layers for transmission using the new configuration;
		- 2>	else:
			- 3>	submit the RRCReconfigurationComplete message via SRB3 to lower layers for transmission using the new configuration;
	- 1>	else (RRCReconfiguration was received via SRB1):
		- 2>	if the UE is in NR-DC and;
		- 2>	if the RRCReconfiguration does not include the mrdc-SecondaryCellGroupConfig:
			- 3>	if the RRCReconfiguration includes the [scg-State](((648eff70-610a-4b5c-a08f-31c0be7672b9))):
				- 4>	perform [SCG deactivation]([[3GPP/SCG (de)activation]]) as specified in [5.3.5.13b](((648ef58e-93b8-44a2-a32c-2acf2e1a83d4)));
			- 3>	else:
				- 4>	perform [SCG activation]([[3GPP/SCG (de)activation]]) without SN message as specified in [5.3.5.13b1](((648ef610-dc49-448f-aaf2-bad36a382691)));
		- (Omitted)
	- (Omitted)
- #### 5.3.5.13a [SCG activation]([[3GPP/SCG (de)activation]])
  id:: 648ef4c8-12ce-4d8f-9022-c0097c73c912
	- Upon initiating the procedure, the UE shall:
		- 1>	if the UE is configured with an SCG after receiving the message for which this procedure is initiated:
			- 2>	if the UE was configured with a deactivated SCG before receiving the message for which this procedure is initiated:
				- 3>	consider the SCG to be activated;
				- 3>	resume performing radio link monitoring on the SCG, if previously stopped;
				- 3>	indicate to lower layers to resume beam failure detection on the PSCell, if previously stopped;
				- 3>	indicate to lower layers that the SCG is activated.
- #### 5.3.5.13b [SCG deactivation]([[3GPP/SCG (de)activation]])
  id:: 648ef58e-93b8-44a2-a32c-2acf2e1a83d4
	- Upon initiating the procedure, the UE shall:
		- 1>	consider the SCG to be deactivated;
		- 1>	indicate to lower layers that the SCG is deactivated;
		- 1>	if bfd-and-RLM is configured to true:
			- 2>	perform radio link monitoring on the SCG;
			- 2>	indicate to lower layers to perform beam failure detection on the PSCell;
		- 1>	else:
			- 2>	stop radio link monitoring on the SCG;
			- 2>	indicate to lower layers to stop beam failure detection on the PSCell;
			- 2>	stop timer T310 for this cell group, if running;
			- 2>	stop timer T312 for this cell group, if running;
			- 2>	reset the counters N310 and N311;
		- 1>	if the UE was in RRC_CONNECTED and the SCG was activated before receiving the message for which this procedure is initiated:
			- 2>	if SRB3 was configured before the reception of the RRCReconfiguration or of the RRCConnectionReconfiguration and SRB3 is not to be released according to any RadioBearerConfig included in the RRCReconfiguration or in the RRCConnectionReconfiguration as specified in TS 36.331[10]:
				- 3>	trigger the PDCP entity of SRB3 to perform SDU discard as specified in TS 38.323 [5];
				- 3>	re-establish the RLC entity of SRB3 as specified in TS 38.322 [4].
- #### 5.3.5.13b1 [SCG activation]([[3GPP/SCG (de)activation]]) without SN message
  id:: 648ef610-dc49-448f-aaf2-bad36a382691
	- Upon initiating the procedure, the UE shall:
		- 1>	if the SCG was deactivated before the reception of the RRCReconfiguration message or the E-UTRA RRCConnectionReconfiguration message for which the procedure invoking this clause is executed:
			- 2>	consider the SCG to be activated;
			- 2>	indicate to lower layers that the SCG is activated;
			- 2>	resume performing radio link monitoring on the SCG, if previously stopped;
			- 2>	indicate to lower layers to resume beam failure detection on the PSCell, if previously stopped;
			- 2>	if bfd-and-RLM was not configured to true before the reception of the RRCReconfiguration message or the E-UTRA RRCConnectionReconfiguration message for which the procedure invoking this clause is executed; or
			- 2>	if lower layers indicate that a Random Access procedure is needed for SCG activation:
				- 3>	initiate the Random Access procedure on the PSCell, as specified in TS 38.321 [3].
- ### 6.2.2 Message definitions
	- #### RRCReconfiguration
		- ```
		  RRCReconfiguration-v1700-IEs ::=        SEQUENCE {
		      otherConfig-v1700                       OtherConfig-v1700                                              OPTIONAL, -- Need M
		      sl-L2RelayUE-Config-r17                 SetupRelease { SL-L2RelayUE-Config-r17 }                       OPTIONAL, -- Need M
		      sl-L2RemoteUE-Config-r17                SetupRelease { SL-L2RemoteUE-Config-r17 }                      OPTIONAL, -- Need M
		      dedicatedPagingDelivery-r17             OCTET STRING (CONTAINING Paging)                               OPTIONAL, -- Cond PagingRelay
		      needForGapNCSG-ConfigNR-r17             SetupRelease {NeedForGapNCSG-ConfigNR-r17}                     OPTIONAL, -- Need M
		      needForGapNCSG-ConfigEUTRA-r17          SetupRelease {NeedForGapNCSG-ConfigEUTRA-r17}                  OPTIONAL, -- Need M
		      musim-GapConfig-r17                     SetupRelease {MUSIM-GapConfig-r17}                             OPTIONAL, -- Need M
		      ul-GapFR2-Config-r17                    SetupRelease { UL-GapFR2-Config-r17 }                          OPTIONAL, -- Need M
		      scg-State-r17                           ENUMERATED { deactivated }                                     OPTIONAL, -- Need N
		      appLayerMeasConfig-r17                  AppLayerMeasConfig-r17                                         OPTIONAL, -- Need M
		      ue-TxTEG-RequestUL-TDOA-Config-r17      SetupRelease {UE-TxTEG-RequestUL-TDOA-Config-r17}              OPTIONAL,  -- Need M
		      nonCriticalExtension                    SEQUENCE {}                                                    OPTIONAL
		  }
		  ```
		- **scg-State**
		  id:: 648eff70-610a-4b5c-a08f-31c0be7672b9
			- Indicates that the [SCG is in deactivated state]([[3GPP/SCG (de)activation]]).
			- This field is not used
				- in an RRCReconfiguration message received:
					- within mrdc-SecondaryCellGroup, or
					- in an E-UTRA RRCConnectionReconfiguration message, or
					- in an E-UTRA RRCConnectionResume message or
				- in an RRCReconfiguration message received via SRB3, except if the RRCReconfiguration message is included in DLInformationTransferMRDC.
			- The field is absent if CPA or CPC is configured for the UE, or if the RRCReconfiguration message is contained in CondRRCReconfig.
	- #### RRCResume
	  id:: 648eff66-a169-42f9-8615-a6fc3233ed81
		- ```
		  RRCResume-v1700-IEs ::=             SEQUENCE {
		      sl-ConfigDedicatedNR-r17            SetupRelease {SL-ConfigDedicatedNR-r16}                         OPTIONAL, -- Cond L2RemoteUE
		      sl-L2RemoteUE-Config-r17            SetupRelease {SL-L2RemoteUE-Config-r17}                         OPTIONAL, -- Cond L2RemoteUE
		      needForGapNCSG-ConfigNR-r17         SetupRelease {NeedForGapNCSG-ConfigNR-r17}                      OPTIONAL, -- Need M
		      needForGapNCSG-ConfigEUTRA-r17      SetupRelease {NeedForGapNCSG-ConfigEUTRA-r17}                   OPTIONAL, -- Need M
		      scg-State-r17                       ENUMERATED {deactivated}                                        OPTIONAL, -- Need N
		      appLayerMeasConfig-r17              AppLayerMeasConfig-r17                                          OPTIONAL, -- Need M
		      nonCriticalExtension                SEQUENCE {}                                                     OPTIONAL
		  }
		  ```
		- **scg-State**
		  id:: 648efffd-2d95-45be-a424-19d273bc88be
			- Indicates that the [SCG is in deactivated state]([[3GPP/SCG (de)activation]]).