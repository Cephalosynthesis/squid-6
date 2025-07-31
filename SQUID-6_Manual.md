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

{% include figure_image.html
fig_class="centered_figure"
max-width="600px"
file="keyboard.jpg"
alt="Up close photograph of the SQUID-6 keyboard."
caption=""
%}


The keyboard consists of 6 keys, their pitch control knobs, three switches, and the Swell control. 

### Keys
Each key corresponds to one of the oscillators in the synthesizer, and its envelope is triggered by pressing the key. Additionally, the position of the press along the key is used as an expression control, who's destination can be changed using the MOD.DEST switch.

### Pitch Control

{% include figure_image.html
fig_class="centered_figure"
max-width="600px"
file="pitch-control-knobs.jpg"
alt="Close up of the SQID-6 per-key pitch control knobs."
caption=""
%}

The `PITCH` of each oscillator can be changed using the knob positioned directly above the key. The knob covers a two octave range, and each key's range is offset a major third higher than the key to its left. This control can be either unquantized, or snapped to the nearest semitone, as controlled by the QUANTIZE switch.

### Quantize Switch 

{% include image_wrap.html
class="small_images"
height="120px"
width="120px"
file="quantize-switch_short.jpg"
alt="Up close picture of the quantize switch."
%} 

`QUANTIZE` switch changes the behaviour of the pitch control knobs from unquantized (any pitch playable) to snapped to the nearest semitone.  

<br></br><br>

### Octave Switch

{% include image_wrap.html
class="small_images"
height="130px"
width="120px"
file="octave-switch.jpg"
alt="Up close image of octave switch."
%} 

The `OCTAVE` switch has three positions, allowing the range of the pitch control knobs to be transposed two octaves up or down.

<br></br><br><br>

### Modulation Destination Switch

{% include image_wrap.html
class="small_images"
height="140px"
width="120px"
file="mod-dest-switch.jpg"
alt="Up close image of the modulation destination switch."
%} 

The `MOD.DEST` switch has three positions, each corresponding to a different setting of modulation destinations. There are two modulation sources: the Swell knob and the key position expression controls. The Swell knob is a global control, while expression from the key positions affect only their corresponding oscillator.

<br></br>

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
caption="If you're curious about the algorithm used by the SQUID-6 to generate the curve shapes for envelope generator this <a href=\"https://dsp.stackexchange.com/a/94617\">StackExchange</a> post inspired our approach. The post also provides a helpful desmos graph (which was also used as the base for this figure) that illustrates how the equation work. Some additional finesse was necessary to make the equation suitable for use in a real-time embedded system."
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

{% include figure_image.html
fig_class="centered_figure"
max-width="600px"
file="sound_source.jpg"
alt="Up close photograph of the SQUID-6 keyboard."
caption=""
%}


## Mixer

## Stereo Filter

## Stereo Delay

{% include figure_image.html
fig_class="centered_figure"
max-width="300px"
file="delay-section.jpg"
alt="Up close photograph of the SQUID-6 keyboard."
caption=""
%}


### Feedback

{% include figure_image.html
fig_class="centered_figure"
max-width="300px"
file="fb-knob.jpg"
alt="Up close photograph of the SQUID-6 keyboard."
caption=""
%}

Each stereo channel has it's own feedback control knob. This lets the user set the amount of echo.

### Mix

{% include image_wrap.html
class="small_images"
height="130px"
width="120px"
file="delay-mix-knob.jpg"
alt="Up close image of the modulation destination switch."
%} 

The delay section's `MIX` knobs controls the relative mix of the undelayed signal (dry) coming from the filter section and the delayed signal (wet) created.

<br><br><br><br>

### Spacing

{% include image_wrap.html
class="small_images"
height="160px"
width="120px"
file="delay-spacing-knob.jpg"
alt="Up close image of the delay section's spacing control knob."
%} 

The delay section's `SPACING` knob control's the amount of delay applied to the left and right channel relative to one another. The knob snaps to the middle position via detent - this is the neutral poisiton where the left and right channel experience the same amount of delay.

<br><br><br><br><br>

### Ping-Pong Switch

{% include image_wrap.html
class="small_images"
height="160px"
width="120px"
file="delay-ping-pong-switch.jpg"
alt="Up close image of the delay section's spacing control knob."
%} 

The feedback loop of each channel's delay effect passes through the `PING-PONG` switch which is named as such because in the bottom position the two feedback loops get swapped. This has the effect of causing a note to get bounced back and forth between the left and right channels.

<br><br><br>

### Time 

{% include image_wrap.html
class="small_images"
height="280px"
width="240px"
file="delay-time-knob.jpg"
alt="Up close image of the delay section's spacing control knob."
%} 

The big `TIME` knob controls the amount of global delay applied to both the left and right channel.
