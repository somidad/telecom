- > Title: Further Multi-RAT Dual-Connectivity enhancements
  TDoc: RP-201040
- Justification
	- In EN-DC, UE and network power consumption is a big issue, due to maintaining two radio links simultaneously. In some cases NR UE power consumption is 3 to 4 times higher than LTE. In EN-DC deployment, MN provides the basic coverage. When UE data rate requirement changes dynamically, e.g. from high to low, [SN is worth considering to be (de)activated]([[./SCG (de)activation|SCG (de)activation]]) to save network and UE energy consumption.
	- There are some leftovers from Release 16 eDCCA and mobility enhancement WIs, which have benefits but not be completed due to limited schedule, e.g. conditional PSCell change etc. These issues can also be addressed in Release 17.
- Objectives
	- Support efficient [activation/de-activation mechanism for one SCG]([[./SCG (de)activation|SCG (de)activation]]) and SCells
	- Support of conditional PSCell change/addition [RAN2,RAN3, RAN4]