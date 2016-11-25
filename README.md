<!-- README.md is generated from README.Rmd. Please edit that file -->
getais
======

The getais R package is simply a data processing package, meant to download and process the very large AIS datasets from MarineCadastre.gov.

You can install the development version of the package with:

``` r
# install.packages("devtools")
if("getais" %in% rownames(installed.packages()) == FALSE) {
  devtools::install_github("eric-ward/getais")
}
library(getais)
```

An example processing script
----------------------------

Create data frame for all combinations

``` r
if (!file.exists("filtered")) dir.create("filtered")

all_combos = expand.grid("zone"=1:19,"year"=2009:2014,"month"=1:12)
```

As an example, we'll only use data from December and UTM Zone 1.

``` r
subset = all_combos[which(all_combos$zone==1 & all_combos$month==12),]

head(subset)
#>      zone year month
#> 1255    1 2009    12
#> 1274    1 2010    12
#> 1293    1 2011    12
#> 1312    1 2012    12
#> 1331    1 2013    12
#> 1350    1 2014    12
```

Process the data for these combinations of months / years / zones. The user can also specify the 'hours' argument, which finds observations from each vessel that are closest to that time. For example, if observations closest to noon each day are wanted, specify 12, if observations every 6 hours are wanted, specify c(0, 6, 12, 18). Here we'll just get records closest to 4am and noon,

``` r
process_ais(df = subset, hours = c(4,12))
```
