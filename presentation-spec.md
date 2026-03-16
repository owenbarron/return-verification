# Return Verification — Presentation Spec

**Presenter:** Owen (PM)
**Audience:** CEO + leadership of USEFULL (small startup)
**Goal:** Present research findings, frame 3 options equally, enable a decision
**Tone:** Prepared, credible, constructive, honest about costs and unknowns
**Slides:** 11
**Format:** HTML slides (frontend-slides skill)

---

## Brand

- **Primary colors:** Deep Teal #008C95 (headers), Golden #D69A2D (accents)
- **Text:** Slate #4C4C4E
- **Backgrounds:** Foam #DDF0EE, Fog #EDECE8, white
- **Secondary accents:** Sky #238DC1, Earth #9AADA4, Wave #8FCCC8
- **Logo:** USEFULL-icons/USEFULL-Logo-Registered_Color.svg (top-left or footer)
- **Icon:** USEFULL-icons/USEFULL-Icon-Registered_Color.svg

---

## Slide 1: Title

**Return Verification System**
*AI-Camera Feasibility Research*

- Subtitle: "One potential build plan"
- Owen's name, date
- USEFULL logo

---

## Slide 2: The Problem We Were Asked to Solve

**Content:**
- Alison's ask: can we use an AI camera to verify containers are actually returned after QR scan?
- Current vulnerability: students can scan QR, walk away without dropping, or drop trash to trigger a simple sensor.

**Visual:** Simple flow diagram:
1. Student scans QR code
2. System expects a return
3. **GAP: did a real container actually drop?**

---

## Slide 3: But Is This the Right Problem?

**This slide is critical — it introduces the field evidence that complicates the ask.**

**Content:**
- NAU feedback: the problem may not be students gaming the return station. Staff believe the main problem is students + employees colluding to *never check out the containers*.
- UMass Lowell: evidence suggests students are protesting the returnable program itself, not cleverly exploiting the return process.
- Implication: a camera verification system solves a specific failure mode. Before investing, we should confirm this failure mode is actually driving losses.

**Visual:** Simple 2-column layout. Left: "What camera verification solves" (scan-and-walk-away, fake drops). Right: "What it doesn't solve" (containers never brought back, protest/non-participation, loss elsewhere in the chain).

---

## Slide 4: What Joshua Told Us

**Context:** Joshua is a computer vision consultant (referred through our fractional CTO) who runs an AI image-processing company. This concept was developed in conversation with him.

**His key guidance:**

1. **Don't point into the bin.** Looking at a messy pile of wet containers is a dead end. Focus on the entrance — the throat — where you can control the scene.

2. **More cameras beats better cameras.** Rather than one expensive industrial camera, use multiple cheap ones and collect more data from more angles.

3. **You need a lot of data to get anywhere.** This is fundamentally a scaling problem — the model needs to see thousands of real return events in all the messy real-world variations before it becomes useful.

4. **It's doable, but expect a long iteration cycle.** Even with the right approach, getting something that works even a little bit in a real food-court environment takes significant time and tuning.

**The resulting design principle:** Watch the passage, not the pile. Create a controlled sensing zone at the return slot ("throat") and verify that something substantial passed through.

---

## Slide 5: The Throat Concept

**Content:**
- Dual side-rails with cameras watching across the throat
- 4 small USB cameras: 2 main cross-view, 1 entry watcher, 1 commit watcher
- System detects: did something substantial pass fully through after a QR scan?

**Visual:** Simplified top-down diagram of the throat concept:
- 14" slot envelope
- 1.75" left rail | 10.5" clear throat | 1.75" right rail
- 4 camera positions marked (2 main cross-view, 1 entry watcher, 1 commit watcher)
- Entry zone / passage zone / commit zone labeled

---

## Slide 6: What's Inside the System

**Content — keep conceptual, not wiring-diagram level:**

**The Rails (in the wet zone):**
- Cameras sit in sealed pockets behind polycarbonate windows
- No bulky electronics in the wet zone — just optics

**The Dry Bay (sealed compartment, above splash zone):**
- Mini PC (edge compute, ~palm-sized)
- Powered USB hub
- Power distribution
- Single Ethernet out, single power in
- Field-serviceable: swap the compute node or hub, don't touch individual camera boards

**Visual:** Block diagram showing: Rails (cameras) --> USB cables --> Dry Bay (hub + mini PC) --> Ethernet out to USEFULL server. Power in on the other side.

---

## Slide 7: The Modularity Challenge

**Content:**
- The concept was designed around USEFULL's own return station (show return-station-concept.png or reference it)
- That's a controlled environment: known slot width (14"), known geometry, designed for this
- BUT: NAU may want to use their existing bins — different geometries, different slot sizes, different internal layouts
- Designing a fully modular "drop-in" system that works in any bin is significantly harder and more expensive than designing for one known form factor
- A pilot should target ONE known bin design to prove the concept before attempting modularity

**Visual:** The return station concept image on one side. On the other side, a "?" representing unknown bin geometries. Arrow between them labeled "modularity gap."

---

## Slide 8: What Would This Cost?

**Content — present as planning ranges, not quotes:**

**Joshua's estimate: $10k-$15k**
- This covers his labor only (4-5 months, including ~60 days on-site testing)
- Referred through our fractional CTO; relationship-priced
- Does NOT include: hardware, fabrication, housing design, installation, dev workstation, USEFULL software integration, cloud/inference costs

**The full picture — what his estimate leaves out:**

| Category | 2-Bin Pilot | 9-Bin Full Rollout |
|---|---|---|
| Hardware + installation | $3.5k - $6.1k | $15.7k - $27.4k |
| Housing/rail design + fabrication | $6k - $15k | $6k - $15k |
| Dev workstation | $2.5k - $4k | $2.5k - $4k |
| USEFULL software integration (Nadia + Yulia) | $21k - $38k | $21k - $38k |
| Consultant labor | $10k - $15k | $10k - $15k |
| **Subtotal before contingency** | **$43k - $78k** | **$56k - $99k** |
| **With 20% contingency** | **~$42k - $76k** | **~$57k - $101k** |

Note: recurring cloud/inference costs estimated at $500-$1,200/month if hosted inference is used later.

**Key message:** The camera hardware (~$400/bin in electronics) is not the expensive part. The expensive parts are software integration, mechanical packaging, and getting it to work reliably in a messy real-world environment.

---

## Slide 9: USEFULL Software Integration — The Hidden Bulk

**Content — this is the largest single cost bucket and leadership should understand why:**

- This is not "plug camera into server." It requires:
  - Ingesting AI detection events into USEFULL's database
  - Matching detection events to QR scan events (the hardest part — multi-scan, multi-drop, timing windows, ambiguous cases)
  - Building "scanned but not dropped" business logic and workflows
  - Ops/support tooling for reviewing ambiguous cases
  - Logging, observability, failure handling
  - QA across all of the above

- Nadia: estimated 197-359 focused hours (~$18k-$32k at loaded rate)
- Yulia (QA): estimated 60-120 hours (~$2.7k-$5.4k)
- Combined: **$21k-$38k**, likely range **$23k-$32k**

**Key message:** Even if the camera system works perfectly, USEFULL still needs significant dev effort to make it operationally useful.

---

## Slide 10: Three Options

**Present all three equally. Use a 3-column layout.**

### Option A: Engage the Consultant — Stage-Gated Pilot
- Start with 2-bin pilot at UMass Lowell (known bin geometry)
- Budget: ~$42k-$76k all-in with contingency
- Timeline: 4-5 months for consultant work + parallel USEFULL dev
- Decision gate after pilot: does it work well enough? Are false reject rates acceptable? Is maintenance burden manageable?
- Only expand to 9 bins if pilot succeeds
- **Pro:** Most thorough path; consultant brings real CV expertise; proves concept before scaling
- **Con:** Significant investment before we know if the problem it solves is the actual problem driving losses

### Option B: Small Internal Pilot (No Consultant)
- Use existing team knowledge to prototype a simpler version
- Could start with off-the-shelf cameras + basic motion detection, skip the custom throat design
- Much lower upfront cost, but lower confidence in results
- **Pro:** Cheaper to start; keeps optionality; builds internal knowledge
- **Con:** No CV expertise on team; risk of building something that doesn't actually validate the concept; could waste Nadia's time on something outside her strengths

### Option C: Shelve for Now
- Gather more data on where containers are actually being lost before investing in return-station verification
- Focus on the root causes suggested by NAU and Lowell feedback
- Revisit when/if return-station fraud is confirmed as a significant loss driver
- **Pro:** No investment risk; addresses the "are we solving the right problem?" question first
- **Con:** If the CEO's instinct is right, we lose time; consultant may not be available later at the same rate

---

## Slide 11: Key Unknowns & Recommended Next Steps

**Content:**

**What we don't know yet:**
- Whether return-station fraud is actually a significant source of container loss (NAU + Lowell evidence suggests maybe not)
- Whether the no-illumination approach works in real dining hall lighting
- Whether the cameras perform on wet, reflective surfaces in food-court conditions
- Whether NAU's existing bins can accommodate the system at all
- Whether Nadia's bandwidth can absorb this without impacting the roadmap
- Exact mechanical fit — 1.75" rails are tight once you add fasteners, brackets, cable bends

**Regardless of which option we choose, recommended immediate steps:**
1. Quantify the actual loss rate at return stations specifically (vs. other points in the container lifecycle)
2. Clarify whether NAU needs to use existing bins or would adopt USEFULL return stations
3. If proceeding: start with a 2-bin pilot at one site with known geometry — don't try to solve modularity first

**The bottom line:**
A camera-based return verification system is technically plausible. The question is whether it solves the right problem, and whether the investment is justified given what we're learning about where containers are actually being lost.

---

## Design Notes for frontend-slides

- Clean, minimal design. USEFULL brand colors throughout.
- Deep Teal for headers and key callouts
- Golden for accent elements, highlights, important numbers
- Fog or Foam backgrounds on alternating slides for variety
- Slate for body text
- Use the USEFULL logo (color SVG) in a subtle footer or top-left position
- No emojis
- Tables should be clean and readable
- Diagrams should be built with HTML/CSS/SVG — simple geometric shapes, not photorealistic
- The return-station-concept.png should appear on Slide 7 (The Modularity Challenge)
- Animations: subtle slide transitions only, nothing flashy
- Aspect ratio: 16:9 widescreen
