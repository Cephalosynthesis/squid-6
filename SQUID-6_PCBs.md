---
layout: "page"
title: PCBs
permalink: /files/ece499_schematic/
---

If you would like [a more interactive look]({{ '/files/project_files' | relative_url }}) at our project schematics and board files.

# Upper PCB

{% include side_by_side_figure.html
   left_src="upper_pcb_bottom.jpg" 
   left_alt="Bottom face of the upper PCB."
   right_src="upper_pcb_top.jpg"
   right_alt="Top face of the lower PCB"
   caption="Left - Bottom face of the upper PCB complete with pick and placed components from JLC-PCB. Right - Top face of the upper PCB."
%}

The upper PCB is where most of the action is. It is home to the power, oscillators, filter, and delay circuits.

## Power 

Power is provided through a DC barrel jack, which is then fed into an integrated DC-DC converter. This provides +12V, -12V, and ground. The +/-12V are used for most of the op-amps in the circuit. The +12V rail also powers two Linear LDO Regulators, providing +5V and +3.3V. The +5V is used by the delay circuit as well as the keyboard, and the +3.3V is used as the digital supply.

## Oscillator Subcircuit 

The core sound generation of the synthesizer is done by a microcontroller, namely the [Raspberry Pi RP2350](https://www.raspberrypi.com/products/rp2350/). This MCU contains a floating point unit, flexible peripherals, and a built-in UF2 bootloader, making it a convenient choice for this application. To provide stereo audio output, the [TI PCM5100A](https://www.ti.com/product/PCM5100A), a cheap and high-fidelity audio DAC is used. The RP2350 only includes 4 analog input pins, so to expand this capability a set of analog multiplexers are used. These allow many more analog inputs to be connected. The subcircuit also includes a USB-C connector for uploading firmware.

## Filter Subcircuit 

{% include side_by_side_figure.html
   left_src="MS-20 Filter.svg" 
   left_alt="PCB Front"
   right_src="MS-20 Filter-HPLP Filter L.svg"
   right_alt="PCB Back"
   caption="Left - The schematic for a single (mono) delay circuit (hierarchical design means that the L and R channel can share the same subsheet). Right - The upper level delay schematic showing the L & R channels with their feedback loops connected through a DPDT switch."
%}


## Delay Subcircuit 

{% include side_by_side_figure.html
   left_src="mono_delay_schematic.svg" 
   left_alt="PCB Front"
   right_src="stereo_delay.svg"
   right_alt="PCB Back"
   caption="Left - The schematic for a single (mono) delay circuit (hierarchical design means that the L and R channel can share the same subsheet). Right - The upper level delay schematic showing the L & R channels with their feedback loops connected through a DPDT switch."
%}

The delay of the SQUID-6 is achieved in hardware using a chip called the PT2399. Originally designed in the late 1980ties by Princeton Technology Corp. for the commercial electronics industry the PT2399 found a second life among guitar pedal and synthesizer enthusiasts. 

The PT2399 can provide a delay between 38.5-342ms (it can be pushed beyond this if distortion isn't a problem for the application). Thanks to some on die opamps the PT2399 can be configured as either an echo or delay/surround effect without only a handful of passive components. With a little creativity it can also provide more effects such as chorus, flanger, and reverb although more than one PT2399 and additional oscillators might be necessary. If you would like to learn more about the PT2399 [Electrosmash](https://www.electrosmash.com/pt2399-analysis "Electrosmash") has an excellent write up on it.

For our purposed we opted for the echo topology with adjustable feedback that passes through a DPDT switch so the L and Right channel's feedback loops can be cross coupled.

# Lower PCB

The lower PCB provides connections for SQUID's 6 keys (and associated control pots), along with the modulation switch and BIG mod wheel. The keys are [membrane potentiometers](https://www.spectrasymbol.com/linear-position-sensors/soft-membrane-linear-pots-softpot), a proprietary invention by SpectraSymbol. Through a fairly simple analog circuit, they allow note on/off information as well as postiion sensing to be read for each key individually. This PCB also includes two analog multiplexers to allow the MCU to read each value from the keys, knobs, and switches.
