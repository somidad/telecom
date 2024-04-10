
## 7.7 SCG/MCG failure handling

TBU

If radio link failure is detected for MCG, fast MCG link recovery is configured and the [SCG is not deactivated](../../3GPP%20features/SCG%20deactivation.md), the UE triggers fast MCG link recovery. Otherwise, the UE initiates the RRC connection re-establishment procedure. During the execution of PSCell addition or PSCell change, if radio link failure is detected for MCG, the UE initiates the RRC connection re-establishment procedure.

TBU

The following SCG failure cases are supported:

- SCG RLF;
- SCG beam failure while the [SCG is deactivated](../../3GPP%20features/SCG%20deactivation.md);
- SN addition/change failure;
- For EN-DC, NGEN-DC and NR-DC, SCG configuration failure or CPC configuration failure (only for messages on SRB3);
- For EN-DC, NGEN-DC and NR-DC, SCG RRC integrity check failure (on SRB3);
- For EN-DC, NGEN-DC and NR-DC, consistent UL LBT failure on PSCell;
- For IAB-MT, reception of a BH RLF indication from SCG;
- CPA/CPC or subsequent CPAC execution failure;
- SCG LTM cell switch failure.

TBU