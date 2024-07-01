# JWST-SMILES
Repository for the JWST/MIRI SMILES multi-band survey. 

README file for the Systematic Mid-Infrared Instrument Legacy Extragalactic Survey (SMILES)

MAST webpage: https://archive.stsci.edu/hlsp/smiles/

Refer to this HLSP with DOI: http://dx.doi.org/10.17909/et3f-zd57

## Contributor
Stacey Alberts, salberts@arizona.edu, Steward Observatory, University of Arizona

## INTRODUCTION

The Systematic Mid-Infrared Instrument Legacy Extragalactic Survey (SMILES) (PID 1207) is a Cycle 1 imaging program that obtained MIRI imaging in eight photometric bands (F560W, F770W, F1000W, F1280W, F1500W, F1800W, F2100W, F2550W) plus NIRSpec spectroscopic follow-up using the Multi-Shutter Array (MSA).  SMILES covers an area of 34.5 arcmin2 in the GOODS-S/HUDF field.  MIRI imaging was obtained via ~650-2200 s exposures, reaching 5sig point source sensitivities of 0.2-17 uJy (25.7 - 20.8 AB) in 65% encircled energy apertures (see Alberts et al., 2024 for details).  Data release 1 (DR1) includes science-ready MIRI mosaics as well as a catalog contains 3,096 sources with photometric measurements in all bands. 

## Data Products

Data Release 1 (June 2024)

The SMILES data products are named according to the following convention:

hlsp_smiles_jwst_\<instrument\>_goodss_\<filter\>_\<version\>_\<data file type\>.fits

where:

\<inst>\ is the instrument, here 'miri'

\<filter\> is the filter or 'multi' for the photometric catalog

\<version\> is the version number ("v1.0").

Data file types:

_drz.fits		Image mosaic
_catalog.fits	Photometric catalog

---------

# Mosaics

MIRI image mosaics are presented with a pixel scale of 0.06" and have the following structure:

No.	Name  		Type  	 	          Format
  0  	PRIMARY   	 PrimaryHDU 		– 	 
  1  	SCI       	 ImageHDU    		float32     basic image 
  2  	ERR       	 ImageHDU    		float32     flux uncertainty
  3  	EXP       	 ImageHDU   		float32     exposure time
  4  	WHT       	 ImageHDU     		float32     weight
  
----------------------

# Photometric catalog

The SMILES DR1 photometric catalog contains 3,096 sources.  Measurements are provided in all bands for sources detected at ≥4sigma in F560W or F770W, with false positives identified and removed using ultra-deep NIRCam imaging from JADES (see Alberts et al., 2024 for details).  Flux densities and their associated uncertainties are provided in 5 circular apertures (CIRC3-7, r = 0.25, 0.3, 0.35, 0.5, 0.6”) and 2.5x scaled Kron apertures. 

Fluxes and uncertainties are in units of nano-Janskys.

The photometric catalog is a fits file with the following structure:

No.	Name  	   		Type  	             
  0  PRIMARY       	  PrimaryHDU	 
  1  FILTERS   	      BinTableHDU       
  2  SIZE      	      BinTableHDU    
  3  CIRC      	      BinTableHDU
  4  KRON       	  BinTableHDU  
  
EXT 1 contains information about the filters used and their corresponding Point Spread Functions (PSFs), including the FWHM and aperture corrections for the circular apertures used.

EXT 2 contains the following:

-----------------------
Description of columns:
-----------------------

'ID'			Observation ID
'RA'			Source RA
'DEC'			Source Dec
'NPIX_DET'		Number of pixels used for detection
'X'				Pixel location in x direction
'Y'				Pixel location in y direction
'XC'			Pixel location of x centroid in detection image
'YC'			Pixel location of x centroid in detection image
'BBOX_XMIN'		The boundaries of the area used for detection
'BBOX_XMAX'		"
'BBOX_YMIN'		"
'BBOX_YMAX'		"
'R_KRON'		Kron radius (2.5x scaled)
'PA'			Position angle of Kron aperture
'Q'				Axial ratio of Kron aperture
'A'				Semi-major axis
'B'				Semi-minor axis

EXT 3 contains the circular aperture photometry:

-----------------------
Description of columns:
-----------------------

'ID'					Observation ID
'RA'					Source RA
'DEC'					Source Dec
<filter>_<aperture>		Flux densities in a given filter for a given circular aperture
<filter>_<aperture>_en	Flux uncertainties in a given filter for a given circular aperture

Flux densities and uncertainties are given in nJy.  The apertures are CIRC3, CIRC4, CIRC5, CIRC6, CIRC7 with radii of r=0.25, 0.3, 0.35, 0.5, 0.6 arcseconds.

EXT 3 contains the Kron aperture photometry:

-----------------------
Description of columns:
-----------------------

'ID'					Observation ID
'RA'					Source RA
'DEC'					Source Dec
<filter>_KRON			Flux densities in a given filter
<filter>_KRON_en		Flux uncertainties in a given filter

Flux densities and uncertainties are given in nJy.  The Kron apertures are 2.5x scaled.


