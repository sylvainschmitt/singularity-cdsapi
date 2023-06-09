Singularity container of the API to access the Copernicus Climate Data
Store (CDS)
================
Sylvain Schmitt
June 9, 2023

**Python API to access the Copernicus Climate Data Store (CDS)**

This container includes:

- Python 3.7
- [cdsapi](https://github.com/ecmwf/cdsapi)

Singularity container based on the recipe:
[Singularity](https://github.com/sylvainschmitt/singularity-cdsapi/blob/main/Singularity)

Image singularity (V\>=3.3) is automatically test and built and pushed
on the registry using
[test.yml](https://github.com/sylvainschmitt/singularity-cdsapi/blob/main/.github/workflows/test.yml)
&
[builder.yml](https://github.com/sylvainschmitt/singularity-cdsapi/blob/main/.github/workflows/builder.yml)

**build**:

``` bash
sudo singularity build cds.sif Singularity
```

**pull**:

``` bash
singularity pull https://github.com/sylvainschmitt/singularity-cdsapi/releases/download/0.0.1/sylvainschmitt-singularity-cdsapi.latest.sif
```

**snakemake**:

``` python
    singularity: 
        "https://github.com/sylvainschmitt/singularity-cdsapi/releases/download/0.0.1/sylvainschmitt-singularity-cdsapi.latest.sif"
```

**configure**:

Get your user ID (UID) and API key from the CDS portal at the address
<https://cds.climate.copernicus.eu/user> and write it into the
configuration file, so it looks like:

    $ cat ~/.cdsapirc
    url: https://cds.climate.copernicus.eu/api/v2
    key: <UID>:<API key>
    verify: 0

Remember to agree to the Terms and Conditions of every dataset that you
intend to download.

**usage**:

``` python
singularity shell cds.sif 
python3.7
import cdsapi
cds = cdsapi.Client()
cds.retrieve('reanalysis-era5-pressure-levels', {
           "variable": "temperature",
           "pressure_level": "1000",
           "product_type": "reanalysis",
           "date": "2017-12-01/2017-12-31",
           "time": "12:00",
           "format": "grib"
       }, 'download.grib')
```
