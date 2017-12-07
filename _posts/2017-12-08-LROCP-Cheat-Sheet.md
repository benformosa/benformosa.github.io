---
layout: default
title: Long Range Operator Certificate of Proficiency Cheat Sheet
categories:
  - blog
tags:
  - radio
  - certification
---

These are my notes taken from the [Marine Radio Operator's Handbook](http://www.amc.edu.au/industry/omc/handbooks-and-revision-questions), in preparation for the LROCP exam.

## Marine Radio Spectrum

### Marine Radio bands

| Band Name           | Abbrv | Freq From | Freq to  | Day     | Night             | Notes                               |
|---------------------|-------|-----------|----------|---------|-------------------|-------------------------------------|
| Medium Frequency    | MF    | 300 kHz   | 3000 kHz | Surface | Surface, Sky      | Sky wave not reliable               |
| High Frequency      | HF    | 3 MHz     | 30 MHz   | Sky     | Sky, longer range | Higher frequency give longer range. |
| Very High Frequency | VHF   | 30 MHz    | 300 MHz  | Surface | Surface           | Range is just more than LOS         |

### All radio bands

| Band | Freq from |
|------|-----------|
| VLF  | 3 kHz     |
| LF   | 30 kHz    |
| MF   | 300 kHz   |
| HF   | 3000 kHz  |
| VHF  | 30 MHz    |
| UHF  | 300 MHz   |
| SHF  | 3 GHz     |
| EHF  | 30 GHz    |
|      | 300 GHz   |

## Agencies

| Agency                                              | Responsibility                       |
|-----------------------------------------------------|--------------------------------------|
| ACMA (Australian Communication and Media Authority) | Government Agency - Creates policies |
| AMSA (Austalian Maritime Safety Authority)          | Issuing MMSIs, register EPIRBs       |
| RCC Australia (Rescue Co-ordination Centre)         | Runs Marine Communication Stations   |
| AusSAR                                              | Operates RCC                         |

## Coast Stations

### Marine Communication Stations (MCS)

* Located in Wiluna, WA and Charleville, QLD
* Controlled by Network Control Centre in Canberra
* SAR operations, continuous watch on HF DSC distress frequencies, automated BOM weather forecasting and alerts
* Identity shared by both stations. MMSI: 00503001, Callsign: "RCC Australia" or "RCC Australia Victor India Charlie"
* Covers Australia's SAR region

### HF Coast Radio

* Operated by States and Territories
* Continuous watch on HF voice distress frequencies: 4125 kHz, 6215 kHz, 8291 kHz
* Covers 200 nautical miles from coast
* Some stations may use VHF - continuous watch on CH 16, weather broadcasts on CH 67

### Limited Coast Stations (LCS)

* May use MF, HF and/or VHF
* May supplement Coast Radio
* No requirement to operate continously or watch distress channels

### VHF Repeater

* Operates in Duplex mode on VHF CH 21, 22, 80, 81 or 82
* Won't relay DSC (CH 70)

## Radio Hardware

### Batteries

* Lead acid batteries are made up of 2 volt cells.
* Lead acid batteries use sulphuric acid, and produce hydrogen gas during operation.
* The electrolyte in lead acid batteries can be topped up with distilled water.
* The hydrometer reading for a fully charged lead acid battery is 1.250.
* Connect batteries in parallel for higher capacity at the same voltage.
* Connect batteries in series for the same capacity with higher voltage.

### Antennae

* A VHF radio antenna is a short vertical whip or rod.

### Radio controls

* Mute - Stop background noise or radio interference.
* Squelch - Prevent constant background roar when the radio is not receiving a transmission.
* Antenna Tuning Unit - Ensure maximum transfer of transmitting power to the antenna at different frequencies.
* Clarifier - Fine-tune distorted incoming Single Side Band transmissions.

## EPIRB

* An Emergency Position Indicating Radio Beacon (EPIRB) broadcasts its position when activated to assist search and rescue operations.
* Transmits on 406 MHz or 121.5 MHz, for a minimum of 48 hours.
* AMSA is responsible for registering EPIRBs in Australia.
* 406 MHz transmissions are received by the COSPAS-SARSAT system, consisting of GEOS and LEOS.
* Five geo-stationary satellites over the equator relay to Local User Terminals on earth
* Four Low Earth Orbiting satellites (LEOS) relay to Local User Terminals on earth, such as at Albany, WA,  Bundaberg, QLD and Wellington, NZ.
* LEOS complete their orbit in around 100 minutes, and cover an area 4000 km across.
* 121.5 MHz transmissions can be received by aircraft.

## MMSI

* Maritime Mobile Service Identities (MMSI) are issued in Australia by AMSA, to uniquely identify stations.
* MMSIs are always included in Digital Selective Calling (DSC) transmissions.
* The first 3 digits of a MMSI indicate the country of registration.
* 00 prefix indicates the MMSI belongs to a coast station.
* 111 prefix indicates the MMSI belongs to a search and rescue aircraft.

## Important Frequencies

| Band   | Channel | Frequency    | Communicate with    | Mode  | Usage                              |
|--------|---------|--------------|---------------------|-------|------------------------------------|
| MF     |         | 2182 kHz     | LCS, Ships          | Voice | Distress, Urgency, Safety calling  |
| MF     |         | 2187.5 kHz   | LCS, Ships          | DSC   | Distress, Urgency, Safety calling  |
| HF     |         | 4125 kHz     | MCS, LCS, Ships     | Voice | Distress, Urgency, Safety calling  |
| HF     |         | 4207.5 kHz   | MCS, LCS, Ships     | DSC   | Distress, Urgency, Safety calling  |
| HF     |         | 6215 kHz     | MCS, LCS, Ships     | Voice | Distress, Urgency, Safety calling  |
| HF     |         | 6312 kHz     | MCS, LCS, Ships     | DSC   | Distress, Urgency, Safety calling  |
| HF     |         | 8176 kHz     | Ships               | Voice | MCS broadcast safety messages      |
| HF     |         | 8291 kHz     | MCS, LCS, Ships     | Voice | Distress, Urgency, Safety calling  |
| HF     |         | 8414.5 kHz   | MCS, LCS, Ships     | DSC   | Distress, Urgency, Safety calling  |
| HF     |         | 12 290 kHz   | MCS, LCS, Ships     | Voice | Distress, Urgency, Safety calling  |
| HF     |         | 12 577 kHz   | MCS, LCS, Ships     | DSC   | Distress, Urgency, Safety calling  |
| HF     |         | 16 420 kHz   | MCS, LCS, Ships     | Voice | Distress, Urgency, Safety calling  |
| HF     |         | 16 804.5 kHz | MCS, LCS, Ships     | DSC   | Distress, Urgency, Safety calling  |
| 27 MHz | 86      | 27.86 MHz    | LCS, Ships          | Voice | Distress, Urgency, Safety calling  |
| 27 MHz | 88      | 27.88 MHz    | LCS, Ships          | Voice | Distress, Urgency, Safety calling  |
| VHF    |         | 121.5 MHz    | Satellite, Aircraft | Data  | EPIRB                              |
| VHF    | 6       | 156.300 MHz  | Ships, Aircraft     | Voice | SAR                                |
| VHF    | 67      | 156.375 MHz  | LCS, Ships          | Voice | Distress, Urgency, Safety calling  |
| VHF    | 70      | 156.525 MHz  | LCS, Ships          | DSC   | Distress, Urgency, Safety calling  |
| VHF    | 13      | 156.650 MHz  | LCS, Ships          | Voice | Intership Maritime safety messages |
| VHF    | 16      | 156.800 MHz  | LCS, Ships          | Voice | Distress, Urgency, Safety calling  |
| UHF    |         | 406.025 MHz  | Satellite           | Data  | EPIRB                              |
| UHF    |         | 406.028 MHz  | Satellite           | Data  | EPIRB with GPS                     |

## Distress, Urgency, Safety

### Signals

| Situation                  | Meaning                                    | Signal                                         |
|----------------------------|--------------------------------------------|------------------------------------------------|
| Distress call              | Immediate grave danger to person or vessel | MAYDAY, MAYDAY, MAYDAY                         |
| Distress message           | Position and nature of distress follows    | MAYDAY                                         |
| Distress message received  | I have received your distress message      | RECEIVED MAYDAY                                |
| Distress - message relay   | Re-transmit received distress message      | MAYDAY RELAY                                   |
| Distress - request silence | Vessel in distress requests radio silence  | SEELONCE MAYDAY                                |
| Distress ended             | Resume normal working                      | SEELONCE FEENEE                                |
| Urgency call               | Urgent safety message                      | PAN PAN, PAN PAN, PAN PAN                      |
| Safety call                | Navigation or weather alert                | SAY-CURE-E-TAY, SAY-CURE-E-TAY, SAY-CURE-E-TAY |

### Distress call and message

```
MAYDAY MAYDAY MAYDAY  
THIS IS  
[Vessel] [Callsign] [Vessel] [Callsign] [Vessel] [Callsign]  
[MMSI (if DSC alert sent)]  
MAYDAY  
[Vessel] [Callsign]
[Position]  
[Nature of distress]  
[Other information]
```

#### Example Distress call and message

```
MAYDAY MAYDAY MAYDAY  
THIS IS  
Aurora Australis VNAA Aurora Australis VNAA Aurora Australis VNAA  
503043000
MAYDAY
Aurora Australis VNAA
--Example position--
--Example Distress--
--X people on board--
--EPIRB Activated--
```

### Distress Acknowledgement

```
MAYDAY  
[Vessel in distress] [Vessel in distress] [Vessel in distress]
THIS IS  
[Vessel] [Callsign] [Vessel] [Callsign] [Vessel] [Callsign]  
RECEIVED MAYDAY
```
