# Vortex Objective Radar Tracking and Circulation (VORTRAC)

The Vortex Objective Radar Tracking and Circulation software is a collection of radar algorithms designed to provide real-time or post-analysis information about hurricane location and structure from a single Doppler radar. These algorithms are written in C++ and combined with a graphical user interface (GUI) that allows the user to control the software operation and display critical storm parameters for use in an operational environment. The primary display shows a timeline of estimated central surface pressure and the radius of maximum wind (RMW) that updates as new radar volumes are processed. Additional information about the radar data and program operation is also displayed to the user, including a constant altitude plan-position indicator (CAPPI), maximum velocity, storm signal, status light, operation log, and progress bar. This development was funded under a grant from the NOAA Joint Hurricane Testbed program from 2005 – 2007.

## Configuration

### vortex
XML Label:		**name** (default: New Hurricane) 

Input: 		Vortex Name 

Description:		This parameter holds the name of the tropical cyclone that VORTRAC is tracking.  This parameter is used internally for labeling and also for labeling various output files.  

XML Label:		lat (default: 0 deg) 
Input: 		Vortex Latitude
Range: 		[-90, 90] deg
XML Label:		lon (default: 0 deg) 
Input: 		Vortex Longitude
Range: 		[-180, 180] deg
Description:		These parameters hold the first observation latitude and longitude of the tropical cyclone.  The latitude and longitude of the storm given here should correspond with the time shown in “Time of Above Observation” so that VORTRAC can accurately locate the tropical cyclone.  VORTRAC accepts latitude (longitude) in a decimal format where a negative value is in the Northern (Western) hemisphere and a positive value is in the Southern (Eastern) hemisphere.  Initializing the VORTRAC analysis with an accurate storm location and time is required for a successful run and the accuracy of these parameters affects VORTRAC's ability to follow the storm as it evolves. 

XML Label:		direction (default: 0 deg)
Input: 		Direction of Vortex Movement (Degrees clockwise from North)
Range: 		[0, 359.9] deg
XML Label:		speed (default: 0 m/s)
Input: 		Speed of Vortex Movement (Degrees clockwise from North)
Range: 		[0, 100] m/s
Description:		These parameters should hold the direction and speed of the initial storm movement.  These measurements should correspond with the time set in “Time of Above Observation” so that VORTRAC can accurately follow the tropical cyclone.  While these parameters are not required for a successful run, it is highly recommended that the user obtain this information about the storm.  These parameters are particularly useful when the initial observation (observation time, latitude and longitude on the VORTEX panel) is outside of the range of the Doppler radar.  When the initial observation is outside Doppler range VORTRAC will linearly interpolate the initial position based on direction of storm movement and storm speed until the circulation enters the Doppler range of the radar.

XML Label:		obsdate (default: current date UTC)
Input: 		Time of Above Observation
Range: 		Any Valid Date (format: YYYY-MM-DD)
XML Label:		obstime (default: current time UTC)
Input: 		Time of Above Observation
Range: 		Any Valid UTC Time (format: HH:MM:SS)
Description:		These parameters are used to set the time of the initial observation which is described by Vortex Latitude, Vortex Longitude, Vortex Speed and Vortex Direction parameters contained in this panel.  If this time of observation occurs before the starting time in RADAR CONFIGURATION PANEL, then VORTRAC will attempt to interpolate a starting location that is in the Doppler domain after the indicated initial time in the RADAR CONFIGURATION PANEL. 

XML Label:		dir (default: 'default' sets to current working directory at run time)
Input: 		Working Directory
Range:			Any directory where the user has permission to read and write files
Description:		This parameter holds the location of the working directory which will contain many of the products and temporary files that VORTRAC uses during a run.  When other directories in the configuration are left on the default setting they will default to subdirectories of this working directory.  It is recommended that the user not change the working directory once a run has begun processing because this can cause difficulties in locating data products and intermediates.  The working directory is also important when restarting an old run, since VORTRAC will search the working directory for traces of previous runs to restart.




## Running VORTRAC

1. Edit the xml file and configure the information.


2. To initiate a new run, execute VORTRAC using the following command:
```terminal
\path\to\vortrac
```
Click "File", and open the configured xml file. Then, the user can initiate the analysis with the "Run" button on the bottom right.

3. After VORTRAC finishes all the analysis, the program will generate four files: \\

- `TC_name`_`Radar_name`_`Year_of_the_TC`_coefficientlist.csv
- `TC_name`_`Radar_name`_`Year_of_the_TC`_simplexlist.xml
- `TC_name`_`Radar_name`_`Year_of_the_TC`_vortexlist.xml
- VORTRAC_status_`The_time_of_analysis`.log

`TC_name`, `Radar_name`, and `Year_of_the_TC` will be generated based on the configured xml file, and `The_time_of_analysis` depends on the time when the user initiates a new run.

4. Convert the retrieved coefficients into a netCDF file with the coefficintlist and log files by using the following command:
```terminal
\path\to\vo2nc -c `TC_name`_`Radar_name`_`Year_of_the_TC`_coefficientlist.csv -l VORTRAC_status_`The_time_of_analysis`.log
 -o output.nc
 ```
 

