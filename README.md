# VFD-Controlled Induction Motor Simulation

## Overview

This project models a three-phase induction motor controlled by a variable frequency drive (VFD) using MATLAB, Simulink, and Simscape Electrical.

The system uses open-loop V/f control. The motor supply frequency is varied while the voltage command is scaled proportionally to control motor speed.

## System Architecture

Three-Phase AC Source  
→ Three-Phase Rectifier  
→ DC Link  
→ Average-Value Voltage Source Converter  
→ Three-Phase Induction Motor

Control path:

Frequency Reference  
→ V/f Gain  
→ Three-Phase Modulation Signal  
→ Converter

## Motor Configuration

- Rated voltage: 220 V phase-to-phase RMS
- Rated frequency: 60 Hz
- Number of poles: 4
- Synchronous speed at 60 Hz: 1800 RPM
- Motor connection: Wye

## V/f Control

The modulation magnitude is calculated using:

m = 0.015f

where:

- m = modulation magnitude
- f = commanded frequency in Hz

| Frequency | Modulation Magnitude |
|---:|---:|
| 20 Hz | 0.30 |
| 30 Hz | 0.45 |
| 40 Hz | 0.60 |
| 50 Hz | 0.75 |
| 60 Hz | 0.90 |

## Frequency Sweep Results

| Frequency | Theoretical Speed | Simulated Speed |
|---:|---:|---:|
| 20 Hz | 600 RPM | 599.8 RPM |
| 30 Hz | 900 RPM | 893 RPM |
| 40 Hz | 1200 RPM | 1198 RPM |
| 50 Hz | 1500 RPM | 1499 RPM |
| 60 Hz | 1800 RPM | 1811 RPM mean |

The simulated motor speed closely followed the theoretical synchronous-speed relationship.

## Load Response

A mechanical load step from 0 to -20 N·m was applied at 60 Hz.

- Speed before load: ~1820 RPM
- Final speed: ~1740 RPM
- RMS current before load: 27.26 A
- RMS current after load: 32.58 A
- Current increase: approximately 19.5%

The additional mechanical load caused motor speed to decrease while RMS current increased.

## Startup Comparison

### Immediate 60 Hz Start

- Peak RMS current: 108.6 A
- Time to approximately 1620 RPM: 0.07 s
- Peak speed: 1953 RPM
- Speed overshoot: approximately 8.5%

### 0-60 Hz VFD Ramp

- Peak RMS current: 30.08 A
- Time to approximately 1620 RPM: 0.916 s
- Peak speed: 1767 RPM
- Minimal speed overshoot

The ramped VFD startup reduced peak RMS current by approximately 72.3%.

## Frequency Step Response

A frequency command from 30 Hz to 60 Hz was applied at 0.5 s.

- Speed before change: ~901 RPM
- Peak speed: ~2070 RPM
- Final settled speed: ~1760-1770 RPM
- Approximate settling time: ~0.30 s
- RMS current before step: ~7.27 A
- Peak RMS current: ~93.23 A
- Final RMS current: ~15.13 A

## Key Findings

- Motor speed followed the commanded supply frequency closely.
- V/f control maintained proportional voltage and frequency commands.
- Increased mechanical load reduced motor speed and increased current.
- Ramped startup reduced peak RMS current by approximately 72%.
- Sudden frequency changes caused temporary current and speed transients.
- Open-loop V/f control provided effective speed control but showed transient overshoot and steady-state deviations.

## Software

- MATLAB
- Simulink
- Simscape Electrical
