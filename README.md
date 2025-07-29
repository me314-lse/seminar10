# seminar10

This repo contains the material for Seminar 10.

## Troubleshooting `sf`

The `sf` package is a complex wrapper around several frameworks for geospatial data. If you experience issues with the `sf` installation, check out [the `sf` installation guide](https://r-spatial.github.io/sf/#installing) first. 

Try the following steps if your `sf` package installation throws **errors** (warnings are ok and can usually be ignored.)


# SF Package Installation Troubleshooting Guide

## Quick Start (Try This First!)

For most users, installing the sf package is straightforward:

```r
install.packages("sf")
library(sf)
```

If this works without errors, you're ready to go! Test with:

```r
nc <- st_read(system.file("shape/nc.shp", package="sf"))
plot(st_geometry(nc))
```

If you see a map of North Carolina counties, the installation was successful.


## Windows Troubleshooting

### Problem 1: "LoadLibrary failure" errors
**Solution:**
1. Restart R/VScode
2. Try installing from github:
```r
remotes::install_github("r-spatial/sf", dependencies = TRUE)
```

**If this does not work, you may need to install Rtools and install sf from source. Check out the [the `sf` installation guide](https://r-spatial.github.io/sf/#installing) for details.**

## macOS Troubleshooting

### Problem 1: If gdal, geos or proj libraries are not found
**Solution:**
1. Install Homebrew (if not already installed):
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

2. Install spatial libraries:
```bash
brew install gdal proj geos
```

3. Reinstall sf from source:
```r
install.packages("sf", type = "source")
```

### Problem 2: "Symbol not found" errors on M1/M2 Macs
**Solution:**
1. Make sure you have the ARM64 version of R installed
2. Check with:
```r
Sys.info()["machine"]  # Should show "arm64"
```
3. If showing "x86_64", download R for Apple Silicon from CRAN

### Problem 3: "Library not loaded" errors
**Solution:**
1. In Terminal, run:
```bash
brew update
brew upgrade gdal proj geos
```
2. Restart R and reinstall sf



## General Troubleshooting Steps - Clean Installation

```r
# Remove existing installation
remove.packages("sf")
# Clear package cache
unlink(.libPaths()[1], recursive = TRUE)
# Restart R (Session → Restart R in RStudio)
# Reinstall
install.packages("sf")
```