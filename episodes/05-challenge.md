---
title: "Trigger & Lumi challenge"
teaching: 0
exercises: 30
---

::::::::::::: questions

- Which triggers are likely the most useful for selecting top quark events?
- What are the prescale values of some possible triggers?
- What is the luminosity collected by my chosen trigger?

:::::::::::::

::::::::::::: objectives

- Learn to make trigger choices based on analysis goals, expected physics objects, and available trigger paths.
- Practice using brilcalc to extract trigger prescale information
- Practice using brilcalc to compute integrated luminosity

:::::::::::::

:::::::::::::::: testimonial

## Workshop analysis example: $Z' \rightarrow t\bar{t} \rightarrow (bjj)(b\ell\nu)$

Later in the workshop we will search for a Z' boson that decays to a top quark-antiquark pair. The signal for this measurement is one top quark that decays hadronically, and one top quark that decays leptonically, to either a muon or an electron. For Z' bosons with mass in the 1 - 5 TeV range, the top quarks should both be produced with high momentum. 

:::::::::::::::::

## Choosing a trigger path

Using what you have learned about CMS physics objects and triggers, let's sketch out some ideas for potential trigger selections. To begin with:

**Which final state particles would you expect to observe in the detector from your "signal" process?**

Based on these particles, consider:
 * Which physics objects could appear in a useful trigger path? At a hadron collider, which physics objects might be *best* for triggering?
 * What kinematic conditions do you expect for the trigger physics objects?
 * We saw trigger "trade-offs", like requiring isolated particles in exchange for lower momenta -- would that trade-off be beneficial in this case?

::::::::: challenge

## Physics exercise: choose trigger paths

Visit the NanoAOD [HLT branch listing for our signal sample](https://opendata.cern.ch/eos/opendata/cms/dataset-semantics/NanoAODSIM/75156/ZprimeToTT_M2000_W20_TuneCP2_PSweights_13TeV-madgraph-pythiaMLM-pythia8_doc.html#HLT) and choose 3-4 trigger options that might be effective for selecting $Z' \rightarrow t\bar{t}$ events

::::: solution

For the $t\bar{t}$ final state we will consider, we expect one electron or muon, MET from the accompanying neutrino, and several jets, some of which could be tagged as b quark jets. There might even be "fat jets" tagged as entire top quark decays. This analysis is perfect for the common "single lepton" triggers. Since the top quarks will be produced with high momentum, the lepton might not be well separated from a b quark jet, so it would be wisest to include a non-isolated trigger. Since the signal will likely produce high-pT leptons, we can afford to use triggers that require higher momentum in order to relax isolation requirements. 

The triggers used in the CMS analysis that we are mimicking were:

 * HLT_Mu50
 * HLT_Ele50_CaloIdVT_GsfTrkIdT_PFJet165
 * HLT_Ele115_CaloIdVT_GsfTrkIdT

For any of these triggers, the leptons (and jet, if applicable) should ideally be selected using criteria that put them in the "efficiency plateau" of the trigger. For example, the HLT_Mu50 trigger is designed to select muons with at least 50 GeV of transverse momentum, but if you plotted the number of muons selected as a function of pT, you would certainly not see a vertical line step function with 0 muons selected below 50 GeV and 100% of muons selected above 50 GeV. Right in the region of the threshold there will be a "turn-on" effect where the efficiency rises quickly, but not exactly following a step function. This turn-on can be difficult to model well in simulation, so many analysts choose selection criteria for physics objects that will not be subject to the turn-on effects of the trigger. For example, in an analysis using HLT_Mu50, the muon selection criteria would typically be pT > 55 GeV.

:::::

:::::::::::

## Brilcalc exercises

:::::::::::: prereq

These exercises will be performed using the `brilws` container that you installed at the beginning of the lesson. If you have exited that container, restart it:

```bash
docker start -i brilws
```

:::::::::::::

::::::::::::: challenge

## Exercise 1: test brilcalc

As a test, let's see what the integrated luminosity was for run 284044 by running the command:

```bash
brilcalc lumi -c web -r 284044
```

Note: It is important that you use the `-c web` option when running brilcalc. This specifies that you use indirect access to BRIL servers via a web cache.
For users of CMS open data outside CERN and CMS this is the only option that will work.

::::::: solution

You should see the following output:

```output
#Data tag : 24v1 , Norm tag: onlineresult
+-------------+-------------------+-----+------+-------------------+-------------------+
| run:fill    | time              | nls | ncms | delivered(/ub)    | recorded(/ub)     |
+-------------+-------------------+-----+------+-------------------+-------------------+
| 284044:5451 | 10/26/16 20:46:05 | 594 | 40   | 5450634.956154574 | 4912825.742705812 |
+-------------+-------------------+-----+------+-------------------+-------------------+
#Summary:                                                                               
+-------+------+-----+------+-------------------+-------------------+                   
| nfill | nrun | nls | ncms | totdelivered(/ub) | totrecorded(/ub)  |                   
+-------+------+-----+------+-------------------+-------------------+
| 1     | 1    | 594 | 40   | 5450634.956154574 | 4912825.742705812 |
+-------+------+-----+------+-------------------+-------------------+
```

:::::::

:::::::::::::::

::::::::::::::: challenge

## Exercise 2: 2016 validated runs & luminosity sections

All CMS data is studied by data quality monitoring groups for various subdetectors to determine whether it is suitable for physics analysis.
Data can be accepted or rejected in units of "luminosity sections". These are periods of time covering $2^{18}$ LHC revolutions, or about 23 seconds.
The list of validated runs and luminosity sections is stored in a `json` file that can be downloaded from the Open Data Portal.

First, obtain the file with the list of validated runs and luminosity sections for 2016 data:

```bash
wget https://opendata.cern.ch/record/14220/files/Cert_271036-284044_13TeV_Legacy2016_Collisions16_JSON.txt
```

Use `brilcalc` to display the luminosity for each valid run in the 2016 Open Data. Currently, we have released 2016G and 2016H data, which
contain runs 278820 through 284044. 

```bash
brilcalc lumi -c web -b "STABLE BEAMS" --begin 278820 --end 284044 -i Cert_271036-284044_13TeV_Legacy2016_Collisions16_JSON.txt > 2016GHlumi.txt
```

* Can you identify the run in this range that had the most luminosity sections?
* What is the total recorded luminosity for this run range?

::::::: solution

You can investigate the output file best using `head`:

```bash
head -165 2016GHlumi.txt
```

The longest run is 279931!

```output
#Data tag : 24v1 , Norm tag: onlineresult
+-------------+-------------------+------+------+---------------------+---------------------+
| run:fill    | time              | nls  | ncms | delivered(/ub)      | recorded(/ub)       |
+-------------+-------------------+------+------+---------------------+---------------------+
| 278820:5199 | 08/14/16 11:00:52 | 1524 | 1524 | 300457014.643834889 | 287580217.903829336 |
| 278822:5199 | 08/14/16 21:52:48 | 1627 | 1627 | 195829703.718308955 | 189724216.323258847 |
| 278873:5205 | 08/15/16 23:25:46 | 67   | 60   | 12468667.004980152  | 2012170.733444575   |
| 278874:5205 | 08/15/16 23:51:54 | 484  | 484  | 88533994.547763854  | 82142606.203014016  |
| 278875:5205 | 08/16/16 03:01:21 | 834  | 834  | 120598272.705723718 | 115092509.056569114 |
| 278923:5206 | 08/16/16 12:16:33 | 413  | 413  | 103255455.458636224 | 98881486.964829206  |
...
| 279887:5270 | 09/01/16 23:20:53 | 319  | 319  | 76790312.907530844  | 72932440.002667427  |
| 279931:5274 | 09/02/16 11:37:40 | 2936 | 2936 | 485408960.517024338 | 470459175.415192366 |
| 279966:5275 | 09/03/16 09:20:25 | 363  | 363  | 95862775.891636893  | 91937407.130460218  |
| 279975:5276 | 09/03/16 14:45:09 | 1024 | 1024 | 244951346.260912448 | 235979324.421879977 |
```

The units are inverse microbarns as default and can be changed to inverse femtobarns with the option `-u /fb`.

The total recorded luminosity for the run range is listed in the summary below the individual runs:

```bash
head -168 2016GHlumi.txt
```

```output
#Summary:
+-------+------+-------+-------+-----------------------+-----------------------+
| nfill | nrun | nls   | ncms  | totdelivered(/ub)     | totrecorded(/ub)      |
+-------+------+-------+-------+-----------------------+-----------------------+
| 64    | 156  | 90807 | 90526 | 17062540322.934297562 | 16290713419.734096527 |
+-------+------+-------+-------+-----------------------+-----------------------+
```

CMS recorded 16.3 inverse femtobarns of proton-proton collisions in 2016 G and H!

:::::::

::::::::::::::::

:::::::::::::::: challenge

## Exercise 3: selecting the best luminometer

Update to 

For Run-2 data, the luminometer giving the best value for each luminosity section is recorded in a 'normtag' file, provided in the [2016 luminosity information record](https://opendata.cern.ch/record/1059) ('normtag_PHYSICS_pp_2016.json'). Use it with the corresponding list of validated runs from 2016 to find the best estimate of the 2016G-H luminosity. 

```bash
wget https://opendata.cern.ch/record/1059/files/normtag_PHYSICS_pp_2016.json
brilcalc lumi -c web -b "STABLE BEAMS" --begin 278820 --end 284044 -i Cert_271036-284044_13TeV_Legacy2016_Collisions16_JSON.txt -u /fb --normtag normtag_PHYSICS_pp_2016.json > 2016GHlumi_normtag.txt
```

Does it change compared to the previous exercise?

::::::: solution

The summary should now read:

```output
#Summary:
+-------+------+-------+-------+-------------------+------------------+
| nfill | nrun | nls   | ncms  | totdelivered(/fb) | totrecorded(/fb) |
+-------+------+-------+-------+-------------------+------------------+
| 64    | 156  | 90807 | 90526 | 17.168970230      | 16.393380532     |
+-------+------+-------+-------+-------------------+------------------+
```

To three significant figures, the luminosity is better reported as 16.4 inverse femtobarns.

:::::::

::::::::::::::::

:::::::::::::::: challenge

## Exercise 4: Luminosity and prescale values for an HLT trigger path

One of the triggers that is a good candidate for the Z' search example is `HLT_Mu50`. Let's calculate the integrated luminosity covered by this trigger for the long run 279931:

```bash
brilcalc lumi -c web -b "STABLE BEAMS" -r 279931 --hltpath="HLT_Mu50*"
```

Compare this luminosity to the similar trigger `HLT_Mu27` -- what difference do you observe? What is happening to Mu27 that is not occurring for Mu50?

::::::: solution

In run 279931, the luminosity collected with Mu50* is:

```output
+-------------+-------------------+------+-----------------------------+---------------------+---------------------+
| run:fill    | time              | ncms | hltpath                     | delivered(/ub)      | recorded(/ub)       |
+-------------+-------------------+------+-----------------------------+---------------------+---------------------+
| 279931:5274 | 09/02/16 11:36:53 | 2945 | HLT_Mu50_IsoVVVL_PFHT400_v3 | 486636050.343178093 | 471451252.657074332 |
| 279931:5274 | 09/02/16 11:36:53 | 2945 | HLT_Mu50_v4                 | 486636050.343178093 | 471451252.657074332 |
+-------------+-------------------+------+-----------------------------+---------------------+---------------------+
```

The luminosity collected with Mu27* is:

```output
+-------------+-------------------+------+--------------------------------------+---------------------+---------------------+
| run:fill    | time              | ncms | hltpath                              | delivered(/ub)      | recorded(/ub)       |
+-------------+-------------------+------+--------------------------------------+---------------------+---------------------+
| 279931:5274 | 09/02/16 11:36:53 | 2945 | HLT_Mu27_Ele37_CaloIdL_GsfTrkIdVL_v4 | 486636050.343178093 | 471451252.657074332 |
| 279931:5274 | 09/02/16 11:36:53 | 2945 | HLT_Mu27_TkMu8_v3                    | 334796076.249607444 | 325826000.870547831 |
| 279931:5274 | 09/02/16 11:36:53 | 2945 | HLT_Mu27_v4                          | 3373601.765050163   | 3273957.230715709   |
+-------------+-------------------+------+--------------------------------------+---------------------+---------------------+
```

The Mu27 trigger is significantly prescaled!

Note: you could combine the example in this exercise with the brilcalc options `--begin`, `--end`, `-i`, and `--normtag` to confirm the total integrated luminosity for a given trigger path. This command can take a while! If you wish to use wildcards to get results for many trigger paths, you can consider adding `--output-style csv` and redirecting the results to a .csv file for easier analysis.

:::::::

More trigger information for these muon triggers can be seen using `brilcalc trg` with the `--prescale` option:

```bash
brilcalc trg --prescale -c web -r 279931 --hltpath "HLT_Mu27*"
```

What are the prescale values for this trigger?

::::::: solution

```output
+--------+-------+----------+-------------+--------------------+-------+---------------------------------------+
| run    | cmsls | prescidx | totprescval | hltpath/prescval   | logic | l1bit/prescval                        |
+--------+-------+----------+-------------+--------------------+-------+---------------------------------------+
| 279931 | 1     | 2        | 260.00      | HLT_Mu27_v4/260    | OR    | L1_SingleMu22/1.00 L1_SingleMu25/1.00 |
| 279931 | 71    | 6        | 140.00      | HLT_Mu27_v4/140    | OR    | L1_SingleMu22/1.00 L1_SingleMu25/1.00 |
| 279931 | 74    | 2        | 260.00      | HLT_Mu27_v4/260    | OR    | L1_SingleMu22/1.00 L1_SingleMu25/1.00 |
| 279931 | 262   | 3        | 230.00      | HLT_Mu27_v4/230    | OR    | L1_SingleMu22/1.00 L1_SingleMu25/1.00 |
| 279931 | 521   | 4        | 200.00      | HLT_Mu27_v4/200    | OR    | L1_SingleMu22/1.00 L1_SingleMu25/1.00 |
| 279931 | 752   | 5        | 160.00      | HLT_Mu27_v4/160    | OR    | L1_SingleMu22/1.00 L1_SingleMu25/1.00 |
| 279931 | 1088  | 6        | 140.00      | HLT_Mu27_v4/140    | OR    | L1_SingleMu22/1.00 L1_SingleMu25/1.00 |
| 279931 | 1946  | 7        | 100.00      | HLT_Mu27_v4/100    | OR    | L1_SingleMu22/1.00 L1_SingleMu25/1.00 |
```

The total prescale value is the product of any prescale applied at L1 with any prescale applied at HLT. As this long run proceeded, the prescale values changed several times. During a portion of the run this trigger was not allowed to collect any luminosity, and in other portions it was scaled down by at least a factor of 100. In contrast, you can confirm that Mu50 always has a prescale of 1. Any wildcard can be given in the `--hltpath` option to compare many triggers for a certain physics object and find unprescaled options.

:::::::

::::::::::::::::::::


:::::::::::::::::::: keypoints

- 
-
-

:::::::::::::::::::::