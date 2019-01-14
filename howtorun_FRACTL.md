# Fast Reorder and CEDRIC Technique in LROSE (FRACTL) 

FRACTL is a fast traditional solver with integrated interpolation using LROSE infrastructure, and it is able to perform both gridding and multi-Doppler synthesis for airborne radars and multiple ground-based radars, which is different than Radx2Grid whereas it only has the capability for gridding of a single ground-based radar data. FRACTL adopts both REORDER and CEDRIC programs which REORDER is a program that transforms radar data from its native coordinate system to cartesian space and the data can then be ingested into CEDRIC for synthesis.

## Running FRACTL

The main features of using FRACTL are:
- "Traditional" multi-Doppler solver written from the ground up in C++
- Quasi-horizontal 2-radar assumption (U,V) with mass-continuity for W, or full 3D solution (U, V, W)
- Nearest neighbor algorithm adds Doppler gates directly to matrix solver at each grid point, no interpolation or averaging of velocity required
- Solve normal equations using Singular Value Decomposition (preferred) or Cramer’s method
- Subset of CEDRIC diagnostics implemented, more on the way
- <5 minutes for dual-Doppler (~3M gates)

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
- minNcp: any values below the minimum NCP will be tossed out. Note that both NEXRAD WSR88D and NOAA P-3 tail radars do not have this variable currently, so the value of minNcp doesn't have any impact on the analysis.
- testMode: set the wind synthesis mode. There are six different modes that you can choose.
- zGrid: specify vertical grid spacing "incr" or "min, max, incr" which represents the lowest level, the highest level, and constant spacing of the vertical level respectively.
- yGrid: similar as zGrid. It specifies the grid parameters in y.
- xGrid: similar as zGrid. It specifies the grid parameters in x.
- gridType: mesh is for stand-alone analysis, while mish is as a background field for SAMURAI input.
- projLat0: the latitude of the reference point (0,0).
- projLon0: the longitude of the reference point (0,0).
- numNbrMax: the nearest number of points for the synthesis.
- inDir: input directory for searching for files. Files will be searched for in this directory.
- fileRegex: regular expression to select files in inDir. If input file format is CfRadial (DORADE), specify it as "^cfrad (^swp)".
- outNc: specify the name of the output netCDF file.
- radialName: specify the variable name of radial velocity.
- dbzName: specify the variable name of reflectivity.
- ncpName: specify the variable name of NCP.
- uvInterp: set the wind interpolation method for u and v. The specified interpolation method will be applied before calculating the vertical velocity.

