# Fast Reorder and CEDRIC Technique in LROSE (FRACTL) 

FRACTL is a fast traditional solver with integrated interpolation using LROSE infrastructure, and it is able to perform both gridding and multi-Doppler synthesis for airborne radars and multiple ground-based radars, which is different than Radx2Grid whereas it only has the capability for gridding of a single ground-based radar data. FRACTL adopts both REORDER and CEDRIC programs which REORDER is a program that transforms radar data from its native coordinate system to cartesian space and the data can then be ingested into CEDRIC for synthesis.

## Running FRACTL

The main features of using FRACTL are:
- "Traditional" multi-Doppler solver written from the ground up in C++
- Quasi-horizontal 2-radar assumption (U,V) with mass-continuity for W, or full 3D solution (U, V, W)
- Nearest neighbor algorithm adds Doppler gates directly to matrix solver at each grid point, no interpolation or averaging of velocity required
- Solve normal equations using Singular Value Decomposition (preferred) or Cramer’s method
- Subset of CEDRIC diagnostics implemented, more on the way
- Fast computation. It takes less than 5 minutes for dual-Doppler synthesis (~3M gates)
- Doppler data only

To check all command line options for FRACTL, including debugging options and file paths, the typical '-h' flag can be invoked:

```terminal
lrose -- fractl -h
```

Likewise, to obtain the default parameter file, use the following command:

```terminal
lrose -- fractl -print_params > fractl.params
```

There are several key parameters to look for and modify and they are listed below. After modifying the parameter file to your desired output analysis, type the following command to the terminal to invoke the program:

```terminal
lrose -- fractl -params fractl.params
```

* Note: FRACTL accepts the file format either with CfRadial or DORADE currently. Different than Radx2Grid, FRACTL doesn't require the CfRadial file with an aggregation of the sweeps. 


## The FRACTL parameter file
To control FRACTL's operation, there are several key parameters to be modified in order to obtain the desired output. 

- minDbz: any values below the minimum reflectivity will be tossed out.
- minNcp: any values below the minimum NCP will be tossed out. Note that both NEXRAD WSR88D and NOAA P-3 tail radars do not have this variable currently, so the NCP variable can be replaced by any other variables to perform the simple quality control (QC). Both minDbz and minNcp are designed for the QC of a real-time analysis. 
- testMode: the default test mode is MODE_ZETA. The testMode option is designed for the developers to test and debug.
- zGrid: specify vertical grid spacing "incr" or "min, max, incr" which represents the lowest level, the highest level, and constant spacing of the vertical level respectively.
- yGrid: similar as zGrid. It specifies the grid parameters in y.
- xGrid: similar as zGrid. It specifies the grid parameters in x.
- gridType: mesh is for stand-alone analysis, while mish is as a background field for SAMURAI input. For the current release, we recommend the users to use mesh for the analysis. The mish gridType is experimental and still under development.
- projLat0: the latitude of the reference point (0,0).
- projLon0: the longitude of the reference point (0,0).
- numNbrMax: the maximum points for the nearest neighbor algorithm to consider at each grid point.
- inDir: input directory for searching for files. Files will be searched for in this directory.
- fileRegex: regular expression to select files in inDir. If input file format is CfRadial (DORADE), specify it as "^cfrad (^swp)".
- outTxt: specify the directory of a output summary file which contains verification of grid results.
- outNc: specify the directory of a output netCDF file which is the result of the analysis.
- radialName: specify the variable name of radial velocity.
- dbzName: specify the variable name of reflectivity.
- ncpName: specify the variable name of NCP. If there is no NCP variable, you can specify any other variable to perform the QC. This variable corresponds to minNcp for the threshold.
- uvInterp: set the wind interpolation method for u and v. The specified interpolation method will be applied before calculating the vertical velocity. The default mode is INTERP_NONE. 


