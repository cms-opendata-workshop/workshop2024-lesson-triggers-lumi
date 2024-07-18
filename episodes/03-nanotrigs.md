---
Title: "Triggers in NanoAOD"
teaching: 15
exercises: 0
---

:::::::::::::::: questions

- What information for triggers can I find in NanoAOD?
- What information is not available in NanoAOD?

::::::::::::::::

:::::::::::::::: objectives

- Identify the L1 and HLT information in NanoAOD
- Learn alternate methods of accessing prescale information
- Access resources to learn about trigger object information in MiniAOD files

:::::::::::::::::

## Triggers in NanoAOD

For many physics analyses, one basic piece of trigger information is required: did this event pass or fail a certain path?
NanoAOD stores this information for both L1 and HLT paths. Let's consider 3 example HLT paths:

 * HLT_Ele35_WPTight_Gsf
 * HLT_IsoMu27
 * HLT_IsoMu27_LooseChargedIsoPFTauHPS20_Trk1_eta2p1_SingleL1

The first element of the name indicates that these paths are part of the "High Level Trigger" mentioned in the introduction.
The second element of the name shows the first physics object that was tested for this path -- the first example is an electron trigger, and the other two are muon triggers.
Following the short name "Ele" or "Mu" is a momentum/energy threshold for this object, measured in GeV. The example "HLT_IsoMu27" has another feature in the name: "Iso". This indicates that the muon is required to be isolated. Adding isolation requirements helps keep the momentum threshold for this popular trigger low without overwhelming the CMS trigger bandwidth.

The final example shows a trigger with multiple objects -- after the "IsoMu27" label comes a label related to tau leptons: "LooseChargedIsoPFTauHPS20_Trk1_eta2p1_SingleL1".
This is a complex label that would share with experts many details of how the tau passing this trigger appeared in the CMS calorimeters. The most important information is that
this tau lepton decayed to hadrons (note the "HPS" label for "hadron plus strips), was loosely isolated from other charged hadrons, passed a 20 GeV threshold, and was found in the central region of the detector ($\eta < 2.1$). This trigger might be used for a $H \rightarrow \tau \tau$ analysis with one hadronic tau and one tau that decayed to a muon. 

### NanoAOD branch listings

Each dataset's record page contains a link to its variable listing, which will show the full list of L1 and HLT paths available in that dataset. We will show short examples below.

Note:

 * No version number appears in the branch names! NanoAOD assumes you want all versions of a trigger
 * All the branches are type "bool", so they indicate pass (true) or fail (false) for the event
 * Some L1 paths relate to detector conditions, and some to energy thresholds
 * Many triggers of the same type exist with a variety of energy or momentum thresholds

Table: L1 information in NanoAOD (truncated example)

| Object property | Type | Description |
| --------------- | ---- | ----------- |
| L1_AlwaysTrue | Bool_t | Trigger/flag bit (process: NANO) |
| L1_BPTX_AND_Ref4_VME | Bool_t | Trigger/flag bit (process: NANO) |
| L1_BPTX_BeamGas_B1_VME | Bool_t | Trigger/flag bit (process: NANO) |
| L1_BPTX_BeamGas_B2_VME | Bool_t | Trigger/flag bit (process: NANO) |
| L1_BPTX_BeamGas_Ref1_VME | Bool_t | Trigger/flag bit (process: NANO) |
| L1_BPTX_BeamGas_Ref2_VME | Bool_t | Trigger/flag bit (process: NANO) |
| L1_BPTX_NotOR_VME | Bool_t | Trigger/flag bit (process: NANO) |
| L1_BptxMinus | Bool_t | Trigger/flag bit (process: NANO) |
| L1_BptxOR | Bool_t | Trigger/flag bit (process: NANO) |
| L1_BptxPlus | Bool_t | Trigger/flag bit (process: NANO) |
| L1_BptxXOR | Bool_t | Trigger/flag bit (process: NANO) |
| L1_CDC_SingleMu_3_er1p2_TOP120_DPHI2p618_3p142 | Bool_t | Trigger/flag bit (process: NANO) |
| L1_DoubleEG8er2p5_HTT260er | Bool_t | Trigger/flag bit (process: NANO) |
| L1_DoubleEG8er2p5_HTT320er | Bool_t | Trigger/flag bit (process: NANO) |
| L1_DoubleEG8er2p5_HTT340er | Bool_t | Trigger/flag bit (process: NANO) |
| L1_DoubleEG_15_10_er2p5 | Bool_t | Trigger/flag bit (process: NANO) |
| L1_DoubleEG_20_10_er2p5 | Bool_t | Trigger/flag bit (process: NANO) |

Table: HLT information in NanoAOD (truncated example)

| Object property | Type | Description |
| --------------- | ---- | ----------- |
| HLT_Ele30_WPTight_Gsf | Bool_t | Trigger/flag bit (process: HLT) |
| HLT_Ele30_eta2p1_WPTight_Gsf_CentralPFJet35_EleCleaned | Bool_t | Trigger/flag bit (process: HLT) |
| HLT_Ele32_WPTight_Gsf | Bool_t | Trigger/flag bit (process: HLT) |
| HLT_Ele32_WPTight_Gsf_L1DoubleEG | Bool_t | Trigger/flag bit (process: HLT) |
| HLT_Ele35_WPTight_Gsf | Bool_t | Trigger/flag bit (process: HLT) |
| HLT_Ele35_WPTight_Gsf_L1EGMT | Bool_t | Trigger/flag bit (process: HLT) |
| HLT_Ele38_WPTight_Gsf | Bool_t | Trigger/flag bit (process: HLT) |
| HLT_IsoMu27 | Bool_t | Trigger/flag bit (process: HLT) |
| HLT_IsoMu27_LooseChargedIsoPFTauHPS20_Trk1_eta2p1_SingleL1 | Bool_t | Trigger/flag bit (process: HLT) |
| HLT_IsoMu27_MET90 | Bool_t | Trigger/flag bit (process: HLT) |
| HLT_IsoMu27_MediumChargedIsoPFTauHPS20_Trk1_eta2p1_SingleL1 | Bool_t | Trigger/flag bit (process: HLT) |
| HLT_IsoMu27_TightChargedIsoPFTauHPS20_Trk1_eta2p1_SingleL1 | Bool_t | Trigger/flag bit (process: HLT) |
| HLT_IsoMu30 | Bool_t | Trigger/flag bit (process: HLT) |
| HLT_IsoTrackHB | Bool_t | Trigger/flag bit (process: HLT) |
| HLT_IsoTrackHE | Bool_t | Trigger/flag bit (process: HLT) |
| HLT_Mu48NoFiltersNoVtx_Photon48_CaloIdL | Bool_t | Trigger/flag bit (process: HLT) |
| HLT_Mu4_TrkIsoVVL_DiPFJet90_40_DEta3p5_MJJ750_HTT300_PFMETNoMu60 | Bool_t | Trigger/flag bit (process: HLT) |
| HLT_Mu50 | Bool_t | Trigger/flag bit (process: HLT) |
| HLT_Mu50_IsoVVVL_PFHT450 | Bool_t | Trigger/flag bit (process: HLT) |

::::::::::: callout

## What is the "process"?

CMS processes data in many steps (RECO, HLT, PAT, NANO...). These branches in NanoAOD are marking for the user which processing step produced the information seen in the NanoAOD file.

:::::::::::

## L1 PreFiring corrections

The 2016 NanoAOD files also contain a set of branches labeled "L1PreFiringWeight". In 2016 and 2017, the gradual timing shift of the ECAL was not properly propagated to the L1 trigger system, resulting in a significant fraction of high-$\eta$ "trigger primitives" being mistakenly associated to the previous bunch crossing. Since Level-1 rules forbid two consecutive bunch crossings from firing, an unpleasant consequence of this is that events can effectively "self veto" if a significant amount of ECAL energy is found in the region $2.0 < |\eta| < 3.0$. The effect is strongly $\eta$- and $p_{T}$-dependent and prefiring rates can be large for high-momentum jets in the forward regions of the detector. A similar effect is present in the muon system, where the bunch crossing assignment of the muon candidates can be wrong due to the limited time resolution of the muon detectors. This effect was most pronounced in 2016, and the magnitude varies between 0% and 3%. 

The L1PreFiring table in NanoAOD provides weights that analysts can apply to simulation to correct for these effects, so that simulation better represents data. The weights carry associated uncertainties, represented in alternate branches. 

| Object property | Type | Description |
| --------------- | ---- | ----------- |
| L1PreFiringWeight_Dn | Float_t | L1 pre-firing event correction weight (1-probability), down var. |
| L1PreFiringWeight_ECAL_Dn | Float_t | ECAL L1 pre-firing event correction weight (1-probability), down var. |
| L1PreFiringWeight_ECAL_Nom | Float_t | ECAL L1 pre-firing event correction weight (1-probability) |
| L1PreFiringWeight_ECAL_Up | Float_t | ECAL L1 pre-firing event correction weight (1-probability), up var. |
| L1PreFiringWeight_Muon_Nom | Float_t | Muon L1 pre-firing event correction weight (1-probability) |
| L1PreFiringWeight_Muon_StatDn | Float_t | Muon L1 pre-firing event correction weight (1-probability), down var. stat. |
| L1PreFiringWeight_Muon_StatUp | Float_t | Muon L1 pre-firing event correction weight (1-probability), up var. stat. |
| L1PreFiringWeight_Muon_SystDn | Float_t | Muon L1 pre-firing event correction weight (1-probability), down var. syst. |
| L1PreFiringWeight_Muon_SystUp | Float_t | Muon L1 pre-firing event correction weight (1-probability), up var. syst. |
| L1PreFiringWeight_Nom | Float_t | L1 pre-firing event correction weight (1-probability) |
| L1PreFiringWeight_Up | Float_t | L1 pre-firing event correction weight (1-probability), up var. |
 
## What's missing from NanoAOD?

NanoAOD does not contain information about trigger **prescales** or **objects**:

 * The prescale is a "scale down factor" for triggers with rates too high to record all events
 * A trigger object is a link to the electron, muon, jet, tau, etc, that specifically satisfied the criteria for a given trigger filter

Prescale information is fixed in the "trigger menu", so it can be accessed outside of NanoAOD. While it's common for prescale values to change from run to run, most
analysts are only interested in determining whether or not a trigger is prescaled at all. If not, that trigger is a good candidate for analyses requiring the full 
amount of data available. If so, the trigger is better suited to studies where statistics are not a limiting factor. Prescale values for any trigger can be accessed 
from the `brilcalc` tool that we will discuss in the upcoming episodes. We will practice finding a prescale value as an exercise. 

Trigger object information is important if an analysis needs to know which specific objects passed a certain set of trigger filters. So for instance, if you needed
to know which tau leptons satisfied `LooseChargedIsoPFTauHPS20_Trk1_eta2p1_SingleL1` in order to make correct analysis choices, then you would need access to trigger
object details. Many analyses do not require this level of detail, since physics objects can usually be selected using the identification and isolation algorithms designed
to be applied separately from the trigger system. Trigger objects can be accessed in MiniAOD -- follow our [trigger lesson for 2015 MiniAOD from 2023](https://cms-opendata-workshop.github.io/workshop2023-lesson-selection/03-miniaodtrigger/index.html) to learn more.

::::::::::::::::: keypoints

- NanoAOD stores basic pass/fail information for both L1 and HLT paths
- NanoAOD does not contain trigger prescale or trigger object information
- Trigger prescale information can be accessed from brilcalc
- Trigger object information must be accessed by processing MiniAOD files in CMSSW

:::::::::::::::::
