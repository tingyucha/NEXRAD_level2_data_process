# Radx2Grid

Radx2Grid performs coordinate transformations from the polar grid on which radar data is collected to a regular grid.

The following regular grids are supported:

- Cartesian grid in (Z,Y,X)
- PPI grid in (EL, Y, Z) - performs Cartesian transformation on each elevation angle separately
- Polar grid, regular in (EL, AZ, RANGE)

## Running Radx2Grid

To check all command line options for RadxConvert, type the following command into a terminal.

```terminal
/path/to/Radx/apps/Radx2Grid -h
```
1. Creat run-time parameter file 


```terminal
/path/to/Radx/apps/Radx2Grid -print_params > Radx2Grid.params
```

The user can edit specific setting in the parameter file (etc. grid spacing, interpolation mode, filename).

Caution: this is not an exhaustive list. We urge each user to read through the entire parameter file carefully.

Specific parameters to edit:

- start_time, end_time: set the start time and end time for ARCHIVE mode analysis. The format should be 'yyyy mm dd hh mm ss'.
- input_dir: input directory for searching for files. Files will be searched for in this directory.
- interp_mode: set the interpolation mode. There are five different modes that you can choose.
- grid_z_geom: specify vertical grid levels. nz, minz, dz represent the number of levels, the lowest level, and constant spacing of the vertical level respectively.
- grid_xy_geom: similar as grid_z_geom. It specifies the grid parameters in x and y.
- netcdf_style: specify different format of netCDF. If output_format is CFRADIAL, specify the netCDF format.
- ncf_title: title string for netCDF file.
- ncf_institution: institution string for netCDF file.
- ncf_source: source string for netCDF file.






