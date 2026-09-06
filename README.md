# Wireless ISP Infrastructure and Field Operations

![Sierra Leone](https://img.shields.io/badge/Sierra_Leone-3B9EFF?style=flat-square)
![Sites](https://img.shields.io/badge/30%2B_base_stations-3B9EFF?style=flat-square)
![MikroTik](https://img.shields.io/badge/MikroTik-3B9EFF?style=flat-square&logo=mikrotik&logoColor=white)
![Ubiquiti](https://img.shields.io/badge/Ubiquiti-3B9EFF?style=flat-square&logo=ubiquiti&logoColor=white)
![Cisco](https://img.shields.io/badge/Cisco-3B9EFF?style=flat-square&logo=cisco&logoColor=white)
![PRTG](https://img.shields.io/badge/PRTG-3B9EFF?style=flat-square)
![Zabbix](https://img.shields.io/badge/Zabbix-3B9EFF?style=flat-square&logo=zabbix&logoColor=white)

**AI Networks and Alemobet, Sierra Leone. 2016 to 2021.**

Two businesses under the same ownership. AI Networks was a wireless internet service provider
covering the country from more than thirty base station sites. Alemobet was the systems and field
side: business IT support, servers, structured cabling and whole building network installs.

I spent five years across both. IT Technician at Alemobet from 2016, then Lead Technical at
AI Networks from 2017 to 2021, within a technical team of twelve reporting to the technical manager
and ultimately the CTO and CEO.

This is where I learned to design for the situation I was in rather than the one in the manual.

---

## At a glance

| | |
|---|---|
| **Coverage** | Nationwide |
| **Base stations** | More than 30, co-located with telecom partners |
| **Core** | Network operations centre in Freetown |
| **Longest link** | 70 km point to point |
| **Backhaul** | Infinet, including the XG series |
| **Access** | Ubiquiti point to multipoint |
| **Subscriber management** | Splynx with RADIUS, PPPoE |
| **Monitoring** | PRTG, later migrated to Zabbix |
| **Team** | 12 technical staff at AI Networks, 6 at Alemobet |

---

## Network architecture

Fibre from the upstream point of presence into the **network operations centre in Freetown**.
Everything was centralised there: routing, subscriber management, billing and monitoring. From the
NOC the network fanned out over point to point microwave to base stations across the country.

A base station carried one or more backhaul radios and the access points facing subscribers. Sites
with good elevation and clear line of sight carried **several backhauls at once, pointing in
different directions**, because the regions they served were not on the same bearing. The topology
followed the terrain rather than a map.

```
Upstream fibre
  -> Network operations centre, Freetown
  -> Point to point backhaul, Infinet
  -> Base station
  -> Point to multipoint access, Ubiquiti
  -> Subscriber unit, roof mounted
```

Paths were planned with a **link plotting tool** before anything was mounted. In a mountainous
country that step is not optional: line of sight is an engineering problem rather than an
assumption, and alignment on a completed link is unforgiving.

### Equipment

| Function | Kit |
|---|---|
| Core routing | MikroTik CCR |
| Backhaul | Infinet, including XG, for the long and difficult paths |
| Access | Ubiquiti Rocket access points |
| Subscriber units | Ubiquiti M5, M3 and AC Pro |
| Also in the estate | Mimosa, LigoWave, MikroTik, Cisco, TP-Link |

### Addressing and subscriber separation

Subscribers authenticated over **PPPoE with private addressing**, which kept every customer session
isolated and made provisioning a central operation rather than a site visit. Routing was a mix of
static and dynamic depending on the segment.

**Splynx with RADIUS** handled subscriber management, provisioning and billing, so a customer could
be activated, suspended or restored from the NOC.

### Site power

Base stations ran on a mix of grid, inverter and battery, and generator supplied by the
co-location partner. Which combination a site got was a decision, not a default: it depended on the
size of the customer base it served, its location, and how much growth we expected there.

### Customer installations

Roof mounted subscriber units, installed by a **two technician team**. A straightforward
residential install took around two hours; a larger commercial site could take a full day.

---

## Monitoring

**PRTG** watched latency, throughput, link speed and device power across the estate from the NOC.
Latency and power were the two that mattered most. Rising latency preceded link failure, and power
told you whether a site was about to go dark before anyone had noticed the outage.

Later we **migrated to Zabbix**. PRTG's licensing cost and its inflexibility as the estate grew made
it the wrong tool at that scale, and Zabbix was the strongest of the alternatives we assessed. That
migration is the direct reason Zabbix is the monitoring platform in every environment I have built
since.

---

## Design decisions

**Infinet for backhaul.** The terrain demanded it. We ran point to point links of up to **70 km**,
and in testing no other platform available to us produced comparable throughput at that distance.
Vendor choice here was driven by geography rather than preference.

**Ubiquiti facing subscribers.** It was the most accessible platform at the time, and it handled
interference well. That mattered enormously in dense urban areas where the same frequencies were
crowded with equipment from every other operator and installer in the city.

**PPPoE and Splynx, replacing static assignment.** We started with static addressing. As the
subscriber base grew, the manual step in every provisioning and disconnection became the failure
point: **human error, at scale**. Moving to PPPoE with Splynx removed that step, and had the side
benefit of making installations noticeably faster.

**Co-location rather than building our own sites.** Building a tower is a regulatory process and a
capital cost. Co-locating on existing telecom infrastructure was faster and cheaper, at the price of
depending on a partner for access and power. For a network that needed nationwide coverage quickly,
that was the right trade.

**Multiple backhauls on high sites.** Where a site had the elevation and the sight lines, we hung
several backhauls on it rather than building more sites. One good location can serve regions that
sit on completely different bearings.

**Everything centralised at the NOC.** Routing, subscriber management, billing and monitoring in one
place. With sites that were hard to reach and a small technical team, the cost of distributing any
of it would have been paid every time something needed changing.

---

## Incident: the lightning strike

Heavy rain and lightning are a feature of the season rather than an exception. One site took a
direct strike and **every device on it was destroyed**, along with the cabling.

Recovery took **three days**. We split the team: some lifting and mounting replacement hardware,
others restoring configurations from backup. We held spare backhaul radios and access points, and we
had current configuration backups, which is the only reason it was three days rather than three
weeks. Cables had to be re-run and the site brought back up before customers had service again.

**What changed afterwards.** We established that **large clients get a second line of sight**, so
that no single site failure removes their service. At least two paths, at any given time.

The pattern is the same one I later applied to the broadcast network: when a failure is outside your
control, the fix is architectural rather than procedural. You cannot stop lightning. You can stop it
being a single point of failure.

---

## The Alemobet side

Business and residential IT support alongside the ISP operation.

- **Windows and Office deployment** across corporate and individual clients
- **Server installation and maintenance**, HP and Dell
- **Active Directory** administration at client sites
- **Whole building network installs**: design, structured cabling, cable management, patch panels
- **Repairs and ongoing support**

This is the work that taught me the unglamorous half of infrastructure. A network that is beautifully
designed and badly cabled is a network that will be hard to fix at two in the morning.

---

## Constraints

Three things shaped every decision, and they are the reason my judgement is different from an
engineer who has only worked where infrastructure is assumed.

**Power.** It could not be relied on, anywhere, at any site.

**Terrain.** A mountainous country makes line of sight a planning problem. Links that would be
trivial elsewhere required a plotting tool, a survey and often a compromise on siting.

**Equipment availability.** We recommended and specified from **what could actually be obtained**,
not what was best on paper. The better option might be months away, or simply unaffordable. Learning
to design a working system from available parts, and to know when the compromise is acceptable and
when it is not, is the most transferable thing I took from those five years.

---

## What I carried forward

- **Zabbix**, arrived at by assessing alternatives when PRTG stopped being the right tool
- **Design and documentation as a habit**, not an afterthought
- **Site planning**: line of sight, path budgets, and how to work around interference
- **Adapting to available equipment** until the right equipment can be obtained
- **Managing a technical team** and working across mixed levels of experience
- **Customer communication during an outage**, including explaining a technical fault to a
  non technical customer in terms they can act on, and keeping them calm while you fix it

That last one is not a soft skill. On a network where outages were a fact of life, the difference
between a customer who renews and one who leaves was often the phone call, not the repair.

---

## Notes on this repository

Written from experience. No configuration files, client data or site photographs appear here.

**Figures are stated only where they can be defended.** Availability was monitored with PRTG but
never formally reported, so no uptime percentage appears in this document. Subscriber numbers and
efficiency improvements from that period are recollection rather than record, so they are not
claimed. What is stated here is what I can still evidence or clearly remember: the topology, the
equipment, the decisions and the reasoning.

---

**Mohamed Kabba**, IT Infrastructure Engineer, Rostock
[portfolio.kabba.tech](https://portfolio.kabba.tech) · mohamed@kabba.tech
