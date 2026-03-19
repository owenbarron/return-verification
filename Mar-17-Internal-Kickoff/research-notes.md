# USEFULL AI Return Verification — Research Notes

**Purpose of this document**  
This is a detailed research / handoff document for another AI that will help write a presentation for USEFULL leadership. It is **not** an executive summary. It is intended to preserve the full reasoning, caveats, assumptions, user preferences, costs, and concept evolution discussed so far.

**Important framing**  
This document describes a **plausible build path** and a set of **presentation-worthy options**, not a final technical recommendation and not a final implementation decision.

**Core internal tension to preserve in the deck**  
- Owen has been asked by USEFULL leadership / CEO to explore an AI-camera-based solution for verifying returns in container return bins.
- Owen is **skeptical / cautious** about the project, mostly because of:
  - technical feasibility in a messy real-world environment
  - potential distraction from USEFULL’s core goals / roadmap
  - risk of underestimating integration and operational burden
- The deck should therefore:
  - present options professionally and constructively
  - make it clear that a build is possible in principle
  - budget on the **safe side** because of real uncertainties
  - avoid sounding obstructive or dismissive
  - avoid overcommitting to precision or feasibility beyond what is actually known

---

## 1. Problem statement as discussed

### Original CEO ask
Leadership wants an “AI camera” or similar AI/ML-powered device to verify that containers being dropped in return bins are actually being returned.

The CEO specifically wants a **camera-based** solution, not just a break-beam sensor or other low-tech sensor.

### Concern motivating the ask
Students can currently:
- scan a container’s QR code at the return bin
- then walk away without actually returning it

There is also concern that if return verification is based on something simple like a beam sensor, students may “monkey with it” by:
- throwing trash into the bin
- triggering the sensor without returning the actual container

### Clarified problem framing
This is **not** primarily an object-recognition problem.

USEFULL already has a QR scan event telling the system that a particular container has supposedly been returned. Therefore the real problem is closer to:

> After one or more valid QR scans, can a system verify that real physical objects actually passed into the return bin in a way consistent with real container returns, rather than fake gestures or random trash?

### Important nuance
Because the QR reader already identifies the item that was scanned, the camera system does **not** need to visually identify the exact SKU in order to be useful.

It may be helpful if the system knows the **general expected class** of object (cup-ish, bowl-ish, rectangular container-ish), but exact visual SKU verification is not required for a first plausible concept.

---

## 2. Environmental / operational constraints gathered so far

These should be carried into any deck or future design work.

### Return flow
- Users may scan **multiple** items and then drop **multiple** items.
- There is **no door or flap** on the return bin.
- Returns happen through an **open slot**.

### Container conditions
- Containers are often returned **immediately after eating** in a food court.
- They are expected to be:
  - **wet**
  - **food-smeared / dirty**
- Lids may be:
  - attached
  - not attached
- Containers should not be nested because they are individually scanned, but operational weirdness is always possible.

### Bin geometry constraints
- Existing concept slot envelope used in prior design work: **14.0 in width** at the slot/header region.
- Widest container: about **9.5 in diameter**.
- Therefore only about **4.5 in total extra width** is available around the container, which means about **2 in per side max**, and even that is tight.
- The user later refined the practical concept to roughly **1.75 in rail per side + 10.5 in clear throat**.

### Operational preference
- False rejects are **worse** operationally than false accepts.
- Honest users being penalized would create support pain.

### Deployment / site scope
- Consultant’s initial estimate was framed around **1 site with 2 return bins** at UMass Lowell.
- Real likely rollout scope is **9 return bins total**:
  - 2 at UMass Lowell
  - 7 at NAU

---

## 3. Why the project is hard / what to preserve as risk framing

The original skepticism should be preserved in the deck in a constructive way.

### Fundamental difficulty
The challenge is not “can a model detect a container in a clean lab demo?”
The challenge is whether a system can work reliably in a:
- low-light
- wet
- reflective
- dirty
- user-interactive
- operationally variable
environment.

### Major sources of uncertainty
1. **Scene control**  
   A vision system becomes much more plausible if the scene is controlled. It becomes much less plausible if leadership expects arbitrary retrofit into many different existing bins with different geometries and lighting.

2. **Open-slot multi-item behavior**  
   Because there is no door, users can scan several objects and then drop several objects quickly. That complicates event matching.

3. **Occlusion and spoofing**  
   Hands, partial insertions, small trash objects, or quick gestures all make event verification harder.

4. **Dirty optics / maintainability**  
   If camera windows get smeared or splashed, performance will degrade.

5. **Mismatch between “camera idea” and real system**  
   The expensive / difficult parts are not just cameras. They are:
   - mechanical packaging
   - field servicing
   - data integration
   - event matching logic
   - support tooling
   - false-positive / false-negative tuning

### Key phrasing to preserve
A strong and accurate way to frame this internally is:

> The biggest uncertainties are not camera purchase cost; they are environmental robustness, mechanical integration into existing bins, event-matching logic with USEFULL scans, and operational performance in live dining environments.

---

## 4. High-level architecture evolution discussed so far

### Early concept: “camera in the bin”
At the start, the concept was loosely about an “AI camera in the bin.”

### Refined concept: controlled return throat
The more plausible direction became:
- create a **controlled sensing zone** in or around the return throat / slot
- avoid looking into the messy pile in the main bin cavity
- verify a **return event** rather than doing broad interior object recognition

### Core idea that both Owen and consultant aligned on
Design around a **return-bin throat** with cameras surrounding or looking across the throat.

### Strong design principle that emerged
Do **not** rely on a camera viewing the pile in the bottom of the bin.
Instead:
- create a controlled passage region near the slot
- watch that region only
- determine whether something substantial passed fully through into the bin

### Consultant’s added suggestion
The consultant recommended **quantity over quality**:
- rather than spending heavily on one fancy industrial camera
- use multiple lower-cost cameras
- collect raw data
- process centrally or on a local host

This is an important option to preserve in the deck.

---

## 5. Detailed concept geometry discussed so far

This section captures the concept geometry that was developed for image-generation and discussion purposes. This is **not** production mechanical design.

### Host bin dimensions carried from existing blueprint concept
These are the numbers used as the basis for concepting:
- Overall front width: **32.8 in**
- Overall side depth: **36.8 in**
- Overall height: **57.2 in**
- Front lower body height to slot/header break: **47.5 in**
- Top header band height: **6.0 in**
- Centered slot/header envelope width: **14.0 in**
- Concrete pad reference: **46.0 in × 38.0 in × 4.0 in**

### Earlier “boxed insert” concept
An earlier concept assumed a removable insert roughly around:
- 13.5 in overall width
- 5.5 in overall height
- 10 in overall depth
with:
- throat liner
- commit lip / baffle
- camera pocket
- light bars
- dry bay elsewhere

This concept was useful for thinking, but later felt too bulky.

### Revised “dual side-rail” concept
Because of the tight 14-inch slot and the 9.5-inch max container diameter, the design evolved into:
- **Left rail:** ~1.75 in width
- **Clear center throat:** ~10.5 in width
- **Right rail:** ~1.75 in width
- Total width: **14.0 in**

This leaves about **0.5 in clearance per side** around a 9.5 in max-diameter container.

### Revised top-plan logic
Use two thin optical side rails rather than a bulky enclosed throat module.

The rails contain cameras and optical windows. Bulk electronics live elsewhere in a dry bay.

---

## 6. Specific 4-camera rail concept discussed

### Why 4 cameras
The consultant suggested a lower-cost, multi-camera approach. A plausible concept became:
- 2 “main” low-light cameras looking across the throat
- 2 smaller “helper” cameras resolving edge cases at entry and commit

### Functional roles
- **Main cameras (left and right):** overlapping cross-throat views
- **Entry helper:** confirm that an object truly entered the throat rather than just flashed at the opening
- **Commit helper:** confirm that the object reached the point of no return toward the back of the throat

### Exact conceptual top-plan layout used in prompts
Coordinate convention:
- **X** = depth into the bin from the slot face
- **Y** = width across the throat

Front / user side at bottom of plan; rear / bin cavity side at top.

#### Overall top-plan envelope
- Overall slot/module envelope width: **14.0 in**
- Overall module depth shown in top plan: **8.0 in**

#### Rail/throat widths
- Left rail: **1.75 in**
- Clear throat: **10.50 in**
- Right rail: **1.75 in**

#### Software zones
- **Zone A (Entry):** X = 0.0 to 2.5 in
- **Zone B (Passage):** X = 2.5 to 7.5 in
- **Zone C (Commit):** X = 7.5 to 8.0 in
- Commit threshold at **X = 8.0 in**

#### Camera positions and roles
**Left rail**
- **L1 — Left main camera**
  - Concept pocket size: ~1.50 in × 1.50 in
  - Lens center: X = 2.0 in, Y = -6.1 in
  - Yaw: 28° inward
  - Target point: X = 6.0 in, Y = 0.0 in
- **L2 — Left helper / entry watcher**
  - Smaller pocket size: ~0.80 in × 0.65 in
  - Lens center: X = 0.8 in, Y = -6.2 in
  - Yaw: 20° inward
  - Target point: X = 1.8 in, Y = 0.0 in

**Right rail**
- **R1 — Right main camera**
  - Pocket size: ~1.50 in × 1.50 in
  - Lens center: X = 2.0 in, Y = +6.1 in
  - Yaw: 28° inward
  - Target point: X = 6.0 in, Y = 0.0 in
- **R2 — Right helper / commit watcher**
  - Smaller pocket size: ~0.80 in × 0.65 in
  - Lens center: X = 6.8 in, Y = +6.2 in
  - Yaw: 24° inward
  - Target point: X = 7.8 in, Y = 0.0 in

### Conceptual logic of this layout
- L1 + R1 do the main work by seeing across the throat from opposite sides.
- L2 helps answer: did something really enter?
- R2 helps answer: did something really commit / pass the threshold?

This is an intentionally asymmetrical helper arrangement and should be described that way.

---

## 7. What the system is trying to verify (important for deck wording)

The system is not trying to prove exact identity by vision.

It is trying to verify something like:

> After one or more valid QR scan events, did one or more substantial physical objects pass through the return throat into the bin in a way consistent with real returns?

### Things the system is trying to prevent
- Scan and walk away
- Scan and fake-drop
- Scan and briefly insert then remove
- Scan and throw in small trash
- Scan multiple items but physically return fewer

### Important business logic nuance
Because users may scan multiple items and then return multiple items, the matching logic should be thought of as a **scan queue** and **return-event counter**, not a one-scan / one-drop lockstep.

Plausible queue logic:
- user scans N items
- system opens a return window
- verified passage events decrement the queue
- if fewer passage events than scans occur, remaining items stay outstanding

---

## 8. Dry bay architecture discussed so far

### Why a dry bay exists
The rails should contain only optics / small cameras / small windows, not bulky electronics.
Bulk electronics should live in a separate protected compartment inside the bin.

### Dry bay purpose
The dry bay is the “boring but critical” part:
- keeps compute and hub out of the wet zone
- makes service easier
- keeps field techs from manipulating raw camera boards in the dirty area

### Conceptual contents of the dry bay
1. Local computer / edge host
2. Powered USB hub
3. Power distribution
4. Network handoff (one Ethernet out of the bin)
5. Cable management / strain relief / service hardware

### Recommended physical organization
A sealed or gasketed access compartment above the splash zone / above the bag line.

Inside on a backplate:
- mini PC / local host
- powered USB hub
- power strip or DC distribution block
- service disconnect / fuse / breaker
- cable strain-relief bar
- Ethernet handoff / coupler / gland

### Service philosophy
Field-serviceable units should be:
- left rail cassette
- right rail cassette
- hub
- local compute node
- optical window covers

Should **not** be field-serviceable:
- loose camera boards
- tiny lens mounts
- individual board-side connectors in the wet zone

### Recommended local software appliance behavior
At boot, local node should:
1. detect all cameras
2. verify expected mapping
3. start capture service
4. start event-detection service
5. start local clip buffer
6. start uploader / API client
7. report health upstream

### External connections goal
Keep external connections minimal:
- 1x power in
- 1x Ethernet out

---

## 9. Specific parts / vendor options discussed

**Important:** these are all examples and references for a plausible build. They are **not final decisions**. Prices should be re-checked before any purchasing.

### A. Low-light / helper camera candidates discussed

#### Waveshare SC2210 2MP USB Camera (A)
Use case discussed:
- main low-light rail camera candidate

Discussed characteristics:
- 2MP USB camera
- “starlight” positioning
- board size around 38 × 38 mm (~1.50 in square)
- approximately suitable for 1.75 in rail packaging
- earlier referenced price: **$57.99 each**

Referenced source:
- https://www.waveshare.com/sc2210-2mp-usb-camera-a.htm

#### Waveshare OV2710 2MP USB Camera (A)
Use case discussed:
- lower-cost helper or budget camera option

Discussed characteristics:
- USB 2.0 / UVC
- lower cost than SC2210
- wide-angle / low-light-ish option
- earlier referenced price: **$34.99 each** in one path

Referenced source:
- https://www.waveshare.com/ov2710-2mp-usb-camera-a.htm

#### Waveshare OV9281 USB camera (from later hardware costing pass)
Use case discussed:
- helper camera in a lower-cost BOM pass

Discussed characteristics:
- smaller / lower-cost helper option used in one cost model
- earlier referenced price: **$25.99 each**

Note:
- This part was used in one later costed electronics subtotal but was not the original helper choice in the rail packaging discussion. Preserve that inconsistency as an open choice.

#### Arducam IMX291 mini USB camera
Use case discussed:
- very small helper camera candidate for entry / commit roles

Discussed characteristics:
- compact board size around 19.5 × 15 × 17.3 mm
- better physical fit for helper role in narrow side rails
- low-light-oriented

Referenced source:
- https://blog.arducam.com/downloads/datasheet/B0520_IMX291_USB_Camera_Datasheet.pdf

#### e-con Systems See3CAM_CU27 (Sony IMX462)
Use case discussed:
- more established / higher-quality low-light / near-IR option
- possible upgrade path if cheaper cameras are insufficient

Discussed characteristics:
- IMX462 / STARVIS-type low-light / NIR sensitivity
- earlier referenced price around **$89**
- good for low-light / near-IR regions
- not a comfortable fit if using enclosed module dimensions in very narrow rails

Referenced source:
- https://www.e-consystems.com/usb-cameras/sony-starvis-imx462-ultra-low-light-camera.asp

### B. Local compute and USB aggregation

#### StarTech HB30A3A1CST powered USB hub
Use case discussed:
- mountable powered hub in the dry bay

Discussed characteristics:
- metal mountable hub
- 3 USB-A + 1 USB-C in one referenced version
- self-powered
- earlier referenced price about **$24.59** in later costing pass; earlier another pass referenced a higher reseller price around **$72**

Important note:
- preserve that prices varied across passes and should be re-verified.

Referenced source(s):
- https://www.startech.com/en-us/usb-hubs/hb30a3a1cst
- or reseller pages used in earlier research

#### GMKtec NucBox G3 Plus / G3 class mini PC
Use case discussed:
- small local edge host in dry bay

Discussed characteristics:
- N100-class mini PC concept
- small x86 box
- Ethernet
- enough USB / hub support
- earlier referenced planning price about **$200**

Referenced source:
- https://de.gmktec.com/en/products/gmktec-nucbox-g3-intel%C2%AE-alder-lake-n100

#### Minisforum UN100P (alternative mini PC reference)
Use case discussed:
- another example N100 mini PC
- used in one earlier BOM pass

Referenced source:
- https://www.minisforum.com/products/minisforum-un100p-1

### C. Dry bay enclosure / no-custom-tooling parts

#### Hammond PCJ12106 polycarbonate enclosure
Use case discussed:
- dry bay enclosure candidate

Discussed characteristics:
- NEMA 4X / IP66-ish product family positioning
- ~12 in × 10 in × 6 in external size in one discussed configuration
- enough room for mini PC + hub + service loops
- off-the-shelf, drillable, modifiable

Referenced source:
- https://www.hammfg.com/part/PCJ12106
- family literature: https://www.hammfg.com/files/literature/pcj.pdf

#### Polycase weatherproof enclosure family
Use case discussed:
- alternative dry-bay enclosure vendor

Referenced source:
- https://www.polycase.com/

#### 80/20 1020-S extrusion
Use case discussed:
- side-rail structural backbone

Discussed characteristics:
- 1.00 in × 2.00 in smooth profile
- off-the-shelf stock length
- can act as revisable rail backbone with brackets/windows attached

Referenced source:
- https://8020.net/1020-s.html

#### Clear polycarbonate sheet (McMaster)
Use case discussed:
- sacrificial optical windows / simple rail covers

Referenced source:
- https://www.mcmaster.com/products/polycarbonate-sheets/

#### Heyco liquid-tight cord grips
Use case discussed:
- sealed cable pass-throughs for dry bay

Referenced source:
- https://www.heyco.com/products/liquid-tight-cordgrips/

---

## 10. Illumination discussion / user preference

### Earlier technical thought
Controlled illumination in the throat was originally suggested as a strong way to reduce variability.

### User preference / presentation constraint
Owen later said:

> let’s not do illumination for now, it might look weird.

This should be preserved.

### How to frame that
- Illumination could improve consistency
- But for near-term concept presentation and physical plausibility, it may add visual bulk / weirdness / user-perception issues
- Therefore the current concept path assumes **no dedicated visible illumination in the throat for now**
- Low-light / NIR-capable cameras are still discussed, but no explicit illuminator is committed in the current presentation direction

This is a **preference and presentation choice**, not proof that illumination is unnecessary.

---

## 11. Compute / model development discussion

### Model family discussed
At one point YOLOv8 was mentioned as a likely model family. Later research indicated Ultralytics now positions **YOLO11** as current default, but that change is not important for the deck beyond the point that a modern YOLO-family detector is plausible.

### Development compute need
The consultant’s initial estimate did **not** include a development tower / workstation.

A separate workstation is likely needed for:
- model training / fine-tuning
- clip review
- labeling
- test iteration
- basic video analysis

### Safe planning spec discussed
A reasonable tower planning spec was framed roughly as:
- RTX 4070 SUPER–class GPU or better
- 64GB RAM
- 2TB NVMe SSD
- modern CPU

### Development workstation budget range used
- **$2,500–$4,000** planning range

### Important note about inference architecture
Do **not** present “must transition to hosted inference” as settled fact.

Safer phrasing:
- During pilot, edge-first / local-first processing is lower risk.
- Hosted inference may become attractive later for centralized monitoring / model ops / logging / easier updates.
- This is an open architectural question, not a settled design decision.

---

## 12. Hosted inference / cloud cost discussion

### Known usage number supplied
Expected return volume across the two campuses discussed:
- **23,000 return events per month**
  - 16,000 for NAU
  - 7,000 for UMass Lowell

### Framing that should be preserved
Do not say cloud cost is known precisely. Say:
- If event-triggered clips / frames are processed centrally, traffic volume is not absurd.
- Monthly hosted processing might be moderate, but depends heavily on:
  - whether inference is event-triggered or continuous
  - how much video is stored
  - whether endpoints are always on
  - logging / observability requirements

### Safe-side monthly cost range discussed
- **$500–$1,200/month** for hosted inference + storage + monitoring was used as a conservative planning range.

### Important nuance
This range is not a final quote.
It is a planning assumption to avoid under-budgeting.

---

## 13. Consultant estimate and how it should be framed

### Consultant relationship / context
The consultant:
- was referred through USEFULL’s fractional CTO
- runs an AI image-processing company
- would be doing this in his own capacity
- is approaching it partly as a relationship-building / passion-project kind of engagement

This context matters because:
- his estimate may be somewhat favorable / relationship-priced
- it may not include all hidden internal or field costs

### Ballpark consultant estimate received
The consultant estimated:
- **$10k–$15k** total
- **4–5 months** total timeline
- including:
  - **60–90 days** of initial design & testing
  - about **60 days** of initial testing at client site in real-world situations

### Later internal assumption for budget model
At one point the working assumption became:
- **$8k** for consultant’s personal labor

This is a useful internal number for budgeting, but it differs from the earlier $10k–$15k total framing. Preserve that nuance.

### Important caution
His estimate did **not** include several major cost buckets. Those omissions should be called out explicitly in the deck.

---

## 14. Major items explicitly identified as not included in consultant estimate

These should appear clearly in the research basis for the deck.

### Not included
1. Development workstation / tower to run the model during dev and testing
2. Fabrication / design of housing that holds cameras, connectors, computing devices
3. Monthly AI image-processing / cloud inference costs
4. Installation of modules in existing return bins
5. USEFULL software development costs, including:
   - ingest AI detection data into USEFULL DB
   - correlate detection data with USEFULL scan events
   - build logic for “scanned but not dropped” handling

### Important resulting takeaway
The consultant’s $10k–$15k should be presented as a **partial technical prototype estimate**, not a true all-in project estimate.

---

## 15. Hardware BOM / per-bin cost estimates discussed

### Important caution
Several BOM variations were discussed. Preserve that these are **conceptual cost models**, not settled purchasing decisions.

### A. Earlier 4-camera / 2 IR + 2 helper style thinking
One concept path used:
- 2 stronger low-light / “IR” main cameras
- 2 helper cameras
- USB hub
- local host

This was more of an architecture concept than a fully normalized BOM.

### B. Later “known-cost electronics subtotal” used for budgeting
A later cleaner cost model used:
- 2 × Waveshare SC2210 main cameras @ $57.99 each
- 2 × Waveshare OV9281 helper cameras @ $25.99 each
- 1 × StarTech HB30A3A1CST powered USB hub @ $24.59
- 1 × GMKtec NucBox G3 Plus mini PC @ $200

That gave a known-cost electronics subtotal of about **$392.55 per bin**.

Across **9 bins**, that subtotal becomes about **$3,532.95**.

### Safe-side per-bin planning number used later
Because electronics alone understate reality, the safer planning number became:
- **$1,000–$1,550 per bin in parts**
- **$1,750–$3,050 per bin installed**

This broader range includes:
- cameras
- host
- hub
- enclosure / dry bay
- rails / brackets / windows
- connectors / glands / harnessing
- miscellaneous fabrication
- install labor (in installed total)

### Installed-cost examples used
- **2 bins installed:** $3.5k–$6.1k
- **9 bins installed:** $15.7k–$27.4k

These are presentation-friendly planning ranges and should be treated as such.

---

## 16. Overall project budget ranges discussed

This section is especially important for the eventual deck.

### Safe-side framing that emerged
A real pilot is not a $10k–$15k project once omitted costs are included.

### 2-bin pilot budget framing discussed
For a 2-bin pilot, the total all-in conservative planning range discussed was:
- **$35k–$63k one-time**, before recurring cloud costs
- with **20% contingency:** **$42k–$76k**

### 9-bin total program framing discussed
If the concept later expands to all 9 bins:
- total project cost estimated at about **$47k–$84k**
- with **20% contingency:** **$57k–$101k**

### Why those totals are much higher than the consultant figure
Because they include:
- consultant labor
- hardware
- dry bay / rails / packaging / fabrication
- installation
- development workstation
- USEFULL software work
- QA
- recurring platform / inference assumptions
- contingency

### Important nuance to preserve
These are **safe-side planning numbers**, not quotes.
They are appropriate for executive budgeting because the project has multiple known unknowns.

---

## 17. USEFULL software integration costs — detailed breakout

This section should be especially detailed because the user explicitly asked to break it out.

### Team members
- **Nadia**: primary developer
- **Yulia**: QA

### Nadia compensation assumptions discussed
- Nadia salary: **$120k/year**
- 4 weeks off
- user calculated raw rate at **$62.50/hr**

### Important user note
User explicitly said:
- Nadia is not always working exactly 40 hours/week of maximum productivity
- any dev estimate has to be padded for:
  - meetings
  - system setup
  - knowledge transfer
  - context switching
  - general overhead

### Effective Nadia planning rate used
A padded internal planning rate was recommended:
- use about **$90/hr** for Nadia in planning
- rationale: 1.4–1.5x overhead on top of raw internal rate

### Nadia work packages discussed
#### A. Integration design and interface definition
- determine what data comes from AI system
- identifiers / confidence / timestamps / retries
- estimate: **15–25 focused hours**

#### B. Event ingestion pipeline
- receive / validate / normalize / store detection events
- estimate: **20–35 focused hours**

#### C. DB / schema work
- tables / fields for AI events, matching status, confidence, audit
- estimate: **12–24 focused hours**

#### D. Matching logic: scan event ↔ return detection
This was identified as the hardest part on USEFULL side.
Includes:
- multiple scans / multiple drops
- delayed drops
- unclear ordering
- windowing logic
- ambiguous matching
- estimate: **40–70 focused hours**

#### E. “Scanned but not dropped” workflow logic
- grace windows
- reprocessing
- business rules
- exception states
- estimate: **25–50 focused hours**

#### F. Ops / support tooling
- viewing unmatched events
- reviewing confidence / ambiguity
- correcting mistakes
- debugging
- estimate: **20–40 focused hours**

#### G. Logging / observability / failure handling
- did AI send data?
- did USEFULL ingest it?
- why did matching fail?
- estimate: **20–35 focused hours**

#### H. QA support / bug fixing / rollout support
- patching edge cases during pilot
- estimate: **30–55 focused hours**

#### I. Knowledge transfer / coordination / deployment support
- consultant sync
- QA sync
- operations support
- estimate: **15–25 focused hours**

### Nadia total hours and cost discussed
Total Nadia estimate:
- **197–359 focused hours**

At **$90/hr**, this becomes:
- **$17,730–$32,310**

Rounded / presentation-friendly Nadia range:
- **$18k–$32k**

### Yulia / QA assumptions discussed
User later supplied:
- Yulia costs about **$45/hr**

QA support range discussed:
- **60–120 hours**

This becomes:
- **$2,700–$5,400**

### Combined USEFULL internal range discussed
Nadia + Yulia combined:
- **$20,700–$37,800**

Rounded / deck-friendly range:
- **$21k–$38k**

“Tighter most-likely” range discussed:
- **$23k–$32k**

### How to present internally
Good deck phrasing:
- Nominal Nadia rate is $62.50/hr, but planning should assume ~$90/hr effective engineering time because of context switching, setup, coordination, testing support, and rework.
- USEFULL software integration and QA should be budgeted around **$21k–$38k**, with **$23k–$32k** as a likely range.

---

## 18. Installation / fabrication cost framing discussed

### Installation
Recommended safe planning assumption:
- **$750–$1,500 per bin**

Why:
- retrofit into existing bins is non-trivial
- mounting, routing, sealing, final fit-up likely requires contractor / fabricator help

### Housing / rail design and prototype fabrication
Recommended safe planning assumption:
- **$6k–$15k one-time**

Includes:
- rail design iteration
- bracket design
- modifying enclosures
- test-fit cycles
- prototype rebuilds

### Important nuance
For the first 10 units, the recommended approach was **COTS + light fabrication**, not full custom-manufactured parts.

---

## 19. Recommendation style that emerged

This is a key message for the eventual deck.

### Recommended strategic posture
Treat this as a **stage-gated pilot**, not a broad deployment commitment.

### Example phase framing discussed
#### Stage 1 — 2-bin technical pilot (likely UML)
Goal:
- prove the throat/rail concept works in real-world conditions
- prove event matching can be made operationally acceptable

#### Stage 2 — decision gate
Only proceed if pilot performance is acceptable for:
- false reject rate
- false accept rate
- maintenance burden
- support burden

#### Stage 3 — optional expansion to 9 bins
Expand only if pilot merits it.

### Tone guidance
The deck should sound:
- prepared
- constructive
- serious
- committed to doing the due diligence

It should **not** sound like:
- “this is impossible”
- “we should definitely do it”
- “here is a single obvious solution”

The right tone is more like:

> Here is a plausible build path, here are the options, here are the real uncertainties, and here is the budget range we should assume if we want to explore it responsibly.

---

## 20. Known unknowns / open questions to preserve

This section is very important. These are not nuisances — they are the heart of why safe-side budgeting is appropriate.

### Mechanical / industrial design unknowns
- Exact usable internal dimensions behind the slot
- Whether Bigbelly / existing-bin geometry allows the rail layout without interference
- Cleaning access and replacement strategy for optical windows
- Whether 1.75 in rails are truly enough once fasteners, brackets, windows, and cable bends are included
- Whether service access is acceptable in the real bin interior

### Computer vision / data unknowns
- Whether no-illumination approach is sufficient in live lighting conditions
- Whether cheaper low-light cameras perform adequately on wet reflective metal in food-court conditions
- What clip lengths / frame rates are needed
- Whether helper cameras materially improve false reject / false accept performance
- Whether event-triggered clips are enough or continuous video is required for debugging

### Product / operations unknowns
- How “returned in time” should be defined
- What business logic should do in ambiguous cases
- Whether ops teams can maintain / clean the system consistently
- How often false rejects will create support tickets
- How much manual review tooling is needed

### Deployment unknowns
- Whether existing bins at both campuses are sufficiently similar
- Whether installers can retrofit without major bespoke work per bin
- Whether network / power availability at each bin is straightforward

### Organizational / prioritization unknowns
- Opportunity cost versus USEFULL’s main goals
- whether Nadia’s bandwidth can absorb the pilot without harming roadmap commitments
- whether leadership wants a technical pilot, an operational pilot, or both

---

## 21. Things that should be emphasized as “plausible build” not final decision

These should be explicit in the notes or deck prep.

### Not final decisions
- exact camera models
- exact number of cameras per bin
- whether helper cameras are OV9281, IMX291, or other
- whether local host is GMKtec, Minisforum, or another mini PC
- whether inference is local-only, hybrid, or hosted
- exact rail / enclosure fabrication method
- whether illumination is eventually added
- whether 2-bin pilot happens at UMass Lowell only or in a mixed-site configuration

### Strong wording to preserve
This is a **plausible build path** and **planning model**, not a locked solution.

---

## 22. Suggested visuals / images that another AI could use in the deck

The user explicitly asked for realism about what AI image generation can and cannot do.

### General rule for visuals
Use visuals to:
- illustrate concepts
- create intuition
- show plausible system layouts

Do **not** overclaim precision through visuals.

### A. Visuals that could realistically be AI-generated

#### 1. Simplified top-plan blueprint of dual side-rail concept
Could generate:
- clean engineering-style top plan
- 14 in envelope
- 1.75 in side rails
- 10.5 in clear throat
- 4 camera pockets
- sightlines
- entry/passage/commit zones

This is already close to feasible from AI image-gen and can be used as a conceptual diagram.

#### 2. Side cutaway concept of bin throat + rails + dry bay
Could generate:
- side sectional concept
- slot opening
- rails near throat
- dry bay elsewhere in bin
- simple arrows showing data flow

Needs to stay conceptual, not detailed production CAD.

#### 3. Dry bay block diagram
Could generate or simply draw as a slide-native diagram:
- rails
- harnesses
- hub
- compute node
- power distribution
- Ethernet out

This does not need image generation; can be a clean vector/block slide.

#### 4. Conceptual “system architecture” graphic
Could show:
- scan event
- camera verification
- local compute
- USEFULL DB / server
- logic for “matched / unmatched / ambiguous”

This is better as a simple diagram than a photoreal image.

#### 5. “Stage-gated pilot” roadmap diagram
Could show:
- 2-bin pilot
- decision gate
- optional 9-bin expansion

Best as simple slide-native graphic.

### B. Visuals that are better pulled from vendor / real websites rather than AI-generated
These are useful because they anchor the presentation in real parts and lower the sense that the concept is purely speculative.

#### 1. Example camera boards
Use product images from sites for:
- Waveshare SC2210
- Waveshare OV2710 / OV9281 (if selected)
- Arducam IMX291 mini
- e-con IMX462 / See3CAM_CU27

These can illustrate size / board-style packaging.

#### 2. Mini PC example
Use product image from:
- GMKtec NucBox G3 Plus or similar
- Minisforum UN100P or similar

#### 3. Powered USB hub
Use product image from:
- StarTech mountable powered USB hub

#### 4. Dry bay enclosure and rail materials
Use vendor imagery for:
- Hammond PCJ enclosure
- 80/20 1020-S extrusion
- Heyco cord grips
- clear polycarbonate sheet or generic window material

### C. Visuals that should probably *not* be over-generated by AI
These are likely to come out inconsistent or overly polished in ways that imply false precision.

#### Avoid relying on AI for:
- fully coherent exploded mechanical assembly unless carefully constrained
- realistic production CAD with fasteners, exact assembly order, etc.
- polished final industrial design renders that look “done”

If used, these should be labeled as **concept sketches**.

### D. Visual strategy suggestion for presentation generator AI
For some slides, it may be better to:
- use a simple concept image
- then let the presentation generator put text / labels around it
rather than trying to get one single AI-generated image to be perfectly complete.

---

## 23. Images already conceptually attempted / feedback to preserve

A dual-side-rail top plan concept was generated and reviewed.

### What was considered successful in that image
- Big idea came through clearly
- side rails instead of bulky center throat module
- 2 main cameras + 2 helpers was legible
- clear center throat was preserved
- commit threshold concept was visible

### What was still wrong / inconsistent
- zones were oriented incorrectly in one version
- one camera coordinate label drifted from spec
- axis marker was wrong in one version
- some harness labels were messy
- image was a good concept sketch but not an authoritative engineering drawing

### Conclusion from that discussion
The visual is useful as a concept illustration, but should not be treated as mechanically authoritative.

---

## 24. Presentation-writing implications for another AI

The AI that reads this should understand the following:

### What to do
- extract an executive summary later
- present a few options without pretending certainty
- emphasize stage-gated evaluation
- preserve the user’s safe-side budgeting stance
- explain that the consultant estimate is partial, not all-in
- distinguish core camera/electronics cost from full system cost
- keep the project framed as plausible but uncertain

### What not to do
- do not present a single architecture as final
- do not imply the project is trivial
- do not imply cloud/hosted inference is already decided
- do not imply exact mechanical fit is solved
- do not say that hardware is the main cost driver
- do not erase Owen’s concern about distraction from core company goals

### Key tone objective
The presentation should read as:
- well researched
- technically credible
- appropriately cautious
- supportive of leadership decision-making

not as:
- evangelism
- sabotage
- a final engineering recommendation

---

## 25. Concise list of likely slide topics (not an exec summary, just organizational guidance)

This is not the slide content itself; it is just a useful organizational map for another AI.

Potential slide buckets:
1. Why this project is being explored / problem statement
2. What problem the camera is actually solving
3. Why a throat-based design is more plausible than “camera in the bin”
4. Option set: cheap multi-camera edge node vs higher-end camera path vs “do not proceed yet” / stage-gated evaluation
5. Plausible 4-camera dual-rail concept
6. Dry bay / installation architecture
7. What is and is not included in the consultant estimate
8. Safe-side pilot budget and 9-bin expansion budget
9. USEFULL software integration effort
10. Open questions / decision gate

---

## 26. Final reminders for the next AI

- Treat all numbers here as planning numbers unless explicitly sourced otherwise.
- Re-verify current component prices before presenting as exact.
- Preserve the distinction between **known-cost electronics subtotal** and **all-in pilot budget**.
- Keep the phrase **“plausible build path”** alive.
- Preserve that many visuals are conceptual and not production drawings.
- The executive audience should leave feeling:
  - there is a viable concept worth evaluating,
  - the uncertainties are real,
  - and the budget should be sized to those uncertainties.

