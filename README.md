# Operators Open Field Manual: Colocation Deployments

![License](https://img.shields.io/badge/license-Unlicense-blue.svg?style=plastic)

**WARNING** This resource is under active development and **will** contain errors or inaccuracies. Use at your own risk. This warning will be removed once the resource is considered stable.

This resource aims to be a high level resource for Operators in the operations of a Colocation Deployment.

It is primarily intended as a means of packaging and sharing information by the owner, but is free to be shared, cloned, or used as needed.

It is written with the audience of a "digital native" Operator in mind, that is an Operator who is already capable of Operating in a DevOps / SRE / PlatOps context.

This resource will differentiate between "Colocation", "Systems", "Network" and other roles, though those roles could all be attributed to the same Operator or Operations Team.

## Table of contents

- Introduction
  - The Three Primitives of Colocation
- Space
- Power
- Connectivity
- Sales
- Support and Compliance
- Lifecycle

## Introduction

Colocation, used here to mean " multi-tenant Data Center Colocation" is a unique operational context. By premise, it sits at the boundary between physical and digital systems. For Operators this means Colocation Operations can require proficiencies in both physical and digital infrastructure contexts, an increasingly unique overlap.

As a deployment model, Colocation and its ecosystems are behind their digital equivalents in the world of open and public documentation and information access. Much, if not most information will be gated behind sign-ins and "email us" buttons, or stored as internal only documentation or in the brains of seniors, having the effect of steepening the learning curve.

Put it simply, there is no [PEP-8](https://peps.python.org/pep-0008/) for Colocation.

This resource aims to reduce that learning curve by treating Colocation as  if it were as simple as ***aaS**, which it broadly is, and documenting it in that style.

### The Three Primitives of Colocation

1. Space for IT equipment
	- Traditionally sold in volumes of [cabinets](https://en.wikipedia.org/wiki/19-inch_cabinet) or [Square Feet](https://en.wikipedia.org/wiki/Square_foot)
2. Power for IT equipment
	- Generally assumes the cooling required for the power delivered, traditionally sold in volumes of [Kilowatt Hour](https://en.wikipedia.org/wiki/Kilowatt-hour)
3. Connectivity for IT equipment
	- Traditionally sold in volumes of [Cross Connects](https://phoenixnap.com/kb/cross-connect)

#### The Ghost Primitive of Colocation

By premise of the product itself, multi-tenant Data Center Colocation is a human to human engagement model between provider and customer, making "Human Engagement" a difficult to define but important "Ghost Primitive" of Colocation Operations.

### The Colocation "Shared Responsibility Mode"

Much like the [" AWS Shared Responsibility Model"](https://aws.amazon.com/compliance/shared-responsibility-model/), Colo

While generally less well documented than the famous AWS Shared Responsibility Model, Colocation facilities also operate under a Shared Responsibility model between vendor and customer. Like Cloud services, the areas of boundary overlap in Colocation services are an important area of focus.

## Space

Space is literally the space for the physical IT equipment. Commonly referred to as "IT Rooms", "IT Halls", "Computer Rooms", this resource considers the names "Customer White Space", "White Space", or just "Space" for short as best in the context of Colocation.

- Scaling
- Availability
- Operating
	- Compliance
- Security
- Monitoring
- Staffing
- Commercials

### Scaling
### Availability
### Operating
### Security

In a Colocation context, there is a golden rule that can be an easy touchstone to avoid in getting lost in [Security Theater](https://en.wikipedia.org/wiki/Security_theater):

- In the event of an emergency, such as an event with electrical safety concerns, facility staff must be able to access any and all Spaces inside the facility, including "Customer Spaces" such as Cages and Cabinets.  Put another way: Facility staff must be able to get into your cabinet to pull the power out of your IT equipement if it is spewing smoke into the facility.

The common reference for Data Center and Colocation controls is [NIST 800-53](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final), which also covers subjects beyond just the "Space".

#### Systems / IT Equipment

This resource starts with the "Security of IT Equipment" because IT equipment is likely to be one of the more tangible, defineable boundaries in consideration.

While the security of IT equipment likely falls more on the "Systems Operations" role, the layering good security requires Systems and Colocation roles to operate in awareness of each other.

This resource is also not meant to be an exhaustive list of IT equipment security concerns, merely just a shortlist of ones relevant to operating in a Colocation environment.

##### "Plug / Unplug" events

If something has physical access to IT equipment, they have access to logically "plug" or "unplug" into a device.

Most data center grade devices can define controls and monitors around "Plug / unplug" events, and generally yield a high return on investment in coverage and risk reduction. Some controls, such a Port-Security can also overlap with best practices architectural design.

Other roles' security controls are relevant as well, devices can be configured to avoid automatically mounting USB devices. Strong password encryption, disk encryption and good update hygiene can help prevent unauthorized local logins, including for people authorized for Physical Access, but not Systems access.

##### Uptime / Reboot

If something has access to IT equipment, they can put the device through physical state changes like reboot and shutdown.

IT equipment is uniquely vulnerable during "boot" events, often exposing critical paths like BIOS and Firmware controls.

Monitors should be put in place to understand both the cause and timeline of Power and Uptime events.

##### Chassis Intrusion / Hardware Modification

The ability of a device to inventory and track internal hardware changes isn't a ubiquitous feature, either in availability or implementation. A modern compute server from Dell, HP or SMC with a featureful BMC (iDRAC / iLO / IPMI) should be capable of inventorying and tracking a diverse set of hardware state changes. A core switch from a major networking vendor is quite capable of reporting a chassis line card change or USB insertion. The further "down market"  the source of IT equipment, the less likely or well covered these features will be.

Monitoring for chassis intrusion or hardware change alarm is a high return on investment monitor, with value not just for security but for Operations as well.

**Disk Changes**: Disks are often children of an HBA or controller, where that HBA or controller may not be able to communicate with a devices' BMC. Put another way, disk changes may be invisible / transparent to a BMC.

##### Firmware change / Unable to validate firmware

If something has access to IT equipment, they have access to modify that equipment’s Firmware.

Firmware correctness is a challenging problem but one that has coverage over a number of security concerns, for example sourcing and supply chain security.

The ability to verify firmware correctness and authenticity is not a table stakes feature in IT equipment, even in the category of "Data Center Grade".


##### Data Encryption, Deletion and Media Destruction

Broadly a "Systems Operation" responsibility with significant responsibility overlap, data lifecycling can have significant scope overlap with Colocation Operations.

Consider what happens to your organization if a remote hands tech accidentally pulls and RMAs the wrong drive? Even with no ill-intent, events like this can pose significant risk if not protected against and prepared for.

In 2025, business and customer data should be encrypted at rest, full stop.

It is the opinion of this reference that media destruction as a default policy should be avoided as a requirement if possible. It may be the right choice for some organizations, but for many, resale and recycling of drives can be an enabling Operational pattern. This only reinforces the correctness of strong data encryption and sanitization practices.

[Secure Erase](https://en.wikipedia.org/wiki/Parallel_ATA#HDD_passwords_and_security) has become a widely adopted feature (NVMe, and  modern SAS / SATA support, SCSI does not) and is considered secure enough to be documented NIST in it's own section of NIST 800-88, and supported in [community tooling](https://wiki.archlinux.org/title/Solid_state_drive/Memory_cell_clearing). Secure Erase is particularly useful during OS re-provisioning, where it can provide a disk wipe like function quickly and without wear on the devices.

NIST is the common reference for data deletion / wiping policies, broadly incorporating legacy references / specifications like "DoD 3-pass" etc.

- [NIST 800-111](https://csrc.nist.gov/pubs/sp/800/111/final): Disk Encryption for End User Devices
- [NIST 800-88](https://csrc.nist.gov/pubs/sp/800/88/r1/final): Media Sanitization


Put another way, a security posture that starts with encrypting all drives with [LUKs] and deletes all drives with [nwipe] is in a good position to meet common expectations of data security inside a colocation environment.

Managing the storage of network devices, appliances and accessories like SmartPDUs should be accounted for as well.


#### Cabinet Security

Cabinet security will primarily be focused on the cabinet door lock and controls on opening the cabinet doors to provide access to the IT equipment inside.

It is highly likely that the facility staff will need a path to quickly and safely opening any customer cabinet during an emergency.

Lock and key are the primary Cabinet access control, given they work quickly and when power is lost. Generally a facility will require that its staff has a copy of a key to open any cabinet in any customer white space, including cages.

The tumblers inside most cabinet locks can be configured to support multiple keys, meaning more than one physical key can open the same lock. Facilities may allow customers to carry keys for their own cabinets in their own cages, some may not. Most facilities will not allow customers to carry a key for cabinets in "Shared Customer Spaces", preferring to be the sole custodian of those shared space cabinet keys.

Re-keying a cabinet is generally something that can be done as a one time charge service, though it can be manually intensive and as such an expensive charge.

Some facilities may install Badge or Biometric readers on cabinet locks as well, though often this is limited to Cabinets sold as part of cages (below), and not "Shared Spaces" (also below).

Even when a cabinet is secured with a Badge Reader or Biometric Control, there must still generally be a physical lock and key to open the cabinet even during an emergency event, say during loss of power, and the facilities staff will be the custodian of that key.

Documenting Shared cabinets is a todo of this resource.

#### Shared Customer Space Security

Many facilities offer Space in "Shared Customer Spaces", this generally implies a large open space with no cages / fencing walls, where long contiguous rows of cabinets are pre-positioned on the floor of the whitespace, and are assigned sequentially to customers by order, meaning two customers can Cabinets can be immediately adjacent.

There is nothing insecure with deploying in these Spaces by premise, access is still generally well controlled through the same primitives as customer cages.

The Security limitation of Shared Spaces is in their turn-key nature, and thus with little flexibility for customization. Facilities may allow something like a combination lock to be added to the Cabinet to allow shared access, but most facilities will want to keep each Cabinet a 1x key / lock combination where their staff hold the key for each Cabinet in the Shared Space.

This generally implies that facility staff will need to open the Cabinets when Colocation Operations or other designated persons arrive, and close it when they leave. This generally requires facility staff to be present to allow Operators in and out of the site.

Customers are generally not allowed to be "above" the Cabinets in shared spaces, and most facilities have strong rules around customers not running any cabling overhead between cabinets. Some facilities may allow customers to pass cables between contiguous cabinets.

##### Cage Security

A "Cage" is a space dedicated for a single customer within a "White Space", that is separated likely by a chain link fence, which designates and separates the space for that customer's sole usage.

A cage will likely have one or more sliding gates, where like Cabinets, most facilities will require a physical key / lock that allows the cage to be opened by facility staff, including in the event of a power outage.

Most facilities will allow adding a Badge or Biometric Reader to cage doors as well. Badge and Biometric readers are generally a little better supported by facilities at the Cage level than Cabinet level.

While the spaces within Cages are often covered by facility cameras, customers can have Cameras installed in their own cage, and connectivity run to a designated cabinet in the cage. Most multi-tenant facilities will have policies on Camera placement inside customer cages, primarily around not allowing customer operated cameras to have visibility into shared or other customers spaces. Cameras with pan / tilt / zoom will generally not be allowed, and most facilities will require Camera installation as a one-time service performed by facilities staff, and will frown upon customer placed cameras inside Cages.

There are examples of Cage security taken to extremes, "blackout curtains or panels" added to the fence to prevent outside in viewing of the cage, or "floor to ceiling" cage walls to prevent someone from climbing over a cage wall (which often only extend to ~10ft up and not all the way to ceiling). These may be required for certain exceptional cases, but these exercises can fall into the realm of [Security Theater](https://en.wikipedia.org/wiki/Security_theater).

##### Facility Security

Facilities Security is a subject so broad this resource will deliberately simplify its scope in the hope of being consumable. It will also broadly lump "facility" and "campus" subjects together as an egregious simplification.

Most multi-tenant Data Center Colocation facilities will share some common Security primitives:

- Cameras: Ideally with the entire external view of the site covered, and complete coverage of customer and critical spaces inside the facility.
	- May be less coverage in older or "edge" locations
- Fenced or Controlled perimeter around the facility:
	- Access controlled gates or access to transition between "public" space to "private" space.
	- Commonly controlled by facility staff, potentially with badge or biometric reader
	- Less common in smaller, older or more urban facilities.
- Controlled Front Entrance
	- Controlled by badge or biometric reader
- Security / Front Desk
	- Most large multi-tenant facilities will staff a facilities person 24x7.
	- Some facilities make distinctions between "security" and "facility" staff
		- The two roles can have different on-site staffing schedules and different responsibilities
		- Often "security" is outsourced to a third party vendor
			- This is broadly to meet the requirements of certain customers who require it for conflict of interest boundaries
- Man Trap
	- Generally requires Badge or Biometric Readers at both entrance and exit
	- Generally limited to one person, or at least one customer group moving through at a time
	- Generally must have exit crash bars or be automatically unlocked for egress in the event of an emergency
- Controlled Customer Space Access
	- Most large sites will be broken up by hall, each hall having its own controlled access and providing its own "Customer White Space".
	- Inside the hall may be "Shared Space", "Cage Space", or both, or a single customer.
- Meet Me Room
	- While the MMR concept has become more ambiguous in modern facilities, most facilities have named places where they concentrate connectivity both intra-site and extra-site
	- Security and frequency of access of these MMRs should be considered part of the availability story of the facility.
- Critical Infrastructure Rooms
	- Most facilities will have rooms outside of the Customer White Spaces where critical infrastructure like cooling and electrical can be separated from customer white space
		- This separation can be of consequence. Some facilities have large cooling infrastructure like Air Handlers / Exchanges or PDUs inside the "Customer White Space", meaning additional outside maintenance and operations staffing that will need access to the Customer White Space.

##### Badge and Biometric Readers

Badge and Biometric readers are common primitives for controlling access and movement through doors and gates.

Badge Readers are simple [proximity card](https://en.wikipedia.org/wiki/Proximity_card) detection devices, requiring the authorized physical credential of a badge or card being present to move through a control.

Biometric Readers, generally a fingerprint or handprint reader, similarly control access through a door or gate, but attempt to validate the person moving through the control instead of their credential.

These readers are usually tied together at a facility level by software operated by the facility. Modifications such as enabling or disabling access are made by facility or vendor staff, usually as part of request by a customer via ticket, though some vendors may have this integrated with their customer facing software / portal.

The logs for these readers should generally be archived safely offsite for some known amount of time.

Customers will generally not have access to these software systems themselves, but can generally request audits / logs of access from the facility.

When a Badge or Biometric reader is installed into a Customers Space, such as a Cage, it is generally assumed that those readers will be operated by the customer, necessitating that that customer operate the relevant software.

It should be noted Badge and Biometric reader software is not generally well supported by open source community, and much of this ecosystem operates in a traditional closed source model.

Some facilities place Readers and their infrastructure on redundant power, some do not.

[NIST 800-116](https://csrc.nist.gov/pubs/sp/800/116/r1/final) covers PIV Credentials in Facility Access

##### Cameras + Motion Sensors

Cameras are excellent as "second factors" for other controls and monitors.

These cameras are usually tied together at a facility level by software operated by the facility.

The video archives for these facility cameras should generally be archived safely offsite for some known amount of time.

Customers will generally not have access to these facility video streams or software systems themselves, but can generally request audits / archives of camera footage from a facility.

When a Camera is installed into a Customers Space, such as a Cage, it is generally assumed that those Cameras will be operated by the customer, necessitating that that customer operate the relevant software.

Historically these video systems were mostly proprietary and cumbersome, however some projects / examples like [Frigate](https://github.com/blakeblackshear/frigate), [Motion](https://motion-project.github.io/) and [ZoneMinder](https://github.com/ZoneMinder/ZoneMinder/) are evidence of community catch-up.

Again, facilities are likely to have policies and requirements on Cameras installed into customer spaces.

Motion Sensors are a less common and less regulated devices, some facilities may even let customers place their own motion detectors so long as they only register in space dedicated to the customer.

Some facilities place Cameras and their infrastructure on redundant power, some do not.

NIST documents for [Digital Video Exchange](https://www.nist.gov/programs-projects/digital-video-exchange-standards) and [Protecting Controlled Unclassified (800-171)](https://csrc.nist.gov/pubs/sp/800/171/r3/final).


## Power

- Introduction to Power
- Scaling
- Availability
- Operating
- Security
- Monitoring

## Connectivity

- Introduction to Connectivity
- Primitives and Widgets
- Scaling
- Availability
- Operating
- Security
- Monitoring

## Sales

## Security

## Support

## Lifecycling

- Introduction to Lifecycling
- Operating
- Scaling
- Availability
- Security
- Monitoring
- Commercials
- Compliance

### Introduction to Lifecycling

Everything that goes in must come out.

Most digitally defined products have the equivalent of a delete button. There is no such equivalent in a Colocation context, instead there is only thousands of pounds of IT equipment.

### Operating

Lifecycle operations...

#### Asseting

Asseting is the linkage of physical assets to logical, likely digital inventories.

##### Inventory / Tracking

Decisions around what to inventory and tracking processes and tools to use are significant, and will dictate much of the rest of Lifecycling context.

- **Tool Interop** Priority should be given to tools that interoperate well with other tools, or at least common data formats.

- **Why track Asset changes?** Why Asset tracking is important may be most easily conveyed by a ghost story:
- Many an Operator has RMA'ed / returned a failed drive to a vendor, only to have the vendor replace it with a known failed drive, and only found it because they tracked drive serials correctly enough to identify they were seeing drives they had seen before.

- **What to Asset?**: A good truism for things that need asseting: If you will need to RMA it individually, or if Finance will want to [depreciate](https://blog.invgate.com/depreciation-of-it-assets) it individually, it should be asseted.

- **What unique key to Asset against?** A unique ID should be given to every asset, independent of the asset’s markings / designation from its vendor. There is value in having the key be "human readable".

##### Labelling / Tagging

- **Barcode / QR / RFID**: It is possible to physically tag / label physical IT equipment with Barcode / QR Code or RFID. While a high standard of operation, managing hardware in this way can enable Operational efficiencies and scaling patterns that would be difficult or impossible if each interaction with equipment required a manual lookup.

- **No stateful information on labels**: While tempting, it is a poor practice to apply state to labels. If during an outage, a cable with an out of date label like "SW-01-E24/app14-p4" gets grabbed and re-used and the old label gets missed, it can sit as a poison pill for the next human to touch it.

- **Safely label SFPs**: Its easy to incorrectly label SFPs. One does not want to obstruct the vendor's label, cause confusion with a cable label, or apply a label to a part of the SFP that might interfere with operation. Some may feel comfortable with applying a label to the SFP "pull tab" if it has one, which has the benefit of exposing the label to view / scanning while the SFP is in operation in a dense environment.

- **Make tags visible and repeatable**: The more visible and accessible a tag is, the more useful it is. Always place tags in places that are expected / repeated, but it is ok to tag an asset repeatedly to increase utility.


### Scaling
### Security
