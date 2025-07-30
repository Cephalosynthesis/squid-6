---
layout: "page"
title: Project Schematics & Board Files
kicanvas: true
exclude: true
---

This interactive viewer for kiCAD files is a neat project called [KiCanvas](https://kicanvas.org/) created by Thea Flowers.

>Tip KiCanvas does require Javascript and as a result may not work in all browsers.

>Note The board files presented below are our first revision of the SQUID-6 and are not without errors. Unfortunately the team has not yet had time to make the updates for revision 2.

{% include kicanvas-multi-embed.html
   project="ece499_project.kicad_prj"    files="ece499_project.kicad_sch,delay_stereo.kicad_sch,mcu_controls.kicad_sch,ms20.kicad_sch,HPLP_filter.kicad_sch,delay_mono.kicad_sch"
   board="ece499_project.kicad_pcb"
   controls="full"
%}
