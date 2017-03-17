qMT_MFA_v1_0_0
=========================

* **What does it do?**
Numerically fits qMT data to the 2004 Yarnykh model. Utilizes an MFA scan for T1 estimation. Also requires B1 and B0 maps for inhomogeneity correction. Fits three parameters, f (PSR), k, and T2b. 

How to use this spider: 
See pipelines/qMT_MFA/v1.0.0/xnat_example/ for scripts on how to create the mat file. The mat file must contain:

| col_center - Centroid for cropping 
| row_center - Centroid for cropping
| initial_model - The initial model for fitting [f,k,T2b], see MT_model.m for example values. 
| imaging - The imaging structure which defines image acquisition parameters needed for simulation. See imaging_yar.m for an example. Structure must contain: 
* deltav - vector of offsets in Hz
* alpha - Excitation flip angle (radians)
* alphaMTv - vector of saturation flip angles (radians)
* TR - the MT acquisition repetition time (s)
* pw - The saturation pulse width (s)
* tauSpoil - the spoling gradient time (s) [typically 1ms]
* B1ev - Vector of B1 equivalent powers
* VFA_TR - Repetition time for the multi flip angle acquisition (s)
* VFA_alpha - flip angle for the multi flip angle acquisition (radians)
* VFA_norm_ind - The index/scan number to be used to normalize the multi flip angle data

All of these parameters must be included in a single MAT file and uploaded to the MAT resource on the qMT scan for it to run. 

* **Data Requirements**
| qMT acquisition
| Multi-flip angle experiment
| B1 map
| B0 map
| MAT file with parameters in resource MAT

* **Software Requirements**
| masimatlab utilities
| niftireg

* **Resources (Outputs)**
| OUTLOG - STDOUT and STDERR from the process on the grid
| PBS - The DRMAA compliant batch script to run the job
| PDF - The output PDF file for determining QA status
| SNAPSHOTS - Thumbnail of the first page of the PDF resource for viewing on XNAT
| FIT_RESULTS - mat file containing fit_results which is [mxnxslicesx4] corresponding to f,k,T2b,R1f results.

* **References**
Robert L Harrigan, Bennett A Landman, Seth A Smith, "Optimization of Quantitative Magnetization Transfer Imaging for Accurate PSR Estimation in the Spinal Cord". ISMRM 2017. Honolulu, Hawaii USA. Poster 

**Current Contact Person**
March 2017 Robert L Harrigan `email <mailto:Rob.L.Harrigan@vanderbilt.edu>`_ 

* **Version History**
<revision> <name> <date> <lines changed>
