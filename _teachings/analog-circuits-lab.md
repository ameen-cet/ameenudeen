---
layout: course
title: Analog Circuits Laboratory
description: The companion third-semester laboratory course to Analog Circuits — hardware realization of wave shaping, amplifier, oscillator, power amplifier, and voltage regulator circuits, plus SPICE-based simulation experiments.
instructor: Ameenudeen P E
year: 2026
term: July - November
location: Department of ECE, College of Engineering Trivandrum
time: As per class timetable
course_id: analog-circuits-lab
schedule:
  - week: 1
    date: Jul 16
    topic: RC Circuits and Diode Circuits
    description: "Hardware: RC integrating and differentiating circuits. Simulation: transient analysis of RC integrating/differentiating circuits with different inputs and frequency response."
    materials:
      - name: Lab Syllabus
        url: /assets/pdf/analog-circuits-lab-syllabus.pdf
      - name: Lab Report Instructions
        url: /assets/pdf/analog-circuits-lab-report-instructions.pdf
      - name: Lab Report Instructions (LaTeX source)
        url: /assets/tex/analog-circuits-lab-report-instructions.tex

  - week: 2
    date: Jul 23
    topic: Diode Clipping and Clamping
    description: "Hardware and simulation: diode clipping and clamping circuits — transient and transfer characteristics."

  - week: 3
    date: Jul 30
    topic: CE Amplifier
    description: "Hardware: design and testing of a CE amplifier. Simulation: CE amplifier designed for a specific voltage gain, with frequency response characteristics."

  - week: 4
    date: Aug 6
    topic: CS MOSFET Amplifier
    description: "Hardware and simulation: CS MOSFET amplifier designed for a specific voltage gain, with frequency response characteristics."

  - week: 5
    date: Aug 13
    topic: Cascaded and Cascode Amplifiers
    description: "Hardware and simulation: cascaded (CE-CE) and cascode amplifiers, each designed for a specific voltage gain, with frequency response characteristics."

  - week: 6
    date: Aug 20
    topic: Feedback Amplifiers
    description: "Hardware and simulation: current-series and voltage-series feedback amplifiers designed for a specific voltage gain, with frequency response characteristics."

  - week: 7
    date: Aug 27
    topic: RC Oscillators
    description: "Hardware and simulation: RC phase-shift or Wien bridge oscillator."

  - week: 8
    date: Sep 3
    topic: Power Amplifiers
    description: "Hardware and simulation: transformer-less power amplifiers — class B and class AB."

  - week: 9
    date: Sep 10
    topic: Voltage Regulator
    description: "Hardware and simulation: transistor series voltage regulator, designed for a specific output voltage with and without short-circuit protection; load and line regulation characteristics plotted."

  - week: 10
    date: Sep 17
    topic: Consolidation and Record Completion
    description: Completion of pending experiments from Part A and Part B, and finalization of lab records.

  - week: 11
    date: Sep 24
    topic: Internal Examination (Tentative)
    description: Tentative date for the lab internal examination — preparation, conduct of experiments, viva, and timely completion of records are assessed. Unlike the theory courses, the lab does not follow the fixed series-exam schedule, so this date is subject to change.

  - week: 12
    date: Oct 1
    topic: Revision
    description: Revision and troubleshooting practice, and finalization of the lab record.
---

## Course Overview

This laboratory course accompanies the Analog Circuits theory course. It gives students hands-on experience building and testing analog circuits with discrete components, alongside SPICE-based simulation of the same circuits using open-source tools.

**Course Outcomes**

- **CO1** — Design and demonstrate the functioning of basic analog circuits using discrete components.
- **CO2** — Design and simulate the functioning of basic analog circuits using simulation tools.
- **CO3** — Conduct troubleshooting of a given circuit and analyze it.

## Part A — Hardware Experiments (any six mandatory)

1. RC integrating and differentiating circuits
2. Diode clipping and clamping circuits
3. CE amplifier — design for a specific voltage gain
4. CS MOSFET amplifier — design for a specific voltage gain
5. Cascaded amplifier (CE–CE) — design for a specific voltage gain
6. Cascode amplifier — design for a specific voltage gain
7. Feedback amplifiers (current-series and voltage-series)
8. RC oscillators — RC phase-shift or Wien bridge oscillator
9. Power amplifiers (transformer-less) — class B and class AB
10. Transistor series voltage regulator, with and without short-circuit protection

## Part B — Simulation Experiments (any six mandatory)

Conducted using open-source tools such as QUCS, KiCad, LTspice, or other SPICE variants — the same ten experiments as Part A, simulated rather than built on hardware.

## Textbooks

- David A. Bell, _Electronic Devices and Circuits_, Oxford University Press, 5th edition, 2008
- D. Meganathan, _Electronic Circuits Analysis and Design 1_, Yes Dee Publishing, 1st edition, 2023

## Grading (CIE — 50 marks)

| Component                                                                                      | Marks |
| ---------------------------------------------------------------------------------------------- | ----- |
| Attendance                                                                                     | 5     |
| Preparation / pre-lab work, viva, and timely completion of lab reports (continuous assessment) | 25    |
| Internal Examination                                                                           | 20    |

## Grading (ESE — 50 marks)

| Component                                           | Marks |
| --------------------------------------------------- | ----- |
| Procedure / preparatory work / design / algorithm   | 10    |
| Conduct of experiment / execution / troubleshooting | 15    |
| Result with valid inference / quality of output     | 10    |
| Viva voce                                           | 10    |
| Record                                              | 5     |

Students are admitted to the End Semester Examination only upon submitting a duly certified lab record, endorsed by the external examiner.
