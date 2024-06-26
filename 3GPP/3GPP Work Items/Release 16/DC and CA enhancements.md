---
type: 3GPP Work Item
release: 16
acronym: LTE_NR_DC_CA_enh-Core
---

- WID: https://www.3gpp.org/ftp/TSG_RAN/TSG_RAN/TSGR_88e/Docs/RP-200791.zip

## Objectives

1. Support of asynchronous and synchronous NR-NR Dual Connectivity
2. **Early measurement reporting:** Early and fast reporting of measurements information availability from neighbor and serving cells to reduce delay setting up MR-DC and/or CA
3. **Efficient and low latency serving cell configuration/activation/setup:** Minimizing signalling overhead and latency needed for initial cell setup, additional cell setup and additional cell activation for data transmission
4. **Fast recovery:** Support fast recovery of MCG link e.g. by utilizing the SCG link and split SRBs for recovery during MCG failure while operating under MR-DC
5. **Cross-carrier scheduling with different numerologies** on the scheduling and scheduled carriers
6. Study and, if found beneficial over the existing single Tx switched uplink solution, specify enhancements to single Tx switched uplink solution for EN-DC, such as allowing all DL and UL subframes for data transmission for both NR and LTE
7. Enable the Release 15 behaviour of “DL HARQ timing for FDD Scell for LTE TDD-FDD CA with TDD Pcell, applied to FDD Pcell” to apply to dual uplink EN-DC, possibly including any conclusions on the previous objective (6) for LTE FDD Pcells
8. Specify the interruption requirements for EN-DC and NE-DC related to features added during the Rel-15 LTE euCA WI
9. Introduce support for aperiodic CSI-RS triggering with different numerology between CSI-RS and triggering PDCCH
10. Introduce support for unaligned frame boundary with slot alignment and partial SFN alignment for R16 NR inter-band CA
