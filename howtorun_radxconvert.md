# RadxConvert

RadxConvert allows you to convert data stored in one format to a different format. It can support in the following formats:

| Format        | Read Access   | Write Access |
| ------------- |:-------------:| -----:|
| CfRadial - NCAR/EOL/UNIDATA	| Yes | Yes |
| DORADE - NCAR/EOL	| Yes | Yes |
| UF - Universal Format	| Yes | Yes |
| Foray-1 netCDF - NCAR/EOL	| Yes | Yes |
| DOE ARM netcdf - precedes CfRadial	| Yes | No |
| MDV radial - NCAR/RAL	| Yes | Yes |
| NEXRAD msg31 level 2 archive	| Yes | Yes |
| NEXRAD msg1 level 2 archive	| Yes | No |
| SIGMET - raw format (Vaisala)	| Yes | No |
| RAPIC - BOM Australia	| Yes | No |
| HRD - HRD NOAA	| Yes | No |
| LEOSPHERE LIDAR, ASCII format	| Yes | No |
| EEC - now supports CfRadial	| Yes | N/A |

## Running RadxConvert

To check all command line options for RadxConvert, type the following command into a terminal.

```terminal
/path/to/Radx/apps/RadxConvert -h
```

There are two different ways to specify the output file format. It can be specified either in parameter file or in command line.

1. Creat run-time parameter file 

```terminal
/path/to/Radx/apps/RadxConvert -print_params > RadxConvert.params
```

The user can specify the specific output format in RadxConvert.params file. 

For example:

Open RadxConvert.params in the terminal and find the line with "output_format"

- Convert Level II data to cfradial format

```terminal
output_format = OUTPUT_FORMAT_CFRADIAL
```

- Convert Level II data to sweep format

```terminal
output_format= OUTPUT_FORMAT_DORADE
```

Once the parameter file is complete, use the following command to run the application:

```terminal
/path/to/Radx/apps/RadxConvert -f Level_II_file -params RadxConvert.params
```

2. Convert file format in command line (by default)

If the user don't have specific requirement to the conversion setting, you can use the following command to obtain the file as well: 

- Convert Level II data to cfradial format

```terminal
/path/to/Radx/apps/RadxConvert -cfradial -f Level_II_file
```

- Convert Level II data to sweep format

```terminal
/path/to/Radx/apps/RadxConvert -dorade -f Level_II_file
```


