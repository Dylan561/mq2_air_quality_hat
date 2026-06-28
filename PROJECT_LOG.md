# Project Log — MQ-2 Air Quality HAT

Running log of decisions, problems, and fixes throughout the design and build.
Add a new entry every time you make a non-trivial decision or hit/fix a problem —

Format per entry:
- **Date**
- **What I did / decided**
- **Why** (the reasoning)
- **Problems hit** (if any) and how they were resolved

---

## 2026-06-28 — initial commit: created schematic

**What:** Wired Pi GPIO header 5V/GND, MQ-2 heater on 5V, ADS1115 VDD on 5V. Created basic schematic draft

**Why:** Followed reference MQ-2 wiring diagram for divider; assumed ADS1115 could also run on 5V since it's within its absolute max rating.

**Problems hit:** None yet

---

## 2026-06-28 — added 3.3V line for ASD1115.

**What:** Moved ADS1115 VDD from the 5V rail to the new 3.3V rail.

**Why:** ADS1115 logic pins (SDA/SCL/ALERT) swing close to VDD. Running VDD at 5V would put ~5V logic levels into the Pi's 3.3V-only GPIO pins — outside the Pi's tolerance. MQ-2 heater stays on 5V since it's a separate, isolated circuit (heater pins are not connected to the sensing/logic side).

**Problems hit:** Caught this during a design review before layout — no rework needed since it was still schematic stage.

---

## 2026-06-28 — Added pulldown for unused ADC channels

**What:** Added R5 (10k) pulling AIN1/AIN2/AIN3 to GND since only AIN0 is used.

**Why:** Floating CMOS/analog inputs can pick up noise from nearby switching signals (e.g. I2C lines toggling close by) and don't settle to a predictable value. A weak pulldown gives a defined, low-noise resting state instead of an undefined floating voltage.

**Problems hit:** None

---

## 2026-06-28 — changed R3 and R4 to 4.7k

**What:** Changed R3 and R4 to 4.7k Ohms

**Why:** Since Raspberry Pi already has internal pull up resistors

**Problems hit:**

---
<!--
TEMPLATE — copy this block for each new entry:

## YYYY-MM-DD — [short title of what changed]

**What:**

**Why:**

**Problems hit:**

-->
