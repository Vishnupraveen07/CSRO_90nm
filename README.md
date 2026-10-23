# Design and Simulation of a 90 nm PMOS Current-Starved Ring Oscillator

## Project Overview

This project focuses on the design and simulation of a **three-stage PMOS-source Current-Starved Ring Oscillator (CSRO)** using **90 nm CMOS technology** in Cadence Virtuoso.

The oscillator uses PMOS current-source transistors to control the charging current of inverter-based delay stages. The relationship between control voltage, oscillation frequency, and power consumption is investigated through transient simulation, frequency and power analysis, PVT analysis, and Monte Carlo analysis.

The project also includes physical layout design, DRC/LVS-related checks, parasitic extraction (PEX), and post-layout simulation.

## Objectives

- Design a three-stage PMOS-source current-starved ring oscillator using 90 nm CMOS technology.
- Verify oscillator startup and sustained periodic output using transient simulation.
- Measure the oscillation frequency.
- Analyze the effect of control voltage on frequency and average power consumption.
- Evaluate performance variations across process corners and temperatures.
- Perform Monte Carlo analysis to study the effects of random device variations.
- Design the physical layout and investigate post-layout performance.

## Design Specifications

| Parameter | Value |
|---|---|
| Circuit | Three-stage PMOS-source CSRO |
| Technology | 90 nm CMOS |
| Supply voltage (`VDD`) | 1.8 V |
| Nominal control voltage (`Vctrl`) | 1 V |
| Output node | `Vosc` |
| Simulation tool | Cadence Virtuoso |
| Simulation analyses | Transient, frequency, power, PVT, Monte Carlo |
| Physical design | Layout, DRC/LVS-related checks, PEX and post-layout simulation |

## Circuit Architecture

The current-starved ring oscillator consists of three inverter-based delay stages connected in a closed feedback loop.

Each basic delay cell contains:
- **Upper PMOS transistor:** Acts as the current-source/current-starving device. Its gate is controlled by `Vctrl`.
- **Middle PMOS transistor:** Forms part of the CMOS inverter.
- **Bottom NMOS transistor:** Forms the complementary part of the CMOS inverter.
- **Feedback connection:** Connects the output of the final stage back to the input of the first stage.

The PMOS current-source arrangement controls the current available to charge the internal nodes. Changing the control voltage changes the available current and the propagation delay of the stages, thereby changing the oscillation frequency.

## Working Principle

When the supply voltage is applied, a small initial disturbance causes the inverter stages to switch between logic HIGH and LOW states. The signal propagates through the three stages and returns through the feedback connection, producing continuous oscillation.

The approximate oscillation frequency is:

\[
f_{osc} \approx \frac{1}{2Nt_d}
\]

where:

- \(f_{osc}\) is the oscillation frequency.
- \(N\) is the number of delay stages.
- \(t_d\) is the average propagation delay of each stage.

For this design, \(N=3\).

The frequency can also be calculated from the measured output period:

\[
f_{osc}=\frac{1}{T}
\]

where \(T\) is the time period of one complete output cycle.

## Simulation Results

### 1. Startup and Transient Analysis

Transient simulation confirms that the designed three-stage oscillator produces a periodic output waveform.

During startup, the waveform begins from an initial condition and subsequently settles into a more consistent periodic oscillation.

The nominal simulation uses:

- Supply voltage: `VDD = 1.8 V`
- Control voltage: `Vctrl = 1 V`
- Output node: `Vosc`

### 2. Frequency Measurement

The nominal pre-layout frequency was measured using the output waveform in Cadence Virtuoso.

| Parameter | Reported result |
|---|---:|
| Supply voltage | 1.8 V |
| Control voltage | 1 V |
| Pre-layout frequency | Approximately 8.076 GHz |
| Measured period in the manual calculation | Approximately 0.124 ns |
| Calculated frequency from the rounded period | Approximately 8.065 GHz |

The report records a nominal pre-layout frequency of approximately **8.076 GHz**.

### 3. Frequency and Power Analysis

A parametric analysis was performed by varying `Vctrl` from 0 V to 1 V while maintaining `VDD = 1.8 V`.

The reported results show that increasing the control voltage increases the oscillation frequency and average power consumption.

At `Vctrl = 1 V`, the reported results are:

| Parameter | Result |
|---|---:|
| Oscillation frequency | Approximately 8.1 GHz |
| Average power consumption | Approximately 260 µW |

This demonstrates the relationship between operating frequency and power consumption in the implemented oscillator.

### 4. PVT Analysis

Process–Voltage–Temperature (PVT) analysis was performed to investigate the effects of process corners and temperature variations on oscillator performance.

**Process corners:**

- `FF` — Fast NMOS, Fast PMOS
- `FS` — Fast NMOS, Slow PMOS
- `NN` — Nominal NMOS, Nominal PMOS
- `SF` — Slow NMOS, Fast PMOS
- `SS` — Slow NMOS, Slow PMOS

**Temperature conditions:**

- −40 °C
- 27 °C
- 125 °C

**Control-voltage conditions:**

- 0.5 V
- 0.625 V
- 0.75 V
- 0.875 V
- 1 V

The report gives the following overall results across the investigated PVT conditions:

| Parameter | Reported result |
|---|---:|
| Minimum frequency | Approximately 1.238 GHz |
| Maximum frequency | Approximately 13.87 GHz |
| Minimum power | Approximately 19.24 µW |
| Maximum power | Approximately 469.9 µW |
| Temperature range | −40 °C to 125 °C |

The results show that process and temperature variations affect the oscillation frequency and power consumption.

### 5. Monte Carlo Analysis

Monte Carlo analysis was performed using **200 simulation samples** at two control-voltage conditions: `Vctrl = 1 V` and `Vctrl = 0.1 V`.

#### Results at Vctrl = 1 V

| Parameter | Result |
|---|---:|
| Number of samples | 200 |
| Reported yield | 100% |
| Mean frequency | 7.96888 GHz |
| Frequency standard deviation | 636.128 MHz |
| Minimum frequency | 6.528 GHz |
| Maximum frequency | 9.715 GHz |
| Mean power | 261.445 µW |
| Power standard deviation | 28.6619 µW |
| Minimum power | 199.8 µW |
| Maximum power | 338.7 µW |

#### Results at Vctrl = 0.1 V

| Parameter | Result |
|---|---:|
| Number of samples | 200 |
| Reported yield | 100% |
| Mean frequency | 420.938 MHz |
| Frequency standard deviation | 132.900 MHz |
| Minimum frequency | 154.8 MHz |
| Maximum frequency | 903.7 MHz |
| Mean power | 3.49059 µW |
| Power standard deviation | 1.28092 µW |
| Minimum power | 1.062 µW |
| Maximum power | 8.839 µW |

The reported Monte Carlo results show that reducing the control voltage significantly reduces the mean oscillation frequency and power consumption. The reported 100% yield means that all 200 simulated samples produced valid results under the selected simulation conditions.

### 6. Layout and Post-Layout Simulation

The project report includes physical layout design, DRC/LVS-related checks, parasitic extraction (PEX), and post-layout simulation.

The reported frequency comparison is:

| Simulation | Frequency |
|---|---:|
| Pre-layout simulation | Approximately 8.076 GHz |
| Post-layout simulation | Approximately 8.088 GHz |

The post-layout simulation was performed using the extracted `av_extracted` view at `VDD = 1.8 V` and `Vctrl = 1 V`.

The reported results show a small difference between the pre-layout and post-layout oscillation frequencies under these simulation conditions.

## Repository Structure

The repository contains a `CSRO_PVG/` directory with Cadence-related project files and supporting directories.

The following structure is based on the repository contents visible in GitHub:

```text
CSRO_90nm/
├── .gitattributes
├── README.md
└── CSRO_PVG/
    ├── .cadence/
    ├── .csro/
    ├── .tmp_vlsilab/
    ├── csro.lvsdb/
    ├── csro/
    ├── logs_vlsilab/
    │   └── logs0/
    ├── .QRC.run
    ├── .assuraLastRun
    ├── .assuraUI.prf
    ├── .assura_DRC.run
    ├── .assura_LVS.run
    ├── .assura_tech.save
    ├── .assura_vlw.state
    ├── .cds_assuraui
    ├── .drc.Last.state
    ├── .lvs.Last.state
    ├── .qrc.Last.state
    └── cds.lib
```

**Note:** This is a partial representation of the repository. Additional files and subdirectories may exist inside `CSRO_PVG/`. The listed names identify files and folders visible in the repository screenshot; their individual contents and verification status are not described here.

## Software and Technology

- **Cadence Virtuoso:** Schematic design, simulation, layout, and extracted-view analysis.
- **90 nm CMOS technology:** Technology used for the oscillator design and simulations.
- **ADE Explorer / ADE Assembler:** Simulation environments identified in the project report.

Reproducing the simulations requires access to the relevant Cadence environment, technology files, transistor models, and design data.

## Conclusion

The project demonstrates the design and simulation of a three-stage 90 nm PMOS-source current-starved ring oscillator using Cadence Virtuoso.

The reported simulations demonstrate sustained oscillation, control-voltage-dependent frequency and power behavior, performance variations across PVT conditions, and statistical variation analysis using Monte Carlo simulation.

The report also documents layout design, DRC/LVS-related checks, parasitic extraction, and post-layout simulation. The nominal pre-layout and post-layout frequencies are approximately 8.076 GHz and 8.088 GHz, respectively.

## Author

**Vishnu Praveen P**

**GitHub Repository:** [CSRO_90nm](https://github.com/Vishnupraveen07/CSRO_90nm)
