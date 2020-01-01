# Precision FDM
Forget using any kind of whole system calibration that depends on taking measurements from a printed part and using a spreadsheet & statistics to get steps/mm and/or CTE values because there are simply too many unknown variables. 
The best way to calibrate is to break it down into direct measurements and minimise the number of unknowns.

### Summary of variables calibrated in this guide
#### Per printer
* [X steps-per-mm](#xyz-stepsmm)
* [Y steps-per-mm](#xyz-stepsmm)
* [Z steps-per-mm](#xyz-stepsmm)
* [E steps-per-mm](#extruder-stepsmm)

#### Per filament
* Nominal filament diameter(#nominal-diameter)
* Extrusion flow(#extrusion-flow)
* Coefficient of thermal expansion (CTE)

## Required items
* Digital vernier caliper
  * Good: 150mm digital vernier caliper (Any cheap brand)
  * Best: 300mm digital vernier caliper (Mitutoyo 500-173)
* Digital micrometer
  * Good: 0-25mm [0-1"] (Any cheap brand)
  * Best: 0-25mm [0-1"] (Mitutoyo)
* Fine permanent marker (Staedtler S)
* Good quality PLA filament


## New Printer
### XYZ steps/mm 
#### Procedure
Using a digital vernier caliper, mount it to the printer in a way that means movements on the axis of interest pushes the caliper head. Start from a zero position, zero the caliper, and send the g-code command to move a good amount (100mm) then take a reading from the caliper. Repeat this 3 times and calculate an average. Use this value to calculate new steps-per-mm.

#### Example
```
Expected reading = 100.00mm
Averaged actual reading = 98.60mm
Printer steps-per-mm on axis = 80

Expected/Averaged actual = Scale
100.00/98.60 = 1.01419878296146

Printer current steps-per-mm * Scale = New steps-per-mm
80 * 1.01419878296146 = 81.136
```

#### Saving value to printer

(Substitute 'X' for whatever axis you desire such as Y/Z/E)
```
M92 X81.136
M500
M501
```
`M501` will show you that the value has been committed.

### Extruder steps/mm
#### Procedure

Ensure extruder tension is low so that there aren't huge tooth marks on the filament.

Remove bowden tube from extruder and ensure there's an approx. 25mm tail of filament sticking out. 

Make a mark on the filament with the permanent marker right at the point where it comes out the bowden fitting. 

Send the g-code command to move a good amount (150mm for small caliper, 300mm for large caliper). 

Make another mark on the filament, extrude 25mm and cut it off. 

Measure distance between markings with vernier and use measurement to calculate new steps-per-mm.

#### Example
````
TBD
````

#### Saving value to printer
```
M92 E390
M500
M501
```
`M501` will show you that the value has been committed.

## New Filament

### Nominal diameter

Check the nominal diameter using the digital micrometer. You're looking for a tight spread of values around 1.75mm (or 3.00mm). If values are wildly varying, return filament for refund.

### Extrusion Flow

#### Assumptions
Printer has 0.4mm nozzle.

#### Procedure
Use the single wall box test at the recommended temps for the filament. Ensure the slicer has 1 wall with a width of 0.5mm, and 2 base layers. Take a series of wall thickness measurements with the digital micrometer and compute an average. Use this value to calculate the filament specific flow rate.

![Single wall box sliced in Cura](/image/Single%20wall%20box%20sliced.png?raw=true)

![Single wall box printed in Anycubic Mega-S](/image/Single%20wall%20box%20printed.jpg?raw=true)

#### Example
````
Expected wall thickness = 0.500mm
Average wall thickness = 0.537mm

(Expected/Averaged actual)*100 = Flow rate %
(0.500/0.537)*100 = 93.1%
````

