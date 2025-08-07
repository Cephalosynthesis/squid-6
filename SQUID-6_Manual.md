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

The sound of the six oscillators are controlled by three knobs: `TIMBRE` offset, `WAVE`, and `TIMBRE` skew (the small knob with the arrow pointing to timbre). The underlying synthesis algorithm that these parameters control could be modified, but as it stands right now they control a simple analog-style oscillator.

### Timbre

Timbre is a parameter that can be modified on a per-note basis. Each of the six voices can have their own timbre parameter. This is controlled using the two knobs, `TIMBRE` offset (the large knob) and `TIMBRE` skew (the small knob). Offset changes the timbre value for each voice simultaneously, while skew affects how different the timbre value for one oscillator is to the next. 

With skew centered, Each voice has the same timbre value. As skew is turned up past 12 o'clock, higher voices on the keyboard get higher and higher timbre values. At maximum, the highest note will have double the timbre of the lowest note. As the knob is turned counterclockwise, this is reversed, so that lower notes have higher timbre values.

The currently implemented synth algorithm has timbre controlled the angle of the waveform. With timbre all the way down, the wave is a simple triangle wave. As timbre is increased, the peak of the triangle wave moves later and later in it's cycle, until at maximum timbre the wave is a sawtooth. This can be heard audibly as an increase in harmonics as timbre is turned up.

Timbre can also be modified using the `MOD.DEST` switch. In the top position, the position of each finger up the key also adds to the timbre value of the corresponding voice.

### Wave

Wave is a parameter that each oscillator shares, unlike timbre. In the case of the current synth algorithm, it mixes in a square wave one octave below the fundamental of it's associated voice (often called a 'sub'), adding depth to the tone.

## Mixer

The mixer on this synthesizer is somewhat unconventional. Instead of representing the mixing of various sound sources in each individual oscillator, it contains parameters describing the way in which each of the six voices are mixed together. It has two parameters: `COLOUR` and `SPREAD`.

### Spread

`SPREAD` affects where each oscillator is placed in the stereo field. With the control centered, each voice is panned to the middle, creating a mono signal. When it is turned up past 12 o'clock, the lower voices are panned left and the upper voices and panned right. At it's maximum, the leftmost key will be heard only in the left ear, and the rightmost only in the right.

### Colour

After the effect of the `SPREAD` knob is applied, a saturator is applied to the signal. Note that this is a stereo saturator, so it is applied to the left and right channel independantly.

A saturator has the effect of smoothing out the tops of waveforms, effectively squashing them down. This is known as a 'nonlinear' effect, because when sounds are combined before being passed through a nonlinear effect, it has different results than if each one was individually affected before being combined. This can be heard on the synth, when playing two or more notes with `COLOUR` turned up. You may notice tones in the audio that were not present when you played any of the notes individually.

This has the effect of distorting and 'warming' the sound somewhat, and interacts well with the filter and delay.

## Stereo Filter

The filter section immediately follows the audio output of the microcontroller. It is two identical two-pole lowpass/highpass filters, one on the left and one on the right channel. The filter topology is based on the Korg MS-20 filter, as described by Rene Schmitz [here](https://www.schmitzbits.de/ms20.html).

### Cutoff

`CUTOFF` is the master frequency control, modifying the cutoff frequency of both filters together. In lowpass mode, turning the knob up lets in higher and higher frequencies, making the sound louder.

### LP/HP Switch

The switch next to the master cutoff knob controls the topology of the filter. In the bottom position, it is a lowpass filter, letting through every frequency below the cutoff. In the top position, it is a highpass filter, only letting in frequencies above the cutoff.

### Q

`Q.LEFT` and `Q.RIGHT` control the resonance for each side independently. This emphasizes the tone at the cutoff frequency. At high levels, the filter can self-oscillate, generating a tone even when no input audio is played. __Patch Tip__: setting the filter to self-oscillate and then turning the cutoff knob will create wide-band sine wave sweeps, which in combination with the delay can create some very interesting tones.

### Envelope Amount

`ENV. AMOUNT` controls how much the envelope signals affect the cutoff frequency. When turned all the way down, the envelope has no effect on the filter. As it is turned up, the envelope pushes the cutoff frequency more and more. Because there are six independant envelopes, the filter is affected by their maximum.

### Spacing

`SPACING` seperates the cutoff frequencies of the left and right channels. Turning it past 12 o'clock increases the right side cutoff while decreasing the left side, and turning it counterclockwise does the opposite. When centered, the left and right side have the same cutoff frequency. __Patch Tip__: this is a very fun knob to turn while sustaining a note!

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
