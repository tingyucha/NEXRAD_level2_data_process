# RadxPrint

RadxPrint allows you to print data header from any of the files supported by Radx, such as cfradial and sweep format.

## Running RadxPrint

To check all command line options for RadxPrint, type the following command into a terminal：

```terminal
/path/to/Radx/apps/RadxPrint -h
```

- To print the data with cfradial format in a generic form, type:

```terminal
/path/to/Radx/apps/RadxPrint -f ./output/20161006/cfrad.20161006_190750.006_to_20161006_191335.539_KAMX_Surveillance_SUR.nc
```

- To print the data with sweep format in a generic form, type:
```terminal
/path/to/Radx/apps/RadxPrint -ag -f ./output/20161006/*.swp 
```


⋅⋅If the user prefers to store the printed information in a .txt file, type:

```terminal
/path/to/Radx/apps/RadxPrint -f ./output/20161006/cfrad.20161006_190750.006_to_20161006_191335.539_KAMX_Surveillance_SUR.nc > file_name.txt
```

⋅⋅In addition, RadxPrint also allows you to print out a specific field.

⋅⋅For example, print the information of REF field into a .txt file:
```terminal
/path/to/Radx/apps/RadxPrint -f ./output/20161006/cfrad.20161006_190750.006_to_20161006_191335.539_KAMX_Surveillance_SUR.nc -field REF > file_name.txt
```


