# Organizational Model of a Casa della Comunità (Community Health House)

**University Exam:** Healthcare Organizational Models
**Type:** Team project

## Overview

This project presents a discrete-event simulation model, developed in Simul8, of a Casa della Comunità (Community Health House) operating in District 28 of the Naples municipality (ASL Napoli 1 Centro). The model was designed in line with Ministerial Decree (DM) 77/2022 and the objectives of Italy's National Recovery and Resilience Plan (PNRR – Mission 6, Component M6C1: "Reti di prossimità, strutture e telemedicina"), which aim to strengthen local, community-based healthcare and reduce inappropriate hospital access.

The main goal of the simulation is to estimate patient waiting times across the three access pathways to the facility, providing a realistic performance benchmark for a structure that is still in the planning phase.

## Background

A Casa della Comunità is a single, accessible point of reference for citizens, where physicians, nurses, social workers, and other healthcare professionals collaborate on personalized care, with a focus on prevention and continuity of care.
Under DM 77/2022, each Hub-type facility serves 40,000–50,000 residents, staffed with 30–35 GPs, 7–11 Family/Community Nurses, and a PUA active 6 days a week. ASL Napoli 1 Centro is implementing 33 such facilities, funded with over €62 million from the PNRR.

## Model Structure

The simulated facility can be accessed through three pathways:
1. **PUA** – processing of a PDTA (Individual Care Plan), average duration 35 minutes
2. **CUP** – booking of a healthcare service, average duration 10 minutes
3. **Accettazione (check-in)** – for patients who already hold a booking, average duration 10 minutes, across 6 check-in desks, before being routed to the relevant outpatient clinic

The model covers 26 outpatient specialties (e.g. cardiology, dermatology, gynecology, ophthalmology, orthopedics, psychiatry, radiology, general surgery, etc.), each with its own service-time distribution, and uses real service-volume data for District 28 (52,710 annual outpatient services, patient inter-arrival time of 1.05 minutes). Access is split 60% check-in, 30% CUP, 10% PUA. Operating hours follow DM 77 standards (outpatient clinics 8:00–16:00 Mon–Fri; check-in/CUP/PUA 8:00–14:00, with PUA also open Saturdays).

## Methodology

- **Simulation:** patient flows and service pathways were modeled as a discrete-event simulation in Simul8, using real service-volume and timing data for District 28.
- **AI-assisted benchmarking:** prompt engineering was used to independently estimate the same waiting-time indicators from the underlying process description and data, as a comparison baseline for the simulation output.
- **Statistical validation (R):**
  - Normality of the simulated waiting-time distributions (booking, PUA, check-in) was tested using the **Anderson-Darling test** — all three distributions were found to be non-normal (p < 2.2e-16).
  - Given the non-normality, a **One Sample Wilcoxon signed-rank test** was used to compare the simulated median waiting times against the AI-estimated reference values. In all three cases (booking, PUA, check-in) the test did not reject the null hypothesis (p > 0.05), indicating no statistically significant difference between the simulated and estimated medians.

## Key Results

| Waiting time (median) | Value |
|---|---|
| Booking → service delivery | ~15 days |
| PDTA (PUA) | ~13 days |
| Check-in (accettazione) | ~3 hours |

## Tools

- **Simul8** – discrete-event simulation of healthcare processes
- **R** (ggplot2, Anderson-Darling test, Wilcoxon signed-rank test) – statistical validation of simulation results

## Repository Contents

- `Casa della Comunità.S8` – Simul8 model file
- `Presentazione Casa della Comunità.pdf` – slide deck explaining the model, methodology, and results

## Future Developments

- Detailed analysis of home-care (ADI) and continuity-of-care processes
- Detailed analysis of internal workflows within each outpatient clinic
- Validation against real-world data and/or stakeholder-provided data
