# Vortex Objective Radar Tracking and Circulation (VORTRAC)

The Vortex Objective Radar Tracking and Circulation software is a collection of radar algorithms designed to provide real-time or post-analysis information about hurricane location and structure from a single Doppler radar. These algorithms are written in C++ and combined with a graphical user interface (GUI) that allows the user to control the software operation and display critical storm parameters for use in an operational environment. The primary display shows a timeline of estimated central surface pressure and the radius of maximum wind (RMW) that updates as new radar volumes are processed. Additional information about the radar data and program operation is also displayed to the user, including a constant altitude plan-position indicator (CAPPI), maximum velocity, storm signal, status light, operation log, and progress bar. This development was funded under a grant from the NOAA Joint Hurricane Testbed program from 2005 – 2007.

## Configuration

### vortex
XML Label:		**name** (default: New Hurricane) 

- Input: 		Vortex Name 

- Description:		This parameter holds the name of the tropical cyclone that VORTRAC is tracking.  This parameter is used internally for labeling and also for labeling various output files.  

XML Label:		**lat** (default: 0 deg) 

- Input: 		Vortex Latitude

- Range: 		[-90, 90] deg

XML Label:		**lon** (default: 0 deg) 

- Input: 		Vortex Longitude

- Range: 		[-180, 180] deg

- Description:		These parameters hold the first observation latitude and longitude of the tropical cyclone.  The latitude and longitude of the storm given here should correspond with the time shown in “Time of Above Observation” so that VORTRAC can accurately locate the tropical cyclone.  VORTRAC accepts latitude (longitude) in a decimal format where a negative value is in the Northern (Western) hemisphere and a positive value is in the Southern (Eastern) hemisphere.  Initializing the VORTRAC analysis with an accurate storm location and time is required for a successful run and the accuracy of these parameters affects VORTRAC's ability to follow the storm as it evolves. 

XML Label:		**direction** (default: 0 deg)

- Input: 		Direction of Vortex Movement (Degrees clockwise from North)
- Range: 		[0, 359.9] deg

XML Label:		**speed** (default: 0 m/s)

- Input: 		Speed of Vortex Movement (Degrees clockwise from North)
- Range: 		[0, 100] m/s
- Description:		These parameters should hold the direction and speed of the initial storm movement.  These measurements should correspond with the time set in “Time of Above Observation” so that VORTRAC can accurately follow the tropical cyclone.  While these parameters are not required for a successful run, it is highly recommended that the user obtain this information about the storm.  These parameters are particularly useful when the initial observation (observation time, latitude and longitude on the VORTEX panel) is outside of the range of the Doppler radar.  When the initial observation is outside Doppler range VORTRAC will linearly interpolate the initial position based on direction of storm movement and storm speed until the circulation enters the Doppler range of the radar.

XML Label:		**obsdate** (default: current date UTC)

- Input: 		Time of Above Observation
- Range: 		Any Valid Date (format: YYYY-MM-DD)

XML Label:		**obstime** (default: current time UTC)

- Input: 		Time of Above Observation
- Range: 		Any Valid UTC Time (format: HH:MM:SS)
- Description:		These parameters are used to set the time of the initial observation which is described by Vortex Latitude, Vortex Longitude, Vortex Speed and Vortex Direction parameters contained in this panel.  If this time of observation occurs before the starting time in RADAR CONFIGURATION PANEL, then VORTRAC will attempt to interpolate a starting location that is in the Doppler domain after the indicated initial time in the RADAR CONFIGURATION PANEL. 

XML Label:		**dir** (default: 'default' sets to current working directory at run time)
- Input: 		Working Directory
- Range:			Any directory where the user has permission to read and write files
- Description:		This parameter holds the location of the working directory which will contain many of the products and temporary files that VORTRAC uses during a run.  When other directories in the configuration are left on the default setting they will default to subdirectories of this working directory.  It is recommended that the user not change the working directory once a run has begun processing because this can cause difficulties in locating data products and intermediates.  The working directory is also important when restarting an old run, since VORTRAC will search the working directory for traces of previous runs to restart.

XML Label:		**centers** (optional)
- Input: 		Center file directory
- Range:			Any directory where the user has permission to read and write files
- Description:		This parameter should hold the name of the directory that contains the centers information that VORTRAC can use it as a first guess to perform the simplex algorithm or as a final center to perform the GBVTD/GVTD algorithm. It is optional to include the center file.

### radar
XML Label:		**name** (default: WSR-88D)
- Input: 		Radar Name
- Range: 		Any four letters (preferably radar call letters)
- Description:		This parameter is intended to hold the radar call letters for WRS-88D radar that is being used to observe the storm.  The drop down box in the RADAR CONFIGURATION PANEL can be used to select from several existing radars near the Atlantic and Gulf coasts.  Additionally the user may choose to add new radars to this list by clicking 'Other Radar ...' and entering or editing parameters as necessary.  The radar call letters entered here are used for identifying radar volume data, in addition to internal labeling and naming data products, so entering these correctly is highly recommended.  

XML Label:		**lat** (default: 0 deg)
- Input: 		Radar Latitude (deg)
- Range: 		[-90, 90] decimal degrees

XML Label:		**lon** (default: 0 deg)
- Input: 		Radar Longitude (deg)
- Range: 		[-180, 180] decimal degrees

XML Label:		**alt** (default: 0 m)
- Panel Label: 		Radar Altitude (meters)
- Range: 		[-999, 999] m
- Description:		These three parameters describe the location of the radar in latitude, longitude and altitude.  They will be automatically set when a radar is selected from the radar name drop box.  These can be manually adjusted in the panel or in the radar list dialog which can be accessed by choosing 'Other Radar ...' in the Radar Name drop box.  These three parameters are all required to successfully run VORTRAC.

XML Label:		dir (default: 'default')
- Input: 		Radar Data Directory
- Range: 		Any existing directory where the user has read permissions
- Description:		This parameter should hold the name of the directory that contains the level II radar data from the radar specified in this panel.  The level II data in this directory should be the same format as that selected in the format drop box on this panel.  Additionally, the level II data should be named in the following format: `KXXXyyyyMMdd_hhmmss`

where KXXX is the station call letters specified in the radar name parameter.  The call letters are followed by the UTC time stamp of the volume in above format.  This parameter will default to the working directory if no other directory is given.

XML Label:		**format** (default: LEVELII)
- Input: 		Data Format
- Range: 		[LDMLEVELII, NCDCLEVELII,NETCDF]
- Description:		This parameter is used to select the radar data format of the files contained in the directory specified in dir.  These formats are explained in greater detail in Sec 1A.  This is a required parameter, selecting a format that doesn't correspond with the files located in the Radar Data Directory will cause VORTRAC to run improperly.

XML Label:		**startdate** (default: current date UTC, format: YYYY-MM-DD)

XML Label:		**starttime** (default: current time UTC, format: HH:MM:SS)

- Input: 		Start Date and Time
- Range: 		Any valid date and time
- Description:		These date and time parameters indicate the earliest time stamp that a volume of level II radar data may have in order to be processed by VORTRAC.  This parameter is intended to help the user control which volumes are read in by VORTRAC for each analysis.

XML Label:		**enddate** (default: current date UTC + 3 days, format: YYYY-MM-DD)

XML Label:		**endtime** (default: current time UTC, format: HH:MM:SS)
- Panel Label: 		End Date and Time
- Range: 		Any valid date and time
- Description:		These date and time parameters indicate the latest time stamp that a volume of level II radar data may have in order to be processed by VORTRAC.  This parameter is intended to help the user control which volumes are read in by VORTRAC for each analysis.


### cappi

XML Label:		**dir** (default: default)
- Input: 		CAPPI Output Directory
Range: 		Any directory where the user has read and write permission
Description:		This directory will be used to store CAPPI output files in the .asi format.  More information on the .asi format can be found in Sec 1A.  When the xml parameter dir is set to 'default' this directory will default to subdirectory of the working directory selected in the VORTEX CONFIGURATION PANEL.  If such a subdirectory does not exist, one will be created.  The user can also choose to adjust this directory independent of the main working directory.

XML Label:		**xdim** (default: 150)
- Input: 		Grid Dimension in X Direction 
- Range: 		[0, 256]

XML Label:		**ydim** (default: 150)
- Input: 		Grid Dimension in Y Direction
- Range: 		[0, 256]

XML Label:		**zdim** (default: 3)
- Input: 		Grid Dimension in Z Direction
- Range: 		[0, 20]
- Description:		These three parameters allow the user to adjust the size of the CAPPI used in the analysis.  The default dimensions are intended to meet the needs of the 'average' circulation, but these parameters can be adjusted to meet specific needs.  Larger grids provide more data for analysis, but they also increase processing times considerably.

XML Label:		**xgridsp** (default: 1.0 km)
- Input: 		X Grid Spacing (km)

XML Label:		**ygridsp** (default: 1.0)
- Input: 		Y Grid Spacing (km)

XML Label:		**zgridsp** (default: 1.0)
- Input: 		Z Grid Spacing (km)
- Description:		These values control the grid spacing of the CAPPI.  Currently these value are fixed at 1 km, but VORTRAC's functionality may be expanded later to allow adjustments in these parameters.

XML Label:		**interpolation** (default: cressman)
- Input: 		Interpolation
- Range: 		[cressman]
- Description:		This parameter contains the interpolation method used for mapping data from the level II radar volume to the CAPPI for further processing.  Currently Cressman interpolation is the only option for interpolating.

### center

XML Label:		**dir** (default: 'default')
- Input: 		Center Output Directory
- Range: 		Any directory where the user has read and write permission
- Description:		This parameter stores the directory where the results of each simplex search will be stored.  These files are intermediates which are only valuable to the advanced user, but if they are discarded the user will be unable to restart the VORTRAC run.  A list of these files are stored in the working directory (file ending in simplexList.xml).  This directory will default to use or create a center subdirectory in the working directory if its value is not altered.

XML Label:		**skipsimplex** (default: false)
- Input: 		skip the simplex to find the center
- Range: 		[false,true]
- Description:		This parameter determines whether to perform the center finding algorithm for the VORTRAC analysis. The user can put predetermined centers into a file (in the vortex section) and use them for the VORTRAC analysis.

XML Label:		**geometry** (default: GBVTD)
- Input: 		Geometry
- Range: 		[GBVTD,GVTD]
- Description:		This parameter holds the geometry for the VORTRAC analysis.  Currently only the GBVTD geometry is implemented so this parameter should not be changed.

XML Label:		**closure** (default: original)
- Input: 		Closure				
- Range: 		[original]
- Description:		This parameter holds the closure assumption to be used in the VORTRAC analysis.  Currently only the original closure assumption is available for use.  This closure assumption is used in the simplex search for the vorticity center.  For more about closure assumptions see Sec. 3A Algorithm Overview.

XML Label:		**reflectivity** (default: DZ)
- Input: 		Reflectivity
- Range: 		[DZ]
- Description:		This parameter holds the letters that identify the reflectivity data within the radar volumes.  There is currently only one option for this parameter but it may be expanded later to suit user needs.

XML Label:		**velocity** (default: VE)
- Input: 		Velocity
- Range: 		[VE]
- Description:		This parameter holds the letters that identify the velocity data within the radar volumes.  There is currently only one option for this parameter but it may be expanded later to suit user needs.

XML Label:		**bottomlevel** (default: 1 km)
- Input: 		Bottom Level (km)
- Range: 		[1, 5] km

XML Label:		**toplevel** (default: 3)
- Input: 		Top Level (km)
- Range: 		[2, 20] (km)
- Description:		These two parameters control which height range within the CAPPI is used in the SIMPLEX search algorithms.  The user can adjust these parameters, but the total number of levels used cannot exceed 20 due to memory constraints.  Examining a greater number of levels may provide greater accuracy, but at the cost of computation time.  The default values for these parameters should be appropriate for most cases.  The user should also be cautioned that trying to examine levels outside of those contained in the CAPPI could yield undesirable results due to absent data.

XML Label:		**innerradius** (default: 10)
- Input: 		Inner Radius (km)
- Range: 		[1, 120]
XML Label:		**outerradius** (default: 35)
- Input: 		Outer Radius (km)
- Range: 		[2, 150]
- Description:		These two parameters control the range that the SIMPLEX algorithm searches for a circulations radius of maximum wind.  These parameters should be adjusted based on outside information on the approximate radius of the tropical cyclone.  If a cyclone's RMW is not enclosed in this range SIMPLEX is unlikely to accurately locate a center.  These are required parameters, they should also be adjusted if the storm changes size during the analysis.  The SIMPLEX radius search range is displayed on the CAPPI DISPLAY once VORTRAC has completely processed a volume.  This visual display should help the user locate the best radius range for subsequent simplex searches.

XML Label:		**ringwidth** (default: 1.0 km)
- Input: 		Width of Search Rings (km)	
- Range: 		[0.01, 10.00] km
- Description:		This parameter controls the width of the search ring for each radius search preformed by the SIMPLEX algorithm.  This parameter does not change the ring spacing (SIMLEX will search in 1 km increments between the Inner Radius and the Outer Radius).  This parameter controls the thickness of the annuli of data points from the CAPPI that are used for each search.  It may be useful to increase this value when data in the region of interest is very sparse.  However, increasing this value significantly may cause greater uncertainty in the radius of maximum wind.

XML Label:		**search** (default: MAXVT0)
- Input: 		Center Finding Criteria 
- Range: 		[MAXVT0]
- Description:		This parameter contains the criteria that simplex searches for when attempting to locate the tropical cyclone center.  Currently the only available option is MAXVT0.  This selection indicates that the SIMPLEX search will attempt to locate the tropical cyclone based on the greatest primary circulation wind that it can locate during its search.

XML Label:		**influenceradius** (default: 4.0)
- Input: 		Radius of Influence (km)
- Range: 		[2, 10] km
- Description:		This parameter controls the initial spacing of points in the SIMPLEX search algorithm.  While this parameter can be adjusted to begin searching smaller or greater areas based on user needs, it is recommended that this parameter only be adjusted by advanced users.

XML Label:		**convergence** (default: 0.05)
- Input: 		Convergence Requirements
- Range: 		[0.001, 2.000]
- Description:		This parameter controls the extent of the convergence of centers required by the SIMPLEX algorithm for agreement between separate searches.  While this parameter can be adjusted to require more or less convergence based on user needs, it is recommended that this parameter only be adjusted by advanced users.

XML Label:		**maxiterations** (default: 60)
- Input: 		Maximum Iterations for Process
- Range: 		[10, 100]
- Description:		This parameter sets the maximum number of iterations possible within a SIMPLEX search.  Increasing this parameter may increase computation time.  It is recommended that this parameter only be adjusted by advanced users.

XML Label:		**boxdiameter** (default: 12.0 km)
- Input: 		Width of Search Zone (km)
- Range: 		[9, 25]
XML Label:		**numpoints** (default: 16)
- Input: 		Number of Center Points
- Range: 		[1, 25]
- Description:		These two parameters control the distribution of initial SIMPLEX searches that are independently run to locate the circulation center.  The Width of Search Zone parameter controls the width of the initial range where SIMPLEX searches are started.  The Number of Center Points parameter controls the number of starting points distributed within this box.  It is recommended that these parameters only be changed by advanced users, the defaults should perform well for most cases.

XML Label:		**maxwavenum** (default: 1)
- Input: 		Maximum Wave Number
- Range: 		[0, no maximum limit]

XML Label:		**maxdatagap** (default: 0 deg)   
- Input: 		Wave # 
- Range: 		[0, 359] deg
- Description:		These parameters control how much data can be missing within a ring of analysis at each wave number.  The Maximum Wave Number controls the order of the Fourier fit used to calculate the winds at each ring.  The SIMPLEX CONFIGURATION PANEL will hold multiple Wave # boxes corresponding to the value assigned maxwavenum. The maximum data gap for each wave number should be assigned based on an understanding of how missing data affects the quality of the fit.  The defaults should work well form most cases.




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
 

