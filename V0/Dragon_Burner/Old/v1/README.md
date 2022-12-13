# Dragon Burner
This is my take on the Voron V0.1 toolhead. I wanted to improve the cooling of the Dragon HF hotend and provide improved part cooling when printing filament that needs it (e.g. PLA).

It uses the standard Voron X carriage, is based on the [Mini-AfterSherpa](https://github.com/KurioHonoo/Mini-AfterSherpa) and uses its extruder mounting system, but I've designed it from the ground up using TinkerCad :man_facepalming:

![Dragon Burner](images/Dragon_Burner.jpg)

## Goals:

- Dragon SF and HF hotend support
- Dragonfly hotend support
- E3D Revo Voron hotend support
- Rapido HF hotend support
- Single 3010 24v hotend cooling fan
- Twin 4010 24v blower part cooling fans
- [SlideSwipe magnetic probe](https://github.com/chestwood96/SlideSwipe) support
- [(Un)Klicky Probe](https://github.com/jlas1/Klicky-Probe) support
- [ZeroClick probe] (https://github.com/zruncho3d/ZeroClick) support
- ADXL345 mount point and board mount
- Heatsink thermistor support
- Screwless hotend fan attachment

These have all been implemented in this public release.

## Printing:

- Use the Voron defaults and print in ABS or better. The part is orientated correctly in the STL.
- Print the appropriate cowl from the Toolheads directory
- Print the FanDuct_Left.stl and the appropriate FanDuct_Right_*.stl depending on whether you use a probe 

## BOM:

In addition to the [Mini-AfterSherpa](https://github.com/KurioHonoo/Mini-AfterSherpa):

- 2x M3x6mm SHCS/BHCS (for fan duct mounts)
- 4x M3 5x4mm additional heat inserts (2 for ADXL345 mount, 2 for fan duct mounts)
- 2x M3x16mm BHCS (optional: for hotend fan)
- 2x M3x8mm BHCS (for ADXL mount)[*]
- 2x M2x10mm self tapping screws (for blower fans)
- 2x M2x8mm BHCS and nuts (to mount ADXL)
- 2x 4010 blower fans (24v recommended)
- 1x 3010 hotend fan (24v recommended)

The cowl supports a no probe setup, [SlideSwipe magnetic probe](https://github.com/chestwood96/SlideSwipe), [(Un)Klicky Probe](https://github.com/jlas1/Klicky-Probe) and [ZeroClick probe](https://github.com/zruncho3d/ZeroClick)

## Fans:

I am using these fans:

- 24v Axial 3010: [Gdstime](https://www.aliexpress.com/item/1005002857100082.html)
- 24v Blower 4010: [Gdstime](https://www.aliexpress.com/item/32799324058.html)

## Heatsink Thermistor:

Each cowl includes a hole at the top to insert a thermistor. With this in place, klipper can track the temperature of the heatsink to watch for heat creep from the heatbreak. You can have klipper abort and shutdown before your whole toolhead melts! You only need a simple klipper entry for the appropriate pin on your MCU, e.g.:

```
[temperature_sensor Heatsink]
sensor_type: Generic 3950
sensor_pin: expander:PA5
max_temp: 85
```

Klipper will shutdown if the top of the heatsink hits 85C. You can use thermal paste to help keep a bulb thermistor in contact with the heatsink and layed the wires through the provided groove, then fitted the extruder on top to hold it in place.

## Assembly:

- Add fan duct inserts to the cowl being careful not to push them all the way through. They should fit level on both surfaces with the standard M3 5x4mm inserts
- Attach the fan ducts to the cowl using 2x M3x6mm. SHCS preferred for a low profile
- Remove the small duct overhang supports
- If you are using one of the Klicky variants, add the wires and magnets to the fan duct
- Add ADXL mount inserts to the lower outside left of the toolhead
- There is a hole on the left face to put the left 4010 blower fan cable through, do this before going further
- Insert the 3010 hotend fan and route both fan cables through the provided channel
- Secure the 3010 fan either using the fan nubs[*], or use 2 FHCS (the fan will need to be chamfered) or BHCS screws
- Take care when screwing the hotend fan as it's secured into plastic and too much force will strip the created threads and/or deform the fan
- Be careful not to leave the cables loose or over the hotend mount
- Insert the 4010 fans into each side and slide backwards into the restraints
- Secure each fan using a M2x10mm self tapping screw at the bottom front hole
- Carefully mount the hotend into place making sure not to pinch any fan cables
- Run the hotend and fan cables along the 10mm side of the 4010 fans on each side and zip tie at the top
- Fit the heatbreak thermistor if you are going to use one
- Fit your extruder
- Offer up to the toolhead mount and secure, being careful not to trap any of the cables
- Check the X and Y movement still triggers the end-stops and that none of the cables are causing the belts to bind to the x axis
- Check you have modified all the fan connections on the MCU if you have switched to higher voltage fans

[*] NOTE: You may lose 1-2mm on the Y axis when using BHCS screws. To reclaim most of that loss, instead use the fan nubs. These are inserted after placing the 3010 fan into the housing from the sides with the domes pointing inwards. The 4010 fans will then hold these in place. If you need to remove the 3010 fan, remove the 4010 fans first, then carefully screw in a short M3 screw into the holes in the centre of the nubs to extract. If either the 3010 fan does not have indents or if it rattles, then you will have to use 2 screws instead to secure the fan. You can use BHCS screws, or to regain some of the Y loss, use FHCS screws. You can then chamfer the insides of the top two fan screw holes to allow the FHCS screws to be flush against the fan and cowl.

## Changelog:

- 2022-04-12 First release
- 2022-04-12 Fixed issue with incorrect part placement
- 2022-04-13 Added mounts for the Dragonfly hotend
- 2022-04-13 Added mounts for the Rapido HF hotend
- 2022-04-13 Fixed clearance to socks on Rapido and Dragonfly
- 2022-04-16 Fixed misalignment of filament tube hole for Dragonfly
- 2022-04-16 New ducts improve airflow over nozzle
- 2022-04-19 New ducts improve airflow direction
- 2022-04-19 Added hole and wire groove for heatsink thermistor
- 2022-04-21 Added Klicky variant support
- 2022-04-21 Reorganised repo to separate hotends
- 2022-04-21 Added screwless 3010 hotend fan mount
- 2022-04-27 Added mounts for the E3D Revo Voron hotend
- 2022-05-07 Added wire exit for Klicky mount for all hotends
- 2022-05-08 Modified all toolheads to use removeable fan ducts
- 2022-05-10 Links to public Tinkercad added
- 2022-05-11 Updated Klicky fan ducts
- 2022-05-21 Added bridging supports to Klicky fan ducts
- 2022-06-03 Added ZeroClick variant support
- 2022-06-05 Easier to print fan ducts and magnet helper for ZeroClick
