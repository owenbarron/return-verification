# USEFULL Return Verification Insert Module

**Document status:** Concept geometry v0.1  
**Purpose:** Save the current insert concept in a consistent, precise form before generating blueprints piece by piece.  
**Important note:** The dimensions below are **proposed concept dimensions** for image generation, discussion, and early mechanical thinking. They are not yet validated against final Bigbelly slot measurements, internal obstructions, jam-clearance testing, cleaning requirements, or vendor mounting constraints.

---

## 1. Design intent

The insert is a **removable internal verification module** that mounts directly behind the existing front slot of the current USEFULL return-station concept.

Its job is to verify a **physical return event** after QR scan.

It is **not** intended to:
- identify the exact returned SKU by vision
- decode QR codes
- inspect the messy pile inside the bin cavity

The insert should create a controlled sensing zone that lets the system confirm:
- an object actually entered the bin
- the object was substantial enough to plausibly be a USEFULL container
- the object crossed a point of no return rather than being briefly presented and pulled back out

---

## 2. Host bin reference dimensions

These are the host-bin dimensions carried forward from the current blueprint and used as the basis for the insert concept:

- **Overall front width:** 32.8 in
- **Overall side depth:** 36.8 in
- **Overall height:** 57.2 in
- **Front lower body height to slot/header break:** 47.5 in
- **Top header band height:** 6.0 in
- **Centered slot/header envelope width:** 14.0 in
- **Concrete pad reference:** 46.0 in x 38.0 in x 4.0 in

### Host-bin assumption used in this concept
For concepting purposes, the insert is assumed to live inside a **front slot/header envelope of 14.0 in W x 6.0 in H**. The true final slot opening still needs measurement.

---

## 3. Coordinate system

This spec uses a simple local coordinate system for the insert module.

- **X** = depth, measured from the front face of the insert backward into the bin
- **Y** = width, measured left to right when facing the bin
- **Z** = height, measured up from the insert floor

Reference origin:
- **X = 0.00** at the front plane of the insert
- **Y = 0.00** at the insert centerline
- **Z = 0.00** at the throat floor at the front aperture

---

## 4. Overall module envelope

### 4.1 Overall assembled insert size
- **Overall module width:** 13.50 in
- **Overall module height:** 5.50 in
- **Overall module depth:** 10.00 in

This leaves nominal clearance inside the concept host envelope of:
- **0.25 in per side** within the 14.0 in width envelope
- **0.25 in top and bottom** within the 6.0 in height envelope

### 4.2 Clear front aperture
- **Clear intake width:** 12.50 in
- **Clear intake height:** 4.50 in
- **Front aperture corner radius:** 0.25 in

### 4.3 Rear exit opening
- **Rear exit clear width:** 10.50 in
- **Rear exit clear height:** 4.00 in

### 4.4 Throat taper
The throat narrows from front to rear as follows:
- width transitions from **12.50 in** front to **10.50 in** rear over **8.00 in** of throat length
- height transitions from **4.50 in** front to **4.00 in** rear over **8.00 in** of throat length

This taper is intentional. It helps control the visual scene and encourages objects to pass through a known corridor.

---

## 5. Assembly overview

The insert is made of the following conceptual components:

1. **Front mounting frame / bezel**
2. **Outer housing shell**
3. **Matte-black throat liner**
4. **Camera bracket**
5. **Compact industrial camera**
6. **Protective optical shield**
7. **Left light bar**
8. **Right light bar**
9. **Rear commit lip / anti-sight baffle**
10. **Rear / top service cover**
11. **Drainage floor slots**
12. **Mounting tabs / flanges**

The exploded-view stack order should make sense as:

- front mounting frame
- outer housing shell
- throat liner
- camera bracket and camera
- optical shield in front of camera pocket
- left and right light bars
- rear commit lip / baffle
- service cover

---

## 6. Exact proposed component dimensions

## C-01 Front mounting frame / bezel
**Function:** Visible front structural frame that mounts the insert behind the existing slot opening.

- **Overall size:** 13.50 in W x 5.50 in H x 0.75 in D
- **Clear opening:** 12.50 in W x 4.50 in H
- **Frame border thickness:** 0.50 in nominal on left, right, top, and bottom
- **Frame thickness:** 0.125 in material
- **Corner radius, outer:** 0.25 in
- **Corner radius, inner aperture:** 0.25 in

### Mounting holes in front frame
- **Quantity:** 4
- **Hole diameter:** 0.218 in (#10 clearance concept)
- **Hole center offset from outer edges:** 0.50 in horizontally, 0.625 in vertically

---

## C-02 Outer housing shell
**Function:** Main structural body enclosing the insert.

- **Overall size:** 13.50 in W x 5.50 in H x 10.00 in D
- **Wall thickness:** 0.090 in concept sheet-metal equivalent
- **Open front:** matches bezel aperture and mounting interface
- **Open rear/bottom exit:** supports commit lip drop into main cavity

### Housing internal nominal volume before throat liner
- **Internal width:** 13.32 in
- **Internal height:** 5.32 in
- **Internal depth:** 9.82 in

(These numbers assume 0.090 in wall thickness on each side.)

---

## C-03 Throat liner
**Function:** Matte-black inner tunnel that creates the controlled sensing zone.

- **Overall liner length:** 8.00 in
- **Front internal opening:** 12.50 in W x 4.50 in H
- **Rear internal opening:** 10.50 in W x 4.00 in H
- **Liner wall thickness:** 0.063 in concept thickness
- **Finish:** matte black, non-reflective

### Wall geometry
- **Left wall taper inward:** 1.00 in total from front to rear
- **Right wall taper inward:** 1.00 in total from front to rear
- **Roof drop from front to rear:** 0.50 in total over 8.00 in depth
- **Floor remains nominally flat from X = 0.00 to X = 8.00**

### Resulting nominal taper angles
- **Side-wall taper:** approx. 7.1 degrees inward per side
- **Roof slope:** approx. 3.6 degrees downward

---

## C-04 Camera bracket
**Function:** Holds the camera in a high off-axis position.

- **Bracket overall size:** 2.75 in W x 2.50 in H x 1.50 in D
- **Bracket material thickness:** 0.125 in
- **Bracket type:** L-bracket with angled face plate

### Camera mounting face angle
- **Yaw inward toward centerline:** 18 degrees
- **Pitch downward:** 22 degrees

### Bracket mounting location
The bracket mounts to the left upper inside wall of the housing.

---

## C-05 Camera
**Function:** Primary visual sensor for passage verification.

### Concept camera body size
- **Camera body:** 1.60 in W x 1.60 in H x 1.90 in D
- **Lens protrusion:** 0.55 in beyond camera face
- **Required clear pocket around camera:** 2.20 in W x 2.20 in H x 2.50 in D

### Camera lens-center location
Measured from the insert coordinate system:
- **X = 2.00 in** behind front face
- **Y = -5.00 in** (5.00 in left of centerline)
- **Z = 4.00 in** above front-floor datum

### Camera sight target
The camera optical axis should intersect the throat center zone approximately at:
- **X = 6.50 in**
- **Y = 0.00 in**
- **Z = 2.25 in**

This keeps the camera focused on the verification corridor rather than the main bin cavity.

---

## C-06 Protective optical shield
**Function:** Protects the camera from fouling and allows wipe-clean service.

- **Shield size:** 2.50 in W x 2.50 in H x 0.118 in thick
- **Material:** clear polycarbonate concept
- **Shield recess from interior throat plane:** 0.50 in
- **Shield clear viewing zone:** centered on camera lens axis

This shield is only for the camera pocket, not a full-width throat window.

---

## C-07 Light bars (left and right)
**Function:** Provide controlled illumination independent of room conditions.

### Quantity
- **2 total**, mirrored left and right

### Per-light-bar dimensions
- **Length:** 5.50 in
- **Width:** 0.50 in
- **Height:** 0.50 in

### Per-light-bar position
Each bar runs roughly parallel to the throat depth and is mounted on the upper side walls.

#### Front and rear extents
- **Front start:** X = 1.75 in
- **Rear end:** X = 7.25 in

#### Height and offset
- mounted near the upper side-wall region
- angled **35 degrees downward and inward**

The two bars should illuminate Zone A, Zone B, and the front edge of Zone C without shining directly into the camera.

---

## C-08 Rear commit lip / anti-sight baffle
**Function:** Defines the point of no return and blocks direct sightline into the messy main cavity.

### Proposed dimensions
- **Overall width:** 10.50 in
- **Overall depth:** 2.00 in
- **Vertical drop from front edge to rear edge:** 2.25 in
- **Front edge location:** X = 8.00 in
- **Rear edge location:** X = 10.00 in

### Geometry
This part begins at the rear of the throat and slopes downward toward the main cavity.

It serves two jobs at once:
1. creates a physical threshold after which an item is committed downward
2. prevents the camera from seeing deeply into the bin interior

### Slope angle
- approx. **48.4 degrees downward** over the 2.00 in run and 2.25 in drop

---

## C-09 Service cover
**Function:** Allows access to camera, light bars, and wiring.

- **Cover overall size:** 13.50 in W x 2.00 in H
- **Cover thickness:** 0.090 in
- **Mounting:** removable fasteners, conceptually four screws
- **Preferred location:** rear or top-rear of module

---

## C-10 Mounting tabs / flanges
**Function:** Attach the insert module behind the host slot assembly.

### Side flanges
- **Quantity:** 2
- **Each flange size:** 1.00 in W x 5.50 in H x 0.125 in thick
- **Hole quantity per flange:** 3
- **Hole diameter:** 0.218 in
- **Vertical hole spacing:** 1.75 in center-to-center

These flanges are conceptual. Final pattern depends on actual host-bin attachment constraints.

---

## C-11 Drainage floor slots
**Function:** Allow liquid drainage and reduce pooling inside the throat.

- **Quantity:** 4
- **Each slot size:** 1.50 in L x 0.25 in W
- **Slot orientation:** parallel to depth axis
- **Slot centerline positions:**
  - X = 6.00 in, Y = -3.00 in
  - X = 6.00 in, Y = -1.00 in
  - X = 6.00 in, Y = 1.00 in
  - X = 6.00 in, Y = 3.00 in

These are conceptual and should be validated against debris-catching risk.

---

## 7. Detection-zone geometry

The software-visible throat is divided into three logical zones.

## Zone A – Entry
- **Depth range:** X = 0.00 to 2.50 in
- **Purpose:** confirm that an object truly entered the module

## Zone B – Passage
- **Depth range:** X = 2.50 to 7.50 in
- **Purpose:** evaluate object size, continuity of motion, and plausibility

## Zone C – Commit
- **Depth range:** X = 7.50 to 8.75 in
- **Purpose:** verify that the object crossed the point of no return before disappearing downward

### Commit threshold
- **Primary commit line:** X = 8.00 in

Beyond approximately **X = 8.75 in**, the camera should no longer have a useful direct view because the item is transitioning over the commit lip into the main cavity.

---

## 8. Proposed event-verification logic thresholds

These are preliminary software thresholds, included here only to preserve context for later blueprinting.

A **verified return event** should require all of the following:

1. object enters **Zone A** during an active return window
2. object presents sufficient visible area in **Zone B**
3. object crosses the **commit threshold at X = 8.00 in**
4. object disappears in the expected downward path
5. object does not reverse back toward the opening by more than **2.00 in** after entering Zone C

### Suggested coarse size threshold for plausibility
- minimum apparent object area in Zone B equivalent to **10 sq in** in normalized image plane terms

This is just a concept threshold for later tuning.

---

## 9. What the module is explicitly designed to do

The module should make these things visually clear in a blueprint:

- the camera looks only into a controlled tunnel
- the camera does **not** look into the messy pile in the bin cavity
- the commit lip marks the transition from “possibly inserted” to “actually returned”
- the optical shield is serviceable
- the light bars provide consistent illumination
- the whole insert is modular and removable

---

## 10. What was inconsistent in the first generated concept image

This section exists to preserve the reasoning for the next round of image generation.

### Issues in the first composite image
- exploded view implied parts that did not stack in a mechanically coherent order
- front frame, throat liner, and housing relationships were not dimensionally consistent
- optical shield looked like a large independent panel rather than a camera-pocket shield
- commit baffle geometry was not tightly tied to the throat dimensions
- rear/internal view was conceptually useful but not dimensionally anchored

### Corrections in this spec
- every major part now has a specific width, height, depth, and role
- the exploded-view order is now defined
- the camera has a precise location and target point
- the light bars have exact extents
- the commit lip has an exact start point, width, run, and drop
- the throat taper is fully defined front-to-rear

---

## 11. Recommended blueprint sequence from this spec

To build the blueprints piece by piece, generate in this order:

1. **Side cutaway only**
   - must show full throat geometry, camera location, light bars, commit lip, and sightline blocking

2. **Top plan only**
   - must show throat taper, camera pocket, light bar placement, and rear exit width

3. **Exploded insert only**
   - must follow the stack order in Section 5 and use the exact component names in Section 6

4. **Front elevation in host bin**
   - should show module fit inside the 14.0 in x 6.0 in front envelope

5. **Detection-zones inset**
   - should use the exact X-ranges in Section 7

---

## 12. Short form summary

### Host envelope used for concept
- 14.0 in W x 6.0 in H front slot/header envelope

### Final proposed insert envelope
- 13.50 in W x 5.50 in H x 10.00 in D

### Clear throat
- 12.50 in W x 4.50 in H front
- 10.50 in W x 4.00 in H rear
- 8.00 in throat length before commit feature

### Camera
- high, left, off-axis
- lens center at X = 2.00, Y = -5.00, Z = 4.00

### Light bars
- 2 units
- each 5.50 in long
- mounted from X = 1.75 to X = 7.25

### Commit lip
- starts at X = 8.00
- 10.50 in wide
- 2.00 in run
- 2.25 in drop

---

## 13. Filename / context note

This file is intended to be the authoritative saved context for the **current proposed insert geometry** before generating cleaner blueprint images one view at a time.
