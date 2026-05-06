+++
title = "3D Printers: A Gentle Introduction"
date = 2023-08-07
description = "A beginner's guide to FDM 3D printing from someone who has been doing it since 2018."
[taxonomies]
tags = ["3d-printing", "hardware", "guide"]
+++

I've been 3D printing since 2018. This isn't meant to be comprehensive documentation—just a starting point for people who are curious and don't know where to begin.

## How 3D Printers Work

This guide focuses on FDM (Fused Deposition Modeling) printers, which are by far the most common type. The process is simple: the printer lays down one thin layer of plastic on the print surface, moves up a tiny bit, lays down another thin layer, moves up again, and repeats until the object is done.

A PCB follows instructions in a `.gcode` file, which contains atomic commands for motor movement, temperature control, and filament extrusion. That's really all there is to it.

## What You Need

- A 3D printer
- Filament
- An SD card with adapter
- A computer with slicer software
- A 3D model file (typically `.STL` format)

For models, check out Printables, Thingiverse, and Thangs.

## Slicers

A slicer converts your 3D model into `.gcode` instructions the printer can follow. I recommend:

- **Prusa Slicer** if you have a Prusa printer
- **UltiMaker Cura** for everything else

Cura is the better choice for beginners—it has a friendlier interface and good defaults.

## Materials

**PLA** is the right choice when you're starting out. It's easy to print, requires lower temperatures, is pretty durable, and is cheap. Optimal settings: 210°C nozzle, 60°C build plate.

**PETG** is more heat-resistant but trickier. It needs 240°C nozzle and 80°C build plate. Important: **do not use bare smooth surfaces for PETG**—it adheres too well and can damage your build plate.

**ABS** has been historically popular but is genuinely difficult to print. Skip it until you're comfortable with the basics.

## Key Slicer Settings

- **Nozzle Diameter:** Standard is 0.4mm. Smaller = more detail, slower. Larger = faster, less detail.
- **Layer Height:** Typically half the nozzle diameter. Thinner layers = better surface quality.
- **Infill:** 20% is usually enough. Going higher wastes material without much benefit for most prints.
- **Support:** Generates temporary structures for overhanging features. Remove after printing.

## Things That Actually Matter

**Clean your build surface.** A dirty build surface is the most common cause of failed prints, full stop. Isopropyl alcohol or warm soapy water removes the oils from your hands that prevent adhesion.

**Level your bed.** This ensures consistent first-layer adhesion across the whole surface. Some printers do this automatically; others require manual adjustment. Either way, don't skip it.

**Calibrate your Z-height.** The first layer needs to be close enough to the bed to stick, but not so close that you're gouging the surface.

---

If you have questions, feel free to reach out. 3D printing has a learning curve but it flattens out quickly once you've done a few prints.
