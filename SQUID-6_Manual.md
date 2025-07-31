---
layout: "page"
title: Manual
---

# General Description

SQUID-6 is a stereo hybrid 6-voice synthesizer designed by Cephalosynthesis. There are 6 main sections:
1. Keyboard
2. Envelopes
3. Sound Source
4. Mixer
5. Stereo Filter
6. Stereo Delay

## Keyboard

The keyboard consists of 6 keys, their pitch control knobs, three switches, and the Swell control. 

### Keys
Each key corresponds to one of the oscillators in the synthesizer, and its envelope is triggered by pressing the key. Additionally, the position of the press along the key is used as an expression control, who's destination can be changed using the MOD.DEST switch.

### Pitch Control
The pitch of each oscillator can be changed using the knob positioned directly above the key. The knob covers a two octave range, and each key's range is offset a major third higher than the key to its left. This control can be either unquantized, or snapped to the nearest semitone, as controlled by the QUANTIZE switch.

### Quantize Switch
The QUANTIZE switch changes the behaviour of the pitch control knobs from unquantized (any pitch playable) to snapped to the nearest semitone.

### Octave Switch
The OCTAVE switch has three positions, allowing the range of the pitch control knobs to be transposed two octaves up or down.

### Modulation Destination Switch
The MOD.DEST switch has three positions, each corresponding to a different setting of modulation destinations. There are two modulation sources: the Swell knob and the key position expression controls. The Swell knob is a global control, while expression from the key positions affect only their corresponding oscillator. 

`vol` controls the volume, either of a specific oscillator or all of the oscillators. 

`noi` mixes in white noise to the audio path, allowing interesting tones when combined with the filter and delay.

`timb` affects the Timbre control of a given oscillator.

`len` affects the envelope length of a given oscillator. This effectively turns the Attack, Decay, and Release knobs up for that specific oscillator, but leaves the Sustain control unchanged.

## Envelopes

{% include figure_image.html
fig_class="centered_figure"
max-width="600px"
file="ADSR.png"
alt="Diagram illustrating an (A)ttack (D)ecay (S)ustain (R)elease Envelope."
caption=""
%}

The envelope of a note or sound is it's volume profile. An envelope generator creates and controls that volume profile of a note and may consist of up to four stages:
- `ATTACK`
- `DECAY`
- `SUSTAIN`
- `RELEASE`

{% include figure_image.html
fig_class="centered_figure"
max-width="600px"
file="panel_adsr_crop.jpg"
alt="Close up of SQUID-6 envelope generator control knobs."
caption=""
%}

The SQUID-6's envelope generator has control knobs for all four plus `ENV. AMOUNT` which controls the overall length of the note. 

## Sound Source

## Mixer

## Stereo Filter

## Stereo Delay
