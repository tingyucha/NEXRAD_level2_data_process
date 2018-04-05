# Radx2Grid

Radx2Grid performs coordinate transformations from the polar grid on which radar data is collected to a regular grid.

The following regular grids are supported:

- Cartesian grid in (Z,Y,X)
- PPI grid in (EL, Y, Z) - performs Cartesian transformation on each elevation angle separately
- Polar grid, regular in (EL, AZ, RANGE)

## Prerequesites
The following item are required:
- RadxConvert output files (cfradial)

## Parameter file
The parameter file will need to be updated to include the location of Radx2Grid files, in addition to data interpolation method set by the user.

### Ensure parameter file is up to date
To obtain the default parameter file, use the following command:

```terminal
/path/to/Radx/apps/Radx2Grid -print_params > param_file_name
```

If you already have a parameter file and simply want to check for (and add) updated parameters while retaining current parameters, use the following command:

```terminal
/path/to/Radx/apps/Radx2Grid -params orig_param_file_name -print_params > new_param_file_name
```

### Specific parameters to edit
Caution: this is not an exhaustive list. We urge each user to read through the entire parameter file carefully.

- start_time, end_time: set the start time and end time for ARCHIVE mode analysis. The format should be 'yyyy mm dd hh mm ss'.
- input_dir: input directory for searching for files. Files will be searched for in this directory.
- interp_mode: set the interpolation mode. There are five different modes that you can choose.
- grid_z_geom: specify vertical grid levels. nz, minz, dz represent the number of levels, the lowest level, and constant spacing of the vertical level respectively.
- grid_xy_geom: similar as grid_z_geom. It specifies the grid parameters in x and y.
- netcdf_style: specify different format of netCDF. If output_format is CFRADIAL, specify the netCDF format.
- ncf_title: title string for netCDF file.
- ncf_institution: institution string for netCDF file.
- ncf_source: source string for netCDF file.


## Running Radx2Grid
To check all command line options for Radx2Grid, including debugging options and file paths, type the following command into a terminal.

```terminal
/path/to/Radx/apps/Radx2Grid -h
```

Once your parameter file is complete, specify the location of cfradial files to run the application:

```terminal
/path/to/Radx/apps/Radx2Grid -f cfradial_file -params param_file_name
```


