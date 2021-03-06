# RGPR: a free and open-source software package to process and visualise *ground-penetrating radar* (GPR) data 


RGPR is a free and open-source software package to read, export, analyse, process and visualise *ground-penetrating radar* (GPR) data. RGPR is written in [R](https://cran.r-project.org/), a high-level  programming language for statistical computing and graphics that is freely available under the GNU General Public License and runs on Linux, Windows and MacOS.


## Note

* supported binary formats: 
    
    - [x] Sensors & Software file format (.DT1, .HD)
    - [x] MALA file format (.rd3, .rad)
    - [x] SEG-Y file format (.sgy) from RadSys Zond GPR device
    
    Do you miss your preferred file format? Send me the file format description with a test file and I will adapt the RGPR-package to support this file format. 
    
* RGPR only support reflection data such as surface-based GPR data (no support for cross-borehole GPR data)
* the documentation is still incomplete (but check the tutorials, http://emanuelhuber.github.io/RGPR)

This is an ongoing project.
If you have any questions, don't hesitate to contact me:

emanuel.huber@alumni.ethz.ch

Thank you!

## Online tutorials
Check the companion website for more info, tutorials, etc.

http://emanuelhuber.github.io/RGPR

## How to install/load

```r
if(!require("devtools")) install.packages("devtools")
devtools::install_github("emanuelhuber/RGPR")
library(RGPR)

frenkeLine00  # data from the package

plot(frenkeLine00)

```

## Existing functions

### Reading/writing/export functions
* `readGPR()`, formats: Sensors & Software (.d11, .hd), MALA (.rd3, .rad), SEG-Y for RadSys Zond GPR device (.sgy),  R (rds)
* `writeGPR()`: format DT1 (Sensors&Software), rds (R-format), ASCII, 'xyz'
* `exportPDF()`: high quality pdf graphic
* `exportDelineations()`
* `exportFID()`: ASCII-file
* `exportCoord()`: SpatialLines, SpatialPoints or ASCII-file
* `exportProc()`: ASCII-file

### Plot functions
* `plot()`:
   * `type = "raster"` 
   * `type = "wiggles"`
* `lines()`
* `plot3D()`


### GPR data editing and referencing

* Trace position reversal: `reverse()`
* Vertical trace shift: `traceShift()`
* Georeference coordinates (based on center and rotation angle): `georef()` 
* Interpolate trace position (x, y, z) from known positions: `interpPos()`
* Estimate shift between two parallel profiles: `shiftEst()`

###  GPR data analysis and transforms
* Trace amplitude: `ampl()`, plot trace amplitude: `plotAmpl()`
* Average trace: `traceAverage()`
* Spectrum (f-x and f-k): `spec(x, type = c("f-x", "f-k"))`
* Structure tensor: `strTensor()`, plot structure tensor: `plotTensor()`

### GPR data interpolation
* Trace interpolation at regularly spaced positions: `regInterpPos()`
* Upsampling (time and position): `upsample()`
* Relative position on the radargramm: `relPos()`

### GPR signal correction
* DC-shift correction: `dcshift()`
* Low-frequency ('wow') component removal: `dewow()` (type = "MAD", "Gaussian")
* First-break picking: `firstBreak()` (method = "coppens", "threshold",  "MER")
* Shift the traces vertically such that they start at time zero: `time0Cor()`
* Constant offset time correction: `timeCorOffset()` 

### GPR signal attenuation compensation (gain)
* Linear, power, exponential, ang agc gain: `gain()` (type = "power", "exp", "agc")


### GPR signal enhancement
* Clip the GPR signal values: `clip()`
* Gamma correction of the GPR signal values: `gammaCorrection()`
* Trace scaling: `traceScaling()`
* Trace filters (1D): `filter1D()`: type = "median", "hampel", "Gaussian"
* Radargramm filters (2D): `filter2D()`: type = "median3x3", "adimpro"
* Trace frequency filter (1D): `fFilter()`: freqency filter, type = 'low','high','bandpass'
* Frequency-wavenumber filter (2D): `fkFilter()`
* Trace (1D) and radargramm (2D) convolution: `conv1D()` and `conv2D()` 
* Deconvolution: `deconv()` (type = "spiking", "wavelet", "min-phase",
  "mixed-phase")
* Phase rotation `rotatePhase()`

### GPR signal velocity 
* Common-mid point analysis (CMP): `CMPAnalysis()` (method = "semblance", "winsemblance",
  "wincoherence")
* Normal Move-Out correction (NMO): `NMOCor()`

### GPR data topographic correction and migration 
* Topography correction and topographic Kirchhoff migration: `migration()` (type = "static", "kirchhoff")

###  GPR structure delineation and mapping  [EH]
* `delineate()`
* `rmDelineations()<-`
* `delineations()`
* `addDelineation()`
* `plotDelineations3D()`
* `plotDelineations()`
* `identifyDelineation()`

### Processing
* Apply many processing steps: `papply()`

### Miscellaneous
* Operators: `+`, `-`, `*`, `/`, `^`
* Mathematical functions: `max()`, `min()`, `mean()`, `median()`, `summary()`, `range()`, `abs()`, `sign()`, `sqrt()`, `ceiling()`, ...
* Matrix functions: `length()`, `nrow()`, `ncol()`, `dim()`
* Coercion: `as.matrix()`, `as.numeric()`, `as.double()`, `as.list()`, `as.SpatialLines()`, `as.SpatialPoints()`

### Setter/getter functions
* `depthunit()` & `depthunit()<-`
* `description()` & `description()<-`
* `ann()` & `ann()<-`
* `coord()` & `coord()<-`
* `crs()` & `crs()<-`
* `fid()` & `fid()<-`
* `filepath()` & `filepath()<-`
* `pos()` & `pos()<-`
* `posunit()` & `posunit()<-`
* `proc<-()` & `processing` 
* `name()` & `name()<-`
* `values()` & `values()<-`
* `vel()` & `vel()<-` 
* `gethd()`
* `svDate()` & `svDate()<-`
     

        


### List of the functions from the class `GPR`
```r
library(RGPR)
mtext <-  showMethods(class="GPR", printTo =FALSE )
i <- grepl('Function', mtext) & grepl('package RGPR', mtext) 
fvec <- gsub( "Function(\\:\\s|\\s\\\")(.+)(\\s\\(|\\\")(.+$)", "\\2", mtext[i] )
fvec
```

### List of the functions from the class `GPRsurvey`
```r
library(RGPR)
mtext <-  showMethods(class="GPRsurvey", printTo =FALSE )
i <- grepl('Function', mtext) & grepl('package RGPR', mtext) 
gvec <- gsub( "Function(\\:\\s|\\s\\\")(.+)(\\s\\(|\\\")(.+$)", "\\2", mtext[i] )
gvec
```

### Incomplete overview of the RGPR-package
```r
?RGPR
```

## Contributions

Thanks to:

-  @jmerc13
