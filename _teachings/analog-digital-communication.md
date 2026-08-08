---
layout: course
title: Analog and Digital Communication
description: A fifth-semester core course (PCECT502) analyzing analog and digital communication systems — amplitude and angle modulation, receivers, sampling and quantization, baseband transmission, and digital band-pass modulation.
instructor: Ameenudeen P E
year: 2026
term: July - November
location: Department of ECE, College of Engineering Trivandrum
time: As per class timetable
course_id: analog-digital-communication
schedule:
  - week: 1
    date: Jul 16
    topic: Amplitude Modulation
    description: Block diagram of a communication system, need for modulation. Amplitude modulation — equation and spectrum of the AM signal, DSB-SC, SSB (pilot carrier), and vestigial sideband systems.
    materials:
      - name: Course Syllabus
        url: /assets/pdf/analog-digital-communication-syllabus.pdf
      - name: Course Project Handbook
        url: /assets/pdf/analog-digital-communication-project-handbook.pdf

  - week: 2
    date: Jul 23
    topic: Angle Modulation
    description: Narrowband and wideband FM and their spectra, relationship between FM and PM, Carson's rule, pre-emphasis and de-emphasis filtering, comparison of AM and FM, block diagram of an FM receiver.

  - week: 3
    date: Jul 30
    topic: Receivers and Noise
    description: Superheterodyne receivers — characteristics of receivers, image frequency. Noise — external, internal, and white noise.

  - week: 4
    date: Aug 6
    topic: Sampling, PCM, and Delta Modulation
    description: Sampling and quantization, SQNR for uniform quantization, companding. Pulse code modulation — transmitter and receiver. DPCM transmitter and receiver. Delta modulation, slope overload, and line codes.

  - week: 5
    date: Aug 14
    topic: First Series Examination
    description: Written internal examination covering Modules 1 and 2.

  - week: 6
    date: Aug 20
    topic: Baseband Data Transmission
    description: Baseband transmission of digital data through an AWGN channel, mathematical model of ISI, Nyquist criterion for zero ISI, signal modelling for ISI, raised cosine spectrum, equalization, zero-forcing equalizer.

  - week: 7
    date: Aug 27
    topic: Signal Space Representation
    description: Geometric representation of signals — Gram-Schmidt procedure, signal space, vector model of the AWGN channel.

  - week: 8
    date: Sep 3
    topic: Optimum Receivers
    description: Matched filter and correlation receivers, MAP receiver, maximum likelihood receiver.

  - week: 9
    date: Sep 10
    topic: BPSK and QPSK
    description: Digital band-pass modulation schemes — BPSK system and signal constellation, BPSK transmitter and receiver. QPSK system and signal constellations, QPSK transmitter and receiver.

  - week: 10
    date: Sep 17
    topic: BER Analysis and QAM
    description: BER analysis of BPSK and QPSK in erfc, plots of BER vs SNR. Quadrature amplitude modulation and signal constellation.

  - week: 11
    date: Sep 24
    topic: Comprehensive Revision
    description: Consolidation across all four modules ahead of the second series examination.

  - week: 12
    date: Oct 9
    topic: Second Series Examination
    description: Written internal examination covering Modules 3 and 4.

  - week: 13
    date: Oct 12
    topic: Final Revision
    description: Final consolidation and doubt-clearing session across all four modules.
---

## Course Overview

Analog and Digital Communication (PCECT502) is a core fifth-semester course for the Electronics and Communication Engineering programme, analyzing analog and digital communication systems — from amplitude and angle modulation through to baseband and digital band-pass transmission.

**Course Outcomes**

- **CO1** — Illustrate the principles of analog communication systems.
- **CO2** — Explain the basic concepts of digital communication.
- **CO3** — Analyze the baseband transmission of digital data through an AWGN channel.
- **CO4** — Apply various digital modulation techniques in the design of digital communication systems.

## Course Project

Every team must complete a course project as the Assignment/Micro-project component of the CIE (15 marks) — a Python-based simulation of a communication system built on the concepts covered in class, with a written report and a final viva. Full guidelines, grading criteria, and the week-by-week plan are in the [Course Project Handbook]({{ '/assets/pdf/analog-digital-communication-project-handbook.pdf' | relative_url }}).

- **Teams**: groups of 3 (4 only with prior approval)
- **Abstract submission**: due August 17
- **Code repository**: each team's project must be uploaded to GitHub — uploading it into your individual GitHub account is mandatory

## Prerequisites

- PCECT402 Signals and Systems
- GBMAT401 Probability, Random Process and Numerical Methods

## Course Structure

- Teaching hours: 3 lecture + 1 tutorial hours/week
- Credits: 4
- Evaluation: 40 marks Continuous Internal Evaluation (CIE) + 60 marks End Semester Examination (ESE)

## Textbooks

- Simon Haykin and Michael Moher, *Communication Systems*, Wiley, 5th edition, 2020
- B. P. Lathi and Zhi Ding, *Modern Digital and Analog Communication Systems*, Oxford University Press, 5th edition, 2018
- Simon Haykin and Michael Moher, *Introduction to Analog and Digital Communication, An Indian Adaptation*, Wiley, 2nd edition, 2022

## Reference Books

- Herbert Taub and Donald L. Schilling, *Principles of Communication Systems*, McGraw-Hill Education, 4th edition, 2013
- John G. Proakis and Masoud Salehi, *Digital Communications*, McGraw-Hill Education, 6th edition, 2020
- John G. Proakis and Masoud Salehi, *Communication Systems Engineering*, Pearson, 2nd edition, 2001
- Simon Haykin, *Digital Communications Systems, An Indian Adaptation*, John Wiley & Sons, 4th edition, 2021
- George Kennedy, *Electronic Communication Systems*, McGraw Hill, 6th edition, 2017
- Wayne Stark, *Introduction to Digital Communications*, Cambridge University Press, 1st edition, 2023

## Video Lectures

- [Module 1](https://youtu.be/hTAlcrqjNps?si=okoRHdUegx9pbOz3)
- [Module 2](https://youtu.be/s_vmLqT_6NQ?si=MF2OW6AaICiYKTfj)

## Grading (CIE — 40 marks)

| Component | Marks |
|---|---|
| Attendance | 5 |
| Assignment / Microproject | 15 |
| Internal Examination 1 (written) | 10 |
| Internal Examination 2 (written) | 10 |
