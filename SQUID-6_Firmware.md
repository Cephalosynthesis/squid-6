---
layout: "page"
title: Firmware
---

# General Structure

The RP2350 is a dual core ARM-M33 microcontroller, and both of these cores are made use of in the firmware for this project. Core 0 (UI) is responsible for input handling, including reading data from the ADCs and processing it into usable values. Core 1 (DSP) is responsible for sound generation, and is passed all the necessary information from the UI core.

## UI Core

The UI core runs a loop at a rate of 1 kHz, in which it reads all values, and then processes them. The values it must read are the positions of all knobs, switches, and keys. This is done by selecting them through the multiplexers, and then reading their values using the ADC. The ADC has 12 bits of precision, but there can be a large amount of noise associated with these values. To increase the stability of read values, readings are decimated by removing the least significant four bits.

Processing is done differently for the various controls. Some of the controls can be simply passed to the DSP core without modification, like the Wave, Spread, and Colour controls. Others must be processed more in depth. For example, the Timbre control includes both offset and skew, so these values must be combined to provide the correct value for each oscillator.

The most complex of these processing steps is the handling of the envelopes. Each key can trigger a unique ADSR envelope, which is implemented using a large state machine.

## DSP Core

The DSP core generates 6 oscillators, and then performs additional processing to combine them. It runs a loop at a rate of 6 kHz, generate a batch of 8 samples each loop. Therefore, the audio is output at 48 kHz. The oscillators are generated using a technique called Direct Digital Synthesis (DDS), and use Polynomial Band-Limited Steps (PolyBLEP) for antialiasing. The Timbre and Wave controls each affect the sound of the oscillators. Wave is a global control, while timbre can be changed per-oscillator. To combine them, the oscillators are mixed in the stereo field according to the setting of the Spread control, and passed through a simple saturator based on the setting of the Colour control.