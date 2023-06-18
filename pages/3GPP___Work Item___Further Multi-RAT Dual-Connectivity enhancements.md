tags:: Rel-17
repository:: https://portal.3gpp.org/desktopmodules/WorkItem/WorkItemDetails.aspx?workitemId=860049

- WID: [RP-201040](https://www.3gpp.org/ftp/TSG_RAN/TSG_RAN/TSGR_88e/Docs/RP-201040.zip)
- [CRs](https://portal.3gpp.org/ChangeRequests.aspx?q=1&workitem=860049)
- # 3 Justification
	- (Omitted)
	- In EN-DC, UE and network power consumption is a big issue, due to maintaining two radio links simultaneously. In some cases NR UE power consumption is 3 to 4 times higher than LTE. In EN-DC deployment, MN provides the basic coverage. When UE data rate requirement changes dynamically, e.g. from high to low, SN is worth considering to be (de)activated to save network and UE energy consumption. This issue has been discussed in Release 16 eDCCA WI and has significant support. But due to time limitation, it is not completed in Release 16. Therefore an efficient SCG (de)activation mechanism should be specified in Release 17. This efficient SCG (de)activation mechanism can also be applied to other MR-DC options.
	- (Omitted)
- # 4 Objective
	- ## 4.1 Objective of SI or Core part WI or Testing part WI
		- The objective of this work item is to specify enhancements to MR-DC related scenarios. At least the following topics should be considered in the work:
			- 1.	Support efficient [activation/de-activation mechanism for one SCG and SCells]([[3GPP/SCG (de)activation]])
				- Support for one SCG  applies to (NG)EN-DC, and NR-DC [RAN2, RAN3, RAN4]
				- Support for SCells applies to NR CA, based on RAN1 leading mechanisms [RAN1, RAN2, RAN4]
				- This objective applies to FR1 and FR2
			- 2.	Support of conditional PSCell change/addition [RAN2,RAN3, RAN4]
				- support scenarios which are not addressed in Rel-16 NR mobility WI