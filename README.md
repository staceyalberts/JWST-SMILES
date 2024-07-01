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

hlsp\_smiles\_jwst\_\<instrument\>\_goodss\_\<filter\>\_\<version\>\_\<data file type\>.fits

where:

\<inst\> is the instrument, here 'miri' <br>
\<filter\> is the filter or 'multi' for the photometric catalog  <br>
\<version\> is the version number ("v1.0").  

Data file types:

\_drz.fits		Image mosaic  <br>
\_catalog.fits	Photometric catalog

---------

# Mosaics

MIRI image mosaics are presented with a pixel scale of 0.06" and have the following structure:

No.	&emsp;Name  		&emsp;Type  	 	          &emsp;Format  <br>
  0  	&emsp;PRIMARY   	 &emsp;PrimaryHDU 		&emsp;– 	  <br>
  1  	&emsp;SCI       	 &emsp;ImageHDU    		&emsp;float32     &emsp;science image  <br>
  2  	&emsp;ERR       	 &emsp;ImageHDU    		&emsp;float32     &emsp;error image  <br>
  3  	&emsp;EXP       	 &emsp;ImageHDU   		&emsp;float32     &emsp;exposure time map  <br>
  4  	&emsp;WHT       	 &emsp;ImageHDU     		&emsp;float32     &emsp;weight map  <br>
  
----------------------

# Photometric catalog

The SMILES DR1 photometric catalog contains 3,096 sources.  Measurements are provided in all bands for sources detected at ≥4sigma in F560W or F770W, with false positives identified and removed using ultra-deep NIRCam imaging from JADES (see Alberts et al., 2024 for details).  Flux densities and their associated uncertainties are provided in 5 circular apertures (CIRC3-7, r = 0.25, 0.3, 0.35, 0.5, 0.6”) and 2.5x scaled Kron apertures. 

Fluxes and uncertainties are in units of nano-Janskys.

The photometric catalog is a fits file with the following structure:

No.	&emsp;Name  	   		&emsp;Type <br>  	             
0  &emsp;PRIMARY       	  &emsp;PrimaryHDU <br>	 
1  &emsp;FILTERS   	      &emsp;BinTableHDU <br>       
2  &emsp;SIZE      	      &emsp;BinTableHDU <br>    
3  &emsp;CIRC      	      &emsp;BinTableHDU <br>
4  &emsp;KRON       	  &emsp;BinTableHDU 
  
EXT 1 contains information about the filters used and their corresponding Point Spread Functions (PSFs), including the FWHM and aperture corrections for the circular apertures used.

EXT 2 contains the following:


Description of columns:

'ID'			&emsp;Observation ID <br>
'RA'			&emsp;Source RA <br>
'DEC'			&emsp;Source Dec  <br>
'NPIX_DET'		&emsp;Number of pixels used for detection <br>
'X'				&emsp;Pixel location in x direction <br>
'Y'				&emsp;Pixel location in y direction <br>
'XC'			&emsp;Pixel location of x centroid in detection image <br>
'YC'			&emsp;Pixel location of x centroid in detection image <br>
'BBOX_XMIN'		&emsp;The boundaries of the area used for detection <br>
'BBOX_XMAX'		&emsp;"  <br>
'BBOX_YMIN'		&emsp;"  <br>
'BBOX_YMAX'		&emsp;" <br>
'R_KRON'		&emsp;Kron radius (2.5x scaled) <br>
'PA'			&emsp;Position angle of Kron aperture <br>
'Q'				&emsp;Axial ratio of Kron aperture <br>
'A'				&emsp;emi-major axis <br>
'B'				&emsp;Semi-minor axis <br>

EXT 3 contains the circular aperture photometry:


Description of columns:

'ID'					&emsp;Observation ID <br>
'RA'					&emsp;Source RA <br>
'DEC'					&emsp;Source Dec <br>
\<filter\>\_\<aperture\>		&emsp;Flux densities in a given filter for a given circular aperture <br>
\<filter\>\_\<aperture\>_en	&emsp;Flux uncertainties in a given filter for a given circular aperture

Flux densities and uncertainties are given in nJy.  The apertures are CIRC3, CIRC4, CIRC5, CIRC6, CIRC7 with radii of r=0.25, 0.3, 0.35, 0.5, 0.6 arcseconds.

EXT 3 contains the Kron aperture photometry:


Description of columns:

'ID'					&emsp;Observation ID <br>
'RA'					&emsp;Source RA <br>
'DEC'					&emsp;Source Dec <br>
\<filter\>\_KRON			&emsp;Flux densities in a given filter <br>
\<filter\>\_KRON_en		&emsp;Flux uncertainties in a given filter

Flux densities and uncertainties are given in nJy.  The Kron apertures are 2.5x scaled.


