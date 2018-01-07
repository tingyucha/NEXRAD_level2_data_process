# RadxConvert

RadxConvert allows you to convert data stored in one format to a different format. It can support in the following formats:
- CfRadial - NCAR/EOL/UNIDATA	
- DORADE - NCAR/EOL	
- UF - Universal Format	
- Foray-1 netCDF - NCAR/EOL	
- DOE ARM netcdf - precedes CfRadial	
- MDV radial - NCAR/RAL	
- NEXRAD msg31 level 2 archive	
- NEXRAD msg1 level 2 archive	
- SIGMET - raw format (Vaisala)	
- RAPIC - BOM Australia	
- HRD - HRD NOAA	
- LEOSPHERE LIDAR, ASCII format	
- EEC - now supports CfRadial	

RadxConvert command can be used either specifying the file format with parameter file or specifying the format in command line.

## Creat run-time parameter file 

```terminal
/path/to/Radx/apps/RadxConvert -print_params > RadxConvert.params
```

The user can specify the specific output format in RadxConvert.params file. 

For example:

Open RadxConvert.params in the terminal and find the line with "output_format"

1. Convert Level II data to cfradial format

```terminal
output_format = OUTPUT_FORMAT_CFRADIAL
```

2. Convert Level II data to sweep format

```terminal
output_format= OUTPUT_FORMAT_DORADE
```

Once the parameter file is complete, use the following command to run the application:

```terminal
/path/to/Radx/apps/RadxConvert -f Level2_KAMX_20161006_1906.ar2v -params RadxConvert.params
```

## Convert file format in command line (by default)

If the user don't have specific requirement to the conversion setting, you can use the following command to obtain the file as well: 

1. Convert Level II data to cfradial format

```terminal
/path/to/Radx/apps/RadxConvert -cfradial -f Level2_KAMX_20161006_1906.ar2v
```

2. Convert Level II data to sweep format

```terminal
/path/to/Radx/apps/RadxConvert -dorade -f Level2_KAMX_20161006_1906.ar2v
```


