alias:: 🏷 UE radio access capabilities
repository:: https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3193

- #### 4.2.7.9 MRDC-Parameters
	- per:: BC
	  mandatory:: No
	  fdd-tdd-diff:: N/A
	  fr1-fr2-diff:: N/A
	  **scg-ActivationDeactivationENDC-r17**
		- Indicates whether the UE supports [activation (with or without RACH) and deactivation on SCG]([[3GPP/SCG (de)activation]]) in EN-DC, upon SCG addition and upon reconfiguration of the SCG, as specified in TS 38.331 [9]. A UE supporting this feature shall indicate support of EN-DC as specified in TS 36.331 [17]. For the UE supporting this feature, it is mandatory to report maxNumberCSI-RS-BFD and maxNumberSSB-BFD for all NR bands of this band combination where the UE supports SpCell.
	- per:: BC
	  mandatory:: No
	  fdd-tdd-diff:: N/A
	  fr1-fr2-diff:: N/A
	  scg-ActivationDeactivationResumeENDC-r17
		- Indicates whether the UE supports [activation (with or without RACH) and deactivation on SCG]([[3GPP/SCG (de)activation]]) in EN-DC, upon reception of an RRCReconfiguration included in an RRCConnectionResume message, as specified in TS 38.331 [9] and TS 36.331 [17], A UE supporting this feature shall indicate support of EN-DC and support of resumeWithSCG-Config-r16 as specified in TS 36.331 [17]. For the UE supporting this feature, it is mandatory to report maxNumberCSI-RS-BFD and maxNumberSSB-BFD for all NR bands of this band combination where the UE supports SpCell.
	- per:: BC
	  mandatory:: No
	  fdd-tdd-diff:: N/A
	  fr1-fr2-diff:: N/A
	  **scg-ActivationDeactivationNRDC-r17**
		- Indicates whether the UE supports [activation (with or without RACH) and deactivation on SCG]([[3GPP/SCG (de)activation]]) in NR-DC, upon SCG addition and upon reconfiguration of the SCG, as specified in TS 38.331 [9]. A UE supporting this feature shall indicate support of NR-DC as specified in TS 38.331 [9]. For the UE supporting this feature, it is mandatory to report maxNumberCSI-RS-BFD and maxNumberSSB-BFD for all NR bands of this band combination where the UE supports SpCell.
	- per:: BC
	  mandatory:: No
	  fdd-tdd-diff:: N/A
	  fr1-fr2-diff:: N/A
	  scg-ActivationDeactivationResumeNRDC-r17
		- Indicates whether the UE supports [activation (with or without RACH) and deactivation on SCG]([[3GPP/SCG (de)activation]]) in NR-DC, upon reception of an RRCReconfiguration included in an RRCResume message, as specified in TS 38.331 [9]. A UE supporting this feature shall indicate support of NR-DC and of resumeWithSCG-Config-r16 as specified in TS 38.331 [9]. For the UE supporting this feature, it is mandatory to report maxNumberCSI-RS-BFD and maxNumberSSB-BFD for all NR bands of this band combination where the UE supports SpCell.