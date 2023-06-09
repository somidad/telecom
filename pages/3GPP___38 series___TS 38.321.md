alias:: 🏷 NR MAC
Repository:: https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3194

- ### 5.1.1a Initialization of variables specific to Random Access type
	- The MAC entity shall:
		- 1>	if RA_TYPE is set to 2-stepRA:
			- 2>	set PREAMBLE_POWER_RAMPING_STEP to msgA-PreamblePowerRampingStep;
			- 2>	set SCALING_FACTOR_BI to 1;
			- 2>	apply preambleTransMax included in the RACH-ConfigGenericTwoStepRA;
			- 2>	if the Random Access procedure was initiated for reconfiguration with sync or for [SCG activation]([[3GPP/NR/SCG (de)activation]]); and
			- 2>	if cfra-TwoStep is configured for the selected carrier:
				- 3>	if msgA-TransMax is configured in the cfra-TwoStep:
					- 4>	apply msgA-TransMax configured in the cfra-TwoStep.
			- 2>	else if msgA-TransMax is included in the RACH-ConfigCommonTwoStepRA:
				- 3>	apply msgA-TransMax included in the RACH-ConfigCommonTwoStepRA.
			- 2>	if the Random Access procedure was initiated for SpCell beam failure recovery (as specified in clause 5.17); and
			- 2>	if beamFailureRecoveryConfig is configured for the active UL BWP of the selected carrier; and
			- 2>	if ra-PrioritizationTwoStep is configured in the beamFailureRecoveryConfig:
				- 3>	set PREAMBLE_POWER_RAMPING_STEP to the powerRampingStepHighPriority included in the ra-PrioritizationTwoStep in beamFailureRecoveryConfig;
				- 3>	if scalingFactorBI is configured in the ra-PrioritizationTwoStep in beamFailureRecoveryConfig:
					- 4>	set SCALING_FACTOR_BI to the scalingFactorBI.
			- 2>	else if the Random Access procedure was initiated for reconfiguration with sync or for [SCG activation]([[3GPP/NR/SCG (de)activation]]); and
			- 2>	if rach-ConfigDedicated is configured for the selected carrier; and
			- 2>	if ra-PrioritizationTwoStep is configured in the rach-ConfigDedicated:
				- 3>	set PREAMBLE_POWER_RAMPING_STEP to the powerRampingStepHighPriority included in the ra-PrioritizationTwoStep in rach-ConfigDedicated;
				- 3>	if scalingFactorBI is configured in ra-PrioritizationTwoStep in the rach-ConfigDedicated:
					- 4>	set SCALING_FACTOR_BI to the scalingFactorBI.
			- 2>	else if both ra-PrioritizationForSlicingTwoStep for a NSAG-ID and ra-PrioritizationForAccessIdentityTwoStep are configured for the selected carrier; and
			- 2>	if the MAC entity is provided by upper layers with both this NSAG-ID and Access Identity 1 or 2; and
			- 2>	if for at least one of these Access Identities the corresponding bit in the ra-PrioritizationForAI is set to one:
				- 3>	if enableRA-PrioritizationForSlicing is set to true:
					- 4>	if powerRampingStepHighPriority is configured in the ra-PrioritizationForSlicingTwoStep for this NSAG-ID:
						- 5>	set PREAMBLE_POWER_RAMPING_STEP to the powerRampingStepHighPriority.
					- 4>	if scalingFactorBI is configured in the ra-PrioritizationForSlicingTwoStep for this NSAG-ID:
						- 5>	set SCALING_FACTOR_BI to the scalingFactorBI.
				- 3>	else if enableRA-PrioritizationForSlicing is set to false:
					- 4>	if powerRampingStepHighPriority is configured in the ra-PrioritizationForAccessIdentityTwoStep:
						- 5>	set PREAMBLE_POWER_RAMPING_STEP to the powerRampingStepHighPriority.
					- 4>	if scalingFactorBI is configured in the ra-PrioritizationForAccessIdentityTwoStep:
						- 5>	set SCALING_FACTOR_BI to the scalingFactorBI.
			- 2>	else if ra-PrioritizationForSlicingTwoStep for a NSAG-ID is configured for the selected carrier; and
			- 2>	if the MAC entity is provided by upper layers with this NSAG-ID:
				- 3>	if powerRampingStepHighPriority is configured in the ra-PrioritizationForSlicingTwoStep for this NSAG-ID:
					- 4>	set PREAMBLE_POWER_RAMPING_STEP to the powerRampingStepHighPriority.
				- 3>	if scalingFactorBI is configured in the ra-PrioritizationForSlicingTwoStep for this NSAG-ID:
					- 4>	set SCALING_FACTOR_BI to the scalingFactorBI.
			- 2>	else if ra-PrioritizationForAccessIdentityTwoStep is configured for the selected carrier; and
			- 2>	if the MAC entity is provided by upper layers with Access Identity 1 or 2; and
			- 2>	if for at least one of these Access Identities the corresponding bit in the ra-PrioritizationForAI is set to one:
				- 3>	if powerRampingStepHighPriority is configured in the ra-PrioritizationForAccessIdentityTwoStep:
					- 4>	set PREAMBLE_POWER_RAMPING_STEP to the powerRampingStepHighPriority.
				- 3>	if scalingFactorBI is configured in the ra-PrioritizationForAccessIdentityTwoStep:
					- 4>	set SCALING_FACTOR_BI to the scalingFactorBI.
			- 2>	set MSGA_PREAMBLE_POWER_RAMPING_STEP to PREAMBLE_POWER_RAMPING_STEP.
		- 1>	else (i.e. RA_TYPE is set to 4-stepRA):
			- 2>	set PREAMBLE_POWER_RAMPING_STEP to powerRampingStep;
			- 2>	set SCALING_FACTOR_BI to 1;
			- 2>	set preambleTransMax to preambleTransMax included in the RACH-ConfigGeneric;
			- 2>	if the Random Access procedure was initiated for SpCell beam failure recovery (as specified in clause 5.17); and
			- 2>	if beamFailureRecoveryConfig is configured for the active UL BWP of the selected carrier:
				- 3>	start the beamFailureRecoveryTimer, if configured;
				- 3>	apply the parameters powerRampingStep, preambleReceivedTargetPower, and preambleTransMax configured in the beamFailureRecoveryConfig.
			- 2>	if the Random Access procedure was initiated for beam failure recovery (as specified in clause 5.17); and
			- 2>	if beamFailureRecoveryConfig is configured for the active UL BWP of the selected carrier; and
			- 2>	if ra-Prioritization is configured in the beamFailureRecoveryConfig:
				- 3>	set PREAMBLE_POWER_RAMPING_STEP to the powerRampingStepHighPriority included in the ra-Prioritization in beamFailureRecoveryConfig;
				- 3>	if scalingFactorBI is configured in ra-Prioritization in the beamFailureRecoveryConfig:
					- 4>	set SCALING_FACTOR_BI to the scalingFactorBI.
			- 2>	else if the Random Access procedure was initiated for reconfiguration with sync or for [SCG activation]([[3GPP/NR/SCG (de)activation]]); and
			- 2>	if rach-ConfigDedicated is configured for the selected carrier; and
			- 2>	if ra-Prioritization is configured in the rach-ConfigDedicated:
				- 3>	set PREAMBLE_POWER_RAMPING_STEP to the powerRampingStepHighPriority included in the ra-Prioritization in rach-ConfigDedicated;
				- 3>	if scalingFactorBI is configured in ra-Prioritization in the rach-ConfigDedicated:
					- 4>	set SCALING_FACTOR_BI to the scalingFactorBI.
			- 2>	else if both ra-PrioritizationForSlicing for a NSAG-ID and ra-PrioritizationForAccessIdentity are configured for the selected carrier; and
			- 2>	if the MAC entity is provided by upper layers with both this NSAG-ID and Access Identity 1 or 2; and
			- 2>	if for at least one of these Access Identities the corresponding bit in the ra-PrioritizationForAI is set to one:
				- 3>	if enableRA-PrioritizationForSlicing is set to true:
					- 4>	if powerRampingStepHighPriority is configured in the ra-PrioritizationForSlicing for this NSAG-ID:
						- 5>	set PREAMBLE_POWER_RAMPING_STEP to the powerRampingStepHighPriority.
					- 4>	if scalingFactorBI is configured in the ra-PrioritizationForSlicing for this NSAG-ID:
						- 5>	set SCALING_FACTOR_BI to the scalingFactorBI.
				- 3>	else if enableRA-PrioritizationForSlicing is set to false:
					- 4>	if powerRampingStepHighPriority is configured in the ra-PrioritizationForAccessIdentity:
						- 5>	set PREAMBLE_POWER_RAMPING_STEP to the powerRampingStepHighPriority.
					- 4>	if scalingFactorBI is configured in the ra-PrioritizationForAccessIdentity:
						- 5>	set SCALING_FACTOR_BI to the scalingFactorBI.
			- 2>	else if ra-PrioritizationForSlicing for a NSAG-ID is configured for the selected carrier; and
			- 2>	if the MAC entity is provided by upper layers with this NSAG-ID:
				- 3>	if powerRampingStepHighPriority is configured in the ra-PrioritizationForSlicing for this NSAG-ID:
					- 4>	set PREAMBLE_POWER_RAMPING_STEP to the powerRampingStepHighPriority.
				- 3>	if scalingFactorBI is configured in the ra-PrioritizationForSlicing for this NSAG-ID:
					- 4>	set SCALING_FACTOR_BI to the scalingFactorBI.
			- 2>	else if ra-PrioritizationForAccessIdentity is configured for the selected carrier; and
			- 2>	if the MAC entity is provided by upper layers with Access Identity 1 or 2; and
			- 2>	if for at least one of these Access Identities the corresponding bit in the ra-PrioritizationForAI is set to one:
				- 3>	if powerRampingStepHighPriority is configured in the ra-PrioritizationForAccessIdentity:
					- 4>	set PREAMBLE_POWER_RAMPING_STEP to the powerRampingStepHighPriority.
				- 3>	if scalingFactorBI is configured in the ra-PrioritizationForAccessIdentity:
					- 4>	set SCALING_FACTOR_BI to the scalingFactorBI.
			- 2>	if RA_TYPE is switched from 2-stepRA to 4-stepRA during this Random Access procedure:
				- 3>	set POWER_OFFSET_2STEP_RA to (PREAMBLE_POWER_RAMPING_COUNTER – 1) × (MSGA_PREAMBLE_POWER_RAMPING_STEP – PREAMBLE_POWER_RAMPING_STEP).
	- NOTE:	If enableRA-PrioritizationForSlicing is not configured in BWP-UplinkCommon and if both the provided NSAG-ID and the provided Access Identity whose corresponding bit in the ra-PrioritizationForAI is set to one are configured with ra-Prioritization either in RACH-ConfigCommon or RACH-ConfigCommonTwoStepRA, it is up to UE implementation how to determine the values of PREAMBLE_POWER_RAMPING_STEP and SCALING_FACTOR_BI.
- ### 5.4.6 Power Headroom Reporting
	- The Power Headroom reporting procedure is used to provide the serving gNB with the following information:
		- Type 1 power headroom: the difference between the nominal UE maximum transmit power and the estimated power for UL-SCH transmission per activated Serving Cell;
		- Type 2 power headroom: the difference between the nominal UE maximum transmit power and the estimated power for UL-SCH and PUCCH transmission on SpCell of the other MAC entity (i.e. E-UTRA MAC entity in EN-DC, NE-DC, and NGEN-DC cases);
		- Type 3 power headroom: the difference between the nominal UE maximum transmit power and the estimated power for SRS transmission per activated Serving Cell;
		- MPE P-MPR: the power backoff to meet the MPE FR2 requirements for a Serving Cell operating on FR2.
	- (Omitted)
- ## 5.29 [Activation/Deactivation of SCG]([[3GPP/NR/SCG (de)activation]])
	- The network may activate and deactivate the configured SCG.
	- The MAC entity shall for the configured SCG:
		- 1>	if upper layers indicate that SCG is activated:
			- 2>	if BFI_COUNTER >= beamFailureInstanceMaxCount for the PSCell or the timeAlignmentTimer associated with PTAG is not running:
				- 3>	indicate to upper layers that a Random Access Procedure (as specified in clause 5.1.1) is needed for SCG activation.
			- 2>	activate the SCG according to the timing defined in TS 38.133 [11].
			- 2>	(re-)initialize any suspended configured uplink grants of configured grant Type 1 associated with this PSCell according to the stored configuration, if any, and to start in the symbol according to rules in clause 5.8.2.2;
			- 2>	apply normal SCG operation including:
				- 3>	SRS transmissions on the PSCell;
				- 3>	CSI reporting for the PSCell;
				- 3>	PDCCH monitoring on the PSCell;
				- 3>	PUCCH transmissions on the PSCell;
				- 3>	transmit on RACH on the PSCell;
				- 3>	initialize Bj for each logical channel to zero.
		- 1>	else if upper layers indicate that the SCG is deactivated:
			- 2>	deactivate all the SCells of the SCG according to clause 5.9;
			- 2>	deactivate SCG according to the timing defined in TS 38.133 [11];
			- 2>	clear any configured downlink assignment and any configured uplink grant Type 2 associated with the PSCell respectively;
			- 2>	suspend any configured uplink grant Type 1 associated with the PSCell;
			- 2>	reset MAC according to clause 5.12.
		- 1>	if the SCG is deactivated:
			- 2>	not transmit SRS on the PSCell;
			- 2>	not report CSI for the PSCell;
			- 2>	not transmit on UL-SCH on the PSCell;
			- 2>	not transmit PUCCH on the PSCell;
			- 2>	not transmit on RACH on the PSCell;
			- 2>	not monitor the PDCCH on the PSCell.