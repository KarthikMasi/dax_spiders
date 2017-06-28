NIRSQA_v1_0_0
=============

What does it do?
----------------

The NIRSQA spider provides initial filtering and some quality metrics for near-infrared optical topography data.

A data quality metric is provided for each channel following the method described by Pollonini et al (2014). A 0.5 Hz to 2.5 Hz bandpass filter is applied to the raw channel data to isolate the cardiac frequency range, and the correlation between the two wavelengths is computed. This metric, called the scalp coupling index, ranges from -1 to 1, and higher values putatively indicate channels with more reliable signal.

Data are converted to relative oxygenated, deoxygenated, and total hemoglobin concentration measurements using the mes2hb function from the NIRS_SPM matlab toolbox [Ye2009]_, https://www.nitrc.org/projects/nirs_spm/). 

The oxy, deoxy, and total signals are downsampled by a factor of 10 (generally from 10 Hz to 1 Hz) after low pass filtering with cutoff frequency of 0.8 times the Nyquist frequency of the downsampled data. For typical data this step removes frequencies above about 0.4 Hz, which are expected to be noise or signals of no interest, and reduces the size of the data for faster processing later.

To remove abrupt transitions in the time series that are characteristic of quick head motions or other artifacts, a piecewise spline filter is applied. Abrupt transitions are identified as times where the signal amplitude changes in a single time point by greater than 3 standard deviations of the changes that are typical for the channel. Piecewise splines with knots placed every 30 seconds are used to fit a low frequency baseline in each segment between transitions, and these low frequency signals are removed. This method is rather similar to that of Scholkmann et al (2010), with some differences in how transitions are identified. For further information, several baseline correction methods have been compared by Cooper et al (2012).

To indicate whether important task- or stimulus-related signal was removed by the spline filter, it is also applied to the regressors created from the task or stimulus timing marks in the data file and presented for each channel along with the amount of variance retained.

Requirements
------------

Currently it reads Hitachi ETG-4000 format NIRS data files, which contain raw signals from two wavelengths at each channel.

Resources
---------

- CORRECTED_HBDATA - Filtered oxy / deoxy / total Hb concentration data. This is generally what will be wanted for future analysis.
- HBDATA - Unfiltered oxy / deoxy / total Hb data.
- OUTLOG - STDOUT and STDERR from the process on the grid.
- PBS - The DRMAA compliant batch script to run the job.
- PDF - The output PDF file for determining QA status.
- SNAPSHOTS - Thumbnail of the first page of the PDF for viewing on XNAT.
- MATLAB - Matlab script that was run.

References
----------

Cooper RJ, Selb J, Gagnon L, Phillip D, Schytz HW, Iversen HK, Ashina M, Boas DA. A systematic comparison of motion artifact correction techniques for functional near-infrared spectroscopy. Front Neurosci. 2012 Oct 11;6:147. doi: 10.3389/fnins.2012.00147. eCollection 2012. PubMed PMID: 23087603; PubMed Central PMCID: PMC3468891.

Pollonini L, Olds C, Abaya H, Bortfeld H, Beauchamp MS, Oghalai JS. Auditory cortex activation to natural speech and simulated cochlear implant speech measured with functional near-infrared spectroscopy. Hear Res. 2014 Mar;309:84-93. doi: 10.1016/j.heares.2013.11.007. Epub 2013 Dec 14. PubMed PMID: 24342740; PubMed Central PMCID: PMC3939048.

Scholkmann F, Spichtig S, Muehlemann T, Wolf M. How to detect and reduce movement artifacts in near-infrared imaging using moving standard deviation and spline interpolation. Physiol Meas. 2010 May;31(5):649-62. doi: 10.1088/0967-3334/31/5/004. Epub 2010 Mar 22. PubMed PMID: 20308772.

.. [Ye2009] Ye JC, Tak S, Jang KE, Jung J, Jang J. NIRS-SPM: statistical parametric mapping for near-infrared spectroscopy. Neuroimage. 2009 Jan 15;44(2):428-47. doi: 10.1016/j.neuroimage.2008.08.036. Epub 2008 Sep 12. PubMed PMID: 18848897.

Version History
---------------

 
Current Contact Person
----------------------

2017-06-28 Baxter Rogers baxter.rogers@vanderbilt.edu
	
