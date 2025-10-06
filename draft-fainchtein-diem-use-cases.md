---
title: "Digital Emblems - Use Cases and Requirements"
abbrev: "DIEM Use Cases and Requirements"
category: info

docname: draft-fainchtein-diem-use-cases-latest
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
area: "Applications and Real-Time"
workgroup: "Digital Emblems"
keyword:
venue:
  group: "Digital Emblems"
  type: "Working Group"
  mail: "diem@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/diem"
  github: "rahelFain/combined-diem-uses-reqs"
  latest: "https://rahelFain.github.io/combined-diem-uses-reqs/draft-fainchtein-diem-use-cases.html"

author:
  -
    fullname: Casey Deccio
    organization: Brigham Young University
    email: casey@byu.edu

  -
    fullname: Rahel A. Fainchtein
    organization: JHU/APL
    email: rahel.fainchtein@jhuapl.edu

  -
    fullname: Felix Linker
    email: linkerfelix@gmail.com

  -
    fullname: Jim Reid
    organization: RTFM llp
    email: jim@rfc1035.com

  -
    fullname: Alex Rosenberg
    organization: Veridigo
    email: alexr@veridigo.com

  -
    fullname: Allison Mankin
    organization: Packet Clearing House
    email: allison@pch.net

normative:
  CHARTER:
    target: https://datatracker.ietf.org/doc/charter-ietf-diem/01/
    title: Digital Emblems
    date: 2025-05-27

informative:
  BLUEHELMET:
    target: https://guide-humanitarian-law.org/content/article/3/peacekeeping/
    title: The Practical Guide to Humanitarian Law
    author:
       org: Doctors Without Borders
  BLUESHIELD:
    target: https://www.unesco.org/en/heritage-armed-conflicts/enhanced-protection-cultural-property-highest-importance-humanity
    title: Enhanced Protection - Cultural Property of Highest Importance to Humanity
    author:
       org: United Nations Educational, Scientific and Cultural Organization
  REDCROSS:
    target: https://www.icrc.org/en/doc/assets/files/other/protection_emblems.pdf
    title: The Protection of the Red Cross / Red Crescent Emblems
    author:
       org: International Committee of the Red Cross
  PRESS:
    target: https://safety.rsf.org/appendix-i-protection-of-journalists-in-war-zones/
    title: RSF Resource for Journalists' Safety
    author:
       org: Reporters Without Borders
  DIPLOMAT:
    target: https://www.law.cornell.edu/cfr/text/19/148.83
    title: Personnel of Foreign Governments and International Organizations and Special Treatment for Returning Individuals
    author:
       org: Cornell Law School - Legal Information Institute
  RAMSAR:
    target: https://www.ramsar.org
    title: The Convention on Wetlands
    author:
       org: Convention on Wetlands Secretariat
  ISPM15:
    target: https://www.ippc.int/static/media/files/publication/en/2019/02/ISPM_15_2018_En_WoodPackaging_Post-CPM13_Rev_Annex1and2_Fixed_2019-02-01.pdf
    title: "International Standards for Phytosanitary Measures No. 15: Regulation of Wood Packaging Material in International Trade"
    author:
       org: International Plant Protection Convention, Food and Agriculture Organization of the United Nations
  UNMODELREGS:
    target: https://unece.org/transport/dangerous-goods/un-model-regulations-rev-23
    title: "UN Model Regulations on the Transport of Dangerous Goods"
    author:
       org: United Nations Economic and Social Council
  HARMONIZED:
    target: https://www.wcotradetools.org/en/harmonized-system
    title: "Harmonized System"
    author:
       org: World Customs Organization


--- abstract

TODO Abstract


--- middle

# Introduction

Digital emblems are a means for an asset to signal to validating entities that it should be protected or treated in a specific way, using some normative framework.
The DIEM WG will define a set of standards for an architecture that enables discovery and validation of digital emblems.
This document lists the requirements that the architecture must accommodate.
These requirements were identified across different use cases.
Not all use cases share all requirements.
We envision an architecture system comprising multiple standards, which can be flexibly profiled for different use cases.
We use the terms "(digital) emblem," "bearer," and "validation" in accordance with the DIEM charter as of this writing {{CHARTER}}.
These definitions have been reproduced in section Conventions and Definitions.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

The definitions for terms "(digital) emblem," "bearer," and "validation" are reproduced from the charter {{CHARTER}} as of this writing.


(Digital) Emblem:
: Emblems such as the Red Cross, Red Crescent, Red Crystal, and Blue Shield can be symbols of protection governed by International Humanitarian Law (IHL).
  Emblems can also be identified by other laws, agreements, or standards.
  There is a need to present emblems through digital communication channels.
  Emblems presented in such ways are called digital emblems.
  Digital emblems extend the range of identifying marks from the physical (visual and tactile) to the digital realm.

Bearer:
: "To bear an emblem" means to present and be identified by a digital emblem.
  The entity that bears the emblem is the bearer or emblem holder.
  This is often a separate entity from the creator or original designer of the emblem.

Validation:
: "To validate an emblem" means to confirm the authenticity or legitimacy of a particular symbol or design,
often by checking its details against a known standard or reference point.
  Validation may include ensuring that the bearer has not forged, stolen, or tampered with an emblem.
  Emblems may be observed by validators without the knowledge of the bearer presenting the emblem, or may be presented to a specific validator upon request.
  Cryptographic verification may or may not be used based on the in-place security mechanisms of the communication channel bearing the emblem.
  Which attributes an emblem contains, and how a digital emblem is secured and presented impacts how a validator interprets and trusts the assertions made within the emblem.

# Requirements

The DIEM architecture will allow validators to discover and validate digital emblems that are associated with bearers. This section contains the requirements that this architecture will address. They are based on use cases identified thus far (see Section Use Cases), but note that not all use cases share all requirements. We categorize these requirements into: requirements on digital emblems and their format, on their discovery, on their validation, and other requirements.

## Digital Emblem Requirements

### Digital Emblem Format
Digital emblems MUST identify their bearer and their kind of digital emblem. Beyond that, digital emblems MAY include other data, for example, an issuer or a validity window. As of writing, the DIEM charter requires that digital emblems MUST explicitly identify their bearer by a Fully Qualified Domain Name (FQDN).

### Emblem Semantics
Individual use cases MUST specify the semantics of the emblem and the bearer. It must be clearly stated how discovery and validation of a digital emblem should inform validator behavior.

## Discovery Requirements

### Discovery

Digital emblems MUST specify how validators can check for the presence of a digital emblem. That is, given a potential bearer a validator must be able to determine whether it has an associated emblem. For example, verifying whether a FQDN has an emblem associated with it could be realized by fetching digital emblem-associated records for said FQDN.

### Removable

Digital emblems MAY require to be removable in that checking for the presence of an emblem associated with a bearer results in no emblem.
Note that checking for emblem presence is independent of its validation.
That is, emblems do not count as removed when they become invalid.

### Undetectable Validation

Digital emblem discovery MAY require that bearers, issuers, and authorizing parties be unable to detect when an emblem is being discovered or validated.
This requirement is motivated by emblems that mark its bearer as protected and ask validators to not attack the bearer.
If emblem discovery were detectable by the bearer, issuer, or by an authorizing party, malicious parties could misuse the digital emblem as an intrusion detection system.

## Validation Requirements

### Validation

Digital emblems MAY require validation. Validation MUST support verification of all the emblem’s data and its context.
In particular, validation MUST ensure that the emblem was issued for the respective bearer.
Some use cases MAY use unverified digital emblems.

### Authorization

Digital emblems MAY require authorization by third-parties.
Any authorization mechanism MUST account for the possibility of compromise of cryptographic key material, for example, by specifying revocation mechanisms or using short-lived credentials.
Individual profiles MUST standardize a trust model that describes how validators can discover authorities and how the system selects authorities.

## Other Requirements

### Extensibility

The digital emblem architecture should be extensible.
The initial work should not preclude future extensions and individual standards should be designed as general as possible.

# Extensions

In this section, we sketch how the digital emblem architecture could be extended by future standards to accommodate more use cases, but it is not a comprehensive list.

## Data Formats
Emblems for additional use cases may be defined via new profiles in future standards, potentially including new types of atomic data elements requiring additional specification.

## Bearer Discovery

It may be non-obvious for some use cases to identify the bearer that is associated with an asset, and thus impossible to fetch emblems associated with that asset.
To accommodate for such use cases, one could specify means to discover bearers for different types of assets.

## Implicit Discovery

An alternative approach to the above problem would be to bind emblems implicitly to their bearer.
Implicit binding would identify the bearer by the emblem's location.
For example, if emblems were distributed via NFC, the bearer could be the asset to which the NFC chip was attached.
As of this writing, the current charter scope requires that digital emblems explicitly identify their bearer, but such discovery mechanisms could be investigated in future WG work.

## Confidentiality
Some use cases may contain confidential or sensitive data, and may require mechanisms to protect such data.
For example, this could be realized with encryption of the general emblem data format that will be part of the architecture or by only serving emblems over channels with access control mechanisms.

## Proof of Presence

For some emblems, it may be relevant to track that an emblem has been presented. This could be achieved, for example, by standardizing different distributions mechanisms, e.g., using decentralized authenticated data structures.

# Use Cases

Different use cases have different requirements.
The purpose of this document is to list the requirements that will be addressed with the initial architecture.
The use cases overlap and would benefit from a DIEM architecture developed to provide the requirements listed above, though some may require additional extensions.
We alphabetically list use cases here so that relevant stakeholders can provide input whether their use case would indeed benefit from a DIEM architecture, and invite participants to provide use cases or details that we have missed.

We provide auxiliary material under Informative References.

## Basel Convention

Regulates the trans-boundary movement of hazardous wastes. Use cases are functionally identical to OPCW and IAEA.

## Ramsar Convention on the Wetlands

The Convention on Wetlands of International Importance especially as Waterfowl Habitat "providees the single most global framework for intergovernmental cooperation on wetland issues" and it features a list of geographic areas designated by Member States.
A digital emblem for the geographic areas potentially requires

* Indication of location
* Access to presence or absence of Ramsar designation of a specified location
* Textual description
* Ability to validate the presence or absence of Ramsar designation

## International Atomic Energy Agency (IAEA)

IAEA administers several treaties, especially related to the controlled shipment of atomic fuels and wastes across borders.
Similar use case as OPCW.

## International Humanitarian Law

The Geneva Conventions and their Additional Protocols constitute the core of International Humanitarian Law (IHL).
Some assets enjoy certain specific protections under IHL, including that they must not be attacked, and IHL codifies four types of protective emblems for armed conflict, which inform other parties that marked assets benefit from one or several of these specific protections:

- The emblems of the Red Cross, Red Crescent, and Red Crystal
- The Blue Shield emblem
- The emblem for the protection of civil defense marks
- The dangerous forces emblem

Digital emblems under IHL could be extended to digital, network-connected and network-addressable assets that enjoy aforementioned specific protections under IHL.

## Organization for the Prohibition of Chemical Weapons (OPCW)

Requires protection of Schedule 1 chemicals in transit between signatory countries for research, medical, pharmaceutical, or protective purposes.
Emblem would identify place, date, and volume of production, and the emblem can contain confidential data.

## Press

Journalists in conflict zones use protective markings that indicate their status as a non-combatant.
Digital assets belonging to the press could be digitally marked, and protective markings in conflict zones could be digitized.

## United Nations Economic and Social Council (ECOSOC)

UN Model Regulations {{UNMODELREGS}} includes "Recommendations on the Transport of Dangerous Goods."
This includes labeling of items with a four digit "UN Number" that indicates the comounds contained within, such as chemicals, explosives, flammable liquids, etc.
For example, items containing lithium-based batteries are labeled with 3480 or 3481 and accompanied by a specific "battery mark" emblem.

## United Nations Peacekeepers

UN Peacekeepers use protective markings in theater as well as facilities associated with the mission.

## World Customs Organization (WCO)

Specifies "Harmonized Systems" codes {{HARMONIZED}} that classify items such as livestock, arms and ammunition, chemicals, plastics, machinery, foodstuffs, etc.
They also provide a system for labeling origin of items and valuation of items, all enforced by numerous international trade agreements between individual nations and groups of nations.

## World Health Organization (WHO)

Similar to the use case of the Red Cross, Red Crystal, and Red Crescent.

## United Nations Food and Agriculture Organization (FAO)

Among other things is responsible for the International Plant Protection Convention (IPPC) and International Standards for Phytosanitary Measures standards including ISPM 15 that requires wood packaging materials (pallets, crates, dunnages) to be debarked, heat-treated or fumigated with methyl-bromide, and stamped or branded with a compliance mark known as a "wheat stamp."

## World Intellectual Property Organization (WIPO)

WIPO administers 26+ treaties with different protections for different things.
Brands that are protected under international law (e.g., Madrid Protocol) can mark their shipments with an emblem allowing customs agents to positively identify legitimate products.

## International Civil Aviation Organization (ICAO)

Requires protection of civil aviation flights and the ability to assert that they are not dual-use (i.e., not carrying military cargo).
Digital emblem would carry a geographic description of the flight plan, its current location, and an indicator of its identity (i.e., tail number).
Potential need for the emblem to reference a limited or partially redacted flight manifest.

# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.

--- back

# Acknowledgments
{:numbered="false"}
