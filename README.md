# SPICE Electronics Lab

An electronics bench in a single web page. Draw a circuit, drive it with a signal generator, probe any
node voltage or part current on an oscilloscope, and read or write SPICE netlists.

**Live demo:** <https://jurgenkobierczynski.com/SPICE_Electronics_Lab/SPICE_Electronics_Lab.html>

## Screenshot

![SPICE Electronics Lab](SPICE_Electronics_Lab.jpg)

The Bode view, showing the gain and phase of a common-emitter amplifier:

![Bode view](SPICE_Electronics_Lab_Bode.jpg)

There is nothing to install or build. Open `SPICE_Electronics_Lab.html` in a browser, or put the file on
any web server. Everything runs in the browser; no data leaves the page.

## What it does

**Schematic editor**

- Parts: resistor, capacitor, inductor, voltage and current sources, switch, diode, zener, LED, NPN and
  PNP transistors, N and P channel MOSFETs, op-amp, voltage-controlled voltage and current sources,
  ground and net labels.
- Place parts from the rack, drag from a pin to wire, drag parts to move them (wires follow), rotate,
  mirror, duplicate, undo and redo. Pan by dragging the sheet, zoom with the wheel.
- Values accept engineering notation: `4.7k`, `100n`, `2.2u`, `1M`, `1meg`.
- Themes: follows the system light or dark setting, or pick Lab Light, Lab Dark, Solarized Light,
  Solarized Dark, Nord, Catppuccin Latte or Catppuccin Mocha. The choice is remembered in the browser.

**Signal generator**

Every source can be DC, sine, square (block), triangle (zigzag), sawtooth, pulse, exponential, AM, FM,
noise or a piecewise-linear shape typed in as time/value points. A small preview shows the waveform
over the simulated time span.

**Oscilloscope**

- Probe tool: click a wire or pin for that node's voltage, click a part for the current through it.
  On a transistor, click near the pin whose current you want. "Voltage across" gives the difference
  between the two pins of a part, and "Power" gives voltage across times current.
- Math traces combine existing traces: difference, sum, product, ratio, derivative and integral.
- Four views of the same probes:
  - **Time:** voltages on the left axis, currents on the right, or one lane per trace. Per trace: value
    at the pointer, minimum, maximum, peak-to-peak, mean, RMS and frequency, measured over the time
    shown on screen. Two cursors give time and value differences. Scroll to zoom, drag to pan.
  - **Spectrum:** the FFT of the time span on screen, in decibels or linear amplitude, on a linear or
    logarithmic frequency axis. Per trace: DC level, fundamental frequency and amplitude, total
    harmonic distortion, and the 2nd and 3rd harmonics.
  - **X-Y:** every trace plotted against a chosen X trace, for device curves, hysteresis loops and
    Lissajous figures.
  - **Bode:** gain in decibels and phase against frequency, from an AC sweep of one source. Per trace:
    low-frequency gain, peak gain and its frequency, and the -3 dB points.

**SPICE import and export**

- Export writes a standard netlist. The drawing is stored in comment lines starting with `*@`, which
  other simulators ignore, so an exported file comes back exactly as drawn.
- Import reads R, C, L, V, I, D, Q, M, E, G and X elements, `.model`, `.subckt` (expanded), `.param`
  with plain numbers, `.tran`, `.ac`, and the sources DC, SIN, PULSE, PWL, EXP, SFFM and AM with an
  optional AC value. A netlist without
  layout comments is drawn as a ladder: one vertical rail per node, parts in a column beside it.
- Elements that are not supported (coupled inductors, transmission lines, behavioural sources,
  current-controlled sources) are skipped and listed after import.
- Square, triangle and sawtooth are written as PULSE, noise as PWL, and the op-amp as a small
  subcircuit of standard parts. In SPICE files `M` means milli and `MEG` means mega; the lab reads and
  writes files that way, while its own value fields treat a capital `M` as mega.

## Example labs

The Example menu holds 87 ready-made circuits, each with probes already placed and the scope set to
the view that shows the point:

- **First steps:** RC low-pass filter; Voltage divider; RC high-pass (differentiator); RL circuit: current build-up; Superposition of two sources.
- **Bode plots:** Bode plot: twin-T notch filter; Bode plot: two-way loudspeaker crossover; Bode plot: op-amp band-pass filter; Bode plot: three RC sections; Bode plot: compensated 10× probe divider; Bode plot: RC low-pass; Bode plot: RC high-pass; Bode plot: RLC band-pass; Bode plot: LC filter with a resonance peak; Bode plot: impedance of a series RLC; Bode plot: Sallen-Key low-pass; Bode plot: op-amp integrator; Bode plot: op-amp gain and bandwidth; Bode plot: common-emitter amplifier; Bode plot: gain between two nodes (ratio trace).
- **Spectrum:** Spectrum: mixing two tones in a diode; Spectrum: harmonics of a square wave; Spectrum: sine, square, triangle and sawtooth; Spectrum: AM carrier and sidebands; Spectrum: FM sidebands; Spectrum: two close tones; Spectrum: diode clipper distortion; Spectrum: half-wave rectifier; Spectrum: crossover distortion; Spectrum: op-amp clipping; Spectrum: noise before and after a filter; Spectrum: PWM before and after the LC filter.
- **X-Y plots:** X-Y: transistor output curve; X-Y: MOSFET transfer curve; X-Y: zener diode curve; X-Y: diode characteristic curve; X-Y: Schmitt trigger hysteresis; X-Y: Lissajous figure; X-Y: phase shift as an ellipse; X-Y: CMOS inverter transfer curve; X-Y: amplifier clipping; X-Y: crossover distortion.
- **Power and math:** Power in a resistor and a capacitor; Power: real and reactive power in an RL circuit; Power: buck converter input and output; Power: dissipation in a switching MOSFET; Math trace: charge from current; Math trace: energy stored in a capacitor; Math trace: slope of a capacitor voltage; Math trace: differential output.
- **Signals:** Signal shapes: sine, square, triangle, sawtooth; Signal shapes: pulse, exponential, FM, noise; Beats from two close frequencies; Ideal amplifier from a controlled source.
- **Resonance and filters:** Series RLC step response; LC tank ringing down; RLC band-pass with a frequency sweep; Noise through a low-pass filter; PWM smoothed by an LC filter; Sallen-Key low-pass filter.
- **Diodes:** Bridge rectifier with smoothing; AM envelope detector; Half-wave rectifier; Zener voltage regulator; Diode clipper; Diode clamper (DC restorer); Voltage doubler; LED and series resistor.
- **Transistors:** Common-emitter amplifier; Emitter follower; Transistor switch driving an LED; Current mirror; Differential pair; Push-pull output stage (crossover distortion); Astable multivibrator; CMOS inverter.
- **Op-amps:** Op-amp inverting amplifier; Op-amp relaxation oscillator; Op-amp non-inverting amplifier; Op-amp summing amplifier (mixer); Op-amp integrator; Schmitt trigger; Precision rectifier; Wien bridge oscillator.
- **Power and switching:** MOSFET switch with inductive load; Buck converter (step-down); Boost converter (step-up).

Every example is an ordinary circuit: edit it, re-probe it, or export it as a netlist.

## Keyboard

| Key | Action |
| --- | --- |
| `W` | Wire tool |
| `P` | Probe tool |
| `Esc` | Back to select, end a wire |
| `R` | Rotate the selection or the part being placed |
| `X`, `Y` | Mirror horizontally, vertically |
| `Del` | Delete the selection |
| `Ctrl`+`D` | Duplicate |
| `Ctrl`+`Z`, `Ctrl`+`Y` | Undo, redo |
| `Ctrl`+`A` | Select all |
| `Shift`+drag | Select an area; `Shift`+click places several parts in a row |

## How it simulates

Transient analysis by modified nodal analysis: a DC operating point (Newton iteration, with gmin
stepping, source stepping and a settle-from-zero fallback), then time steps with the trapezoidal rule
or Backward Euler and Newton iteration at every step. Steps land on the corners of every source
waveform. Fast positive-feedback switching (Schmitt triggers, multivibrators, latches) is detected and
followed with extra small steps.

AC analysis for the Bode view linearises the circuit at its operating point, with every source resting
at its offset, and solves the complex equations at 40 frequencies per decade. Exported netlists carry
the matching `.ac` line and `DC` and `AC` values on the sources.

Device models:

- Diode: Shockley equation with reverse breakdown and a constant junction capacitance.
- Bipolar transistor: Ebers-Moll transport model with constant junction capacitances.
- MOSFET: level 1 square law with channel-length modulation and constant gate capacitances; the bulk
  is tied to the source.
- Op-amp: finite gain, one pole set by the gain-bandwidth product, output held between two limits.

## Limits

- Transient and AC analysis only. No DC sweep, parameter sweep or noise analysis.
- The Bode view is small-signal: clipping, switching and other large-signal effects do not show in it.
- The spectrum is computed from the simulated points, so the solver's own error sets its noise floor
  (typically 60 to 80 dB below the signal). More points lower it.
- The semiconductor models leave out series resistance, charge storage, the Early effect and
  temperature. The part presets (1N4148, 2N3904, 2N7000 and others) use typical published parameter
  values and are not manufacturer models.
- The time step is fixed by the number of points, refined only where the solver needs it. There is no
  error-controlled step size as in a full SPICE.
- Results agree with analytic solutions for RC, RLC and LC circuits. The exported netlists have not
  yet been cross-checked by running them in ngspice or LTspice.
- The AM source exists in ngspice but not in LTspice.

## Relation to SPICE

This is an independent implementation written from the published methods. It contains no code from
Berkeley SPICE, ngspice or any other simulator; it only reads and writes the SPICE netlist format.

The page loads the Barlow and IBM Plex Mono typefaces from Google Fonts when online and falls back to
system fonts otherwise.

## Licence

Copyright (C) 2026 Jurgen Kobierczynski

This program is free software: you can redistribute it and/or modify it under the terms of the GNU
General Public License as published by the Free Software Foundation, version 3. It is distributed in
the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See [LICENSE](LICENSE) for the full text.

## Attribution

Designed and written with Claude Opus 5.5 Medium (Anthropic), directed by Jurgen Kobierczynski.
