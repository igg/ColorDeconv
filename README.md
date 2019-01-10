# ColorDeconv
### Color deconvolution for RGB files with 48-bit RGB-TIFF support
Used to separate/deconvolve histochemical stains out of color images into separate greyscale image files.

* This program uses the method described in:

    Ruifrok AC, Johnston DA. Quantification of histological staining by color deconvolution.
    Analytical & Quantitative Cytology & Histology 2001; 23: 291-299.

* This program is a refinement of the implementation for Color Deconvolution in ImageJ/Fiji:
    * Correctly processes high-bit-depth RGB images
    * Iterative refinement of the deconvolution to maximize the signal in the defined stains
    * Deconvolution of many images in batch mode

Usage:
```
color_deconv -s <stain>[:<label>] [-s <stain>[:<label>]] [-s <stain>[:<label>]] [-w n,n,n] [-i [num iter]] file1.tiff [fileN.tiff ...]
  <stain> is one of 'H', 'E', 'DAB', 'FastRed', 'FastBlue', 'MethylGreen', 'AnilineBlue','Azocarmine',
    'AlcianBlue', 'PAS', 'Nissl', 'R', 'G', 'B', 'C', 'M', 'Y'
    OR, a set of RGB values separated by commas, for example:
    -s 1.23,4.56,7.89 -s 123,456,789:St1 -s H:Hem
    -sOD may be used instead of -s to specify stains in optical densities instead of RGB pixel values
    If only 2 stains are specified, the third file (file_2) contains the 'remainder'
    A maximum of three stains can be specified
  <label> will be appended to the stain's output file base-name after a '_'.
    Default labels will be used if not specified.
    The above example with a 'file.tif' filename will result in:
    file_0.tiff, file_St1.tif and file_Hem.tif
    -w Set white-level by specifying RGB values separated by commas
    -i Iterate to maximize stain separation. Optionally specify the number of iterations (default=%d, min=1)
  Any number of tiff files may be specified at the end.  The tiff files must be RGB format, and may be 8, 16 or 32 bits per channel.
```
