# Vortex Objective Radar Tracking and Circulation (VORTRAC)

The Vortex Objective Radar Tracking and Circulation software is a collection of radar algorithms designed to provide real-time information about hurricane location and structure from a single Doppler radar. These algorithms are written in C++ and combined with a graphical user interface (GUI) that allows the user to control the software operation and display critical storm parameters for use in an operational environment. The primary display shows a timeline of estimated central surface pressure and the radius of maximum wind (RMW) that updates as new radar volumes are processed. Additional information about the radar data and program operation is also displayed to the user, including a constant altitude plan-position indicator (CAPPI), maximum velocity, storm signal, status light, operation log, and progress bar. This development was funded under a grant from the NOAA Joint Hurricane Testbed program from 2005 – 2007.

## Running VORTRAC

1. Edit the xml file and configure the information.


2. To initiate a new run, execute VORTRAC using the following command:
```terminal
\path\to\vortrac
```
Click "File", and open the configured xml file. Then, the user can initiate the analysis with the "Run" button on the bottom right.

3. After VORTRAC finishes all the analysis, the program will generate four files:
-`TC_name`_`Radar_name`_`Year_of_the_TC`_coefficientlist.csv
- `TC_name`_`Radar_name`_`Year_of_the_TC`_simplexlist.xml
- `TC_name`_`Radar_name`_`Year_of_the_TC`_vortexlist.xml
- VORTRAC_status_`The_time_of_analysis`.log

`TC_name`, `Radar_name`, and `Year_of_the_TC` will be generated based on the configured xml file, and `The_time_of_analysis` depends on the time when the user initiate a new run.

4. Convert the retrieved coefficients into a netCDF file with the coefficintlist and log files by using the following command:
```terminal
\path\to\vo2nc -c `TC_name`_`Radar_name`_`Year_of_the_TC`_coefficientlist.csv -l VORTRAC_status_`The_time_of_analysis`.log
 -o output.nc
 ```
 
