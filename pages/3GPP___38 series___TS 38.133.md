alias:: 🏷 NR; Requirements for support of radio resource management
repository:: https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3204

- ## 8.2 Interruption
	- ### 8.2.4 NR-DC: Interruptions
		- #### 8.2.4.2 Requirements
			- ##### 8.2.4.2.16 Interruptions at [SCG activation/deactivation]([[3GPP/NR/SCG (de)activation]])
				- When SCG is activated or deactivated using an RRCConnectionReconfiguration message as defined in TS 38.331 [2], the UE is allowed an interruption on any activated serving cell in MCG during the RRC reconfiguration procedure as follows:
					- an interruption on any active serving cell in MCG:
						- of up to the duration shown in table 8.2.4.2.16-1, if the active serving cell is not in the same band as the PSCell being activated or deactivated, where the requriements for Sync apply for synchronous NR-DC. The requriements for Async apply for asynchronous NR-DC.
						- Table 8.2.4.2.16-1: Interruption duration for SCG activation/deactivation for inter-band DC/CA
						  ![image.png](../assets/image_1687358417216_0.png)
			- ##### 8.2.4.2.17 Interruptions due to RRM measurements on [deactivated SCG]([[3GPP/NR/SCG (de)activation]])
				- If the UE is not configured with RLM or BFD on the deactivated PSCell, interruptions on PCell or activated SCell(s) due to measurements on the deactivated PSCell are allowed with up to 0.5% probability of missed ACK/NACK feedback when the configured measCyclePSCell is 640ms or longer. The UE is only allowed to cause interruptions on PCell or activated SCell(s) immediately before and immediately after an SMTC. Each interruption shall not exceed requirement in Table 8.2.2.2.2-1.
				- If the UE is configured with RLM or BFD on the deactivated PSCell, the rate of ACK/NACK feedback loss on any active serving cell resulting from RRM measurements on the deactivated PSCell shall not exceed 1.0%.
- ## 8.17 [SCG Activation and Deactivation]([[3GPP/NR/SCG (de)activation]]) Delay
	- ### 8.17.1	Introduction
		- This clause defines requirements for the delay within which the UE shall be able to activate one SCG and deactivate on SCG.
		- The requirements shall apply for NR-DC with an NR PCell, PSCell or SCell.
	- ### 8.17.2	SCG Activation Delay Requirement
		- The requirements in this clause shall apply for the UE configured with one deactivated SCG in NR-DC and when PScell in one SCG is being activated.
		- The delay within which the UE shall be able to activate the deactivated SCG depends upon the specified conditions.
		- Upon receiving SCG activation command in slot n, the UE shall be capable to transmit PRACH preamble or PUCCH or PUSCH towards PSCell no later than in slot $n+\frac{T_{activation\_time}}{NR\ slot\ length}$,
			- where:
				- $T_{activation\_time} = T_{RRC\_delay} + T_{processing} + T_{search} + T_∆ + T_{IU} + 2$ ms
				- $T_{RRC\_delay}$ is the RRC procedure delay as specified in TS 38.331 [2].
				- $T_{processing}$ is the SW processing time needed by UE, including RF warm up period. When PSCell is activated from deactivated state, if any PSCell parameter is modified, $T_{processing}$ = 20ms. Otherwise, $T_{processing}$ = 5 ms.	$T_{search}$ is the time for AGC settling and PSS/SSS detection.
				- $T_{search}$ is the time for AGC settling and PSS/SSS detection.
				- For RACH based PSCell activation, if the target cell is a known NR FR2 PSCell, $T_{search}$ = 0 ms. If the target cell is an unknown FR2 PSCell and Es/Iot ≥ -2 dB, then $T_{search}$ = 24* $T_{rs}$ ms.
				- For RACH-less based PSCell activation, if RLM and BFD are configured and TCI state is known, $T_{search}$ = 0 ms if the target cell is a known FR2 PScell. There are no requirements if PSCell is unknown.
				- $T_∆$ is time for fine time tracking and acquiring full timing information of the target PSCell. $T_∆$ = 1*Trs ms.
				- $T_{IU}$: When RACH based PSCell activation is configured, it is the delay uncertainty in acquiring the first available PRACH occasion in the PSCell. $T_{IU}$ is up to the summation of SSB to PRACH occasion association period and 10 ms. SSB to PRACH occasion associated period is defined in Table 8.1-1 of TS 38.213 [3].
				- When RACH-less based PSCell activation is configured, it is the uncertainty in acquiring the first PUSCH transmission occasion [or SR on PUCCH].
				- Trs is the SMTC periodicity of the PSCell if the UE has been provided with an SMTC configuration for the target cell in SCG activation command, otherwise Trs is the SMTC configured in the measObjectNR having the same SSB frequency and subcarrier spacing. If the UE is not provided SMTC configuration or measurement object on this frequency, the requirement in this clause is applied with Trs = 5 ms assuming the SSB transmission periodicity is 5 ms. There is no requirement if the SSB transmission periodicity is not 5.
		- In FR2, the PSCell is known if it has been meeting the following conditions:
			- During the last 5 seconds before the reception of the SCG activation command:
				- the UE has sent a valid measurement report for the PSCell being activated and
				- One of the SSBs measured from the PSCell being activated remains detectable according to the cell identification conditions specified in clause 9.3.
				- One of the SSBs measured from PSCell being activated also remains detectable during the PSCell activation delay $T_{activation\_time}$ according to the cell identification conditions specified in clause 9.3.
		- otherwise it is unknown.
		- If the UE is configured to perform BFD while the SCG is deactivated
			- The TCI state is known if the following conditions are met:
				- During the period from the PSCell deactivation to the completion of PSCell activation, while PSCell was deactivated,
				- UE has not detected beam failure
			- Otherwise, the TCI state is unknown.
		- The PCell interruption specified in clause 8.2 is allowed only during the RRC reconfiguration procedure [2].
	- ### 8.17.3	SCG Deactivation Delay Requirement
		- The requirements in this clause shall apply for a UE which is configured with at least PCell and PScell.
		  Upon receiving RRC-based SCG deactivation command in subframe n, the UE shall accomplish the deactivation actions specified in TS 38.331 [2] no later than in slot $n+\frac{T_{RRC\_delay}}{NR\ slot\ length}$:
			- where
				- $T_{RRC\_delay}$ is the RRC procedure delay as specified in TS 38.331 [2].
		- The PCell interruption specified in clause 8.2 is allowed only during the RRC reconfiguration procedure [2].