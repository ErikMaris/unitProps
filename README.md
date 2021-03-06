# unitProps

A MATLAB class for unit storage and conversion.

## Requirements
Please check 'requirements.txt' for the software's dependencies.

## Installation
1. Download the software by clicking the dropdown menu 'Code' and click 'Download ZIP'.
2. Unpack the zip file and move the folder to your desired location.
3. Go to 'requirements.txt' and move the dependencies, if any, to the folder unitProps/bin/external
4. Open MATLAB and add the folder ("Add with subfolders") to your MATLAB path.

![image](https://user-images.githubusercontent.com/77492856/119955717-99be7300-bfa0-11eb-8c8a-0a6765b572dc.png)

The software is now ready to use.

## Usage

The unitProps class is meant as a superclass that provides functionality for unit conversion. Declare unitProps as a superclass
```
classdef myClass < unitProps
```
. The code can also be used stand-alone and works the same:
```
up = unitProps();
```
. We can check the current base units, which we call the unit system
```
up.unitSystem
```
and find that by default the SI unit system ([kg], [s], [m], [A], [cd], [mol], [K]) is used. The unit system is the set units to which the input units are converted, for instance when plotting data. Let's perform a conversion from the raw data to our unitSystem. The raw measurement data was stored in nanoseconds 'ns' (for shorthand see https://nl.mathworks.com/help/symbolic/units-list.html) thus we set the unit of measurement_time to nanoseconds
```
up = up.setUnit('time','ns');
```
. Now we can get a conversion factor to convert our raw measurement times to SI units 'SI_time'
```
[cF,uF] = up.getUnitFactor('time');
measurement_time = 5; % ns
SI_time = measurement_time * cF;
disp(uF)
fprintf('Raw measurement data %1.1e ns; converted measurement data %1.1e m.\n',measurement_time,SI_time)
```
where cF is the conversion factor and uF the unit of the unit system of this unit. Mathematical operations can be parsed for more complex units, for instance 'time^2/distance'. Let's change the system's unit for time from seconds to nanoseconds
```
up = up.subsUnitSystem('s','ns');
[cF,uF] = up.getUnitFactor('time');
measurement_time = 5; % ns
SI_time = measurement_time * cF;
disp(uF)
```
. Now the conversion factor is 1 because the unit system matches the measurement unit. Go back to SI units:
```
up = up.resetUnitSystem;
```
.

## Documentation

Type
```
doc unitProps
```
for the documentation or
```
help unitProps.subsUnitSystem
```
for the documentation of a specific function, which is the 'subsUnitSystem' function in this example.

## Project organization
- PG = project-generated
- HW = human-writable
- RO = read only
```
.
????????? .gitignore
????????? CITATION.md
????????? LICENSE.md
????????? README.md
????????? requirements.txt
????????? bin                <- Compiled and external code, ignored by git (PG)
???   ????????? external       <- Any external source code, ignored by git (RO)
????????? config             <- Configuration files (HW)
????????? data               <- All project data, ignored by git
???   ????????? processed      <- The final, canonical data sets for modeling. (PG)
???   ????????? raw            <- The original, immutable data dump. (RO)
???   ????????? temp           <- Intermediate data that has been transformed. (PG)
????????? docs               <- Documentation notebook for users (HW)
???   ????????? manuscript     <- Manuscript source, e.g., LaTeX, Markdown, etc. (HW)
??????? ????????? reports        <- Other project reports and notebooks (e.g. Jupyter, .Rmd) (HW)
????????? results
???   ????????? figures        <- Figures for the manuscript or reports (PG)
??????? ????????? output         <- Other output for the manuscript or reports (PG)
????????? src                <- Source code for this project (HW)

```


## License

This project is licensed under the terms of the [GPL-3.0 License](/LICENSE.md).
