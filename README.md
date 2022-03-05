# McMRSGUI
Multi-channel, magnetic resonance spectroscopy combination GUI.  
Summary: The McMRSGUI is a MATLAB-based graphical user interface that is utilized for evaluating and determining the proper multi-channel combination technique based on the spectra and additional information/scans that are available. A decision tree that is based on literature recommendations is available for the user to expedite the selection of the proper multi-channel combination between equal weighting, SNR weighting [1, 2], S/N2 [3], WSVD [4], WSVD+Apod [4], and AOC [5]. The program currently accepts Varian, .mat, and jMRUI text files as inputs. It can likewise export data files in .mat files for recording keeping of operations performed on data, or it can be exported in a jMRUI text format for quantification with jMRUI or other 3rd party software. It provides the user with several pre-processing steps: averaging, linebroadening, zero-padding, automatic/manual 0-order and 1st-order phasing, linewidth calculation, and viewing of spectra/free induction decays. 
Data Loading
The GUI has two main menus for loading of data: preprocessing data (Figure 1- left) and multi-channel combination (Figure 1- right). For the methods that don’t account for the phasing of the spectra (equal and SNR weighting), preprocessing of data to account for 0-order and 1st-order phases is necessary. Data can be loaded in via three different formats: 
1.	Matlab structure with the name “Starting.” The requisite fields and data types are shown in Figure 2. Note: Data is composed of free induction decay data in the matrix form (Num_channels x Num_acquisitions x Num_datapts).
2.	Varian format with the .fid folder organization.
3.	jMRUI TextFile format with subsequent acquisitions labeled below (Figure 3). Note: this method requires separation of channel data into different files as this format can only display multiple acquisitions. 
  
Figure 1. Data input loading options for pre-processing and multi-channel combination options.
 
Figure 2. “Starting” structure used to initially load in data into the pre-processing menu or data-combination.
 
Figure 3. jMRUI TextFile format for export option.

After the file is selected for the structure “Starting,” a dialog box will appear with the total number of channels for selection. Only one channel of data can be pre-processed at a time. Following the requisite pre-processing, the processed data will need to be saved through the “Export Matlab Data” button or the batch processing menu option, shown in Figure 5. This feature allows for the automatic or manual phasing to be set and quickly iterate through each channel. 
 
Figure 4. Individual channel selection for pre-processing.
 
Figure 5. Batch Process option becomes available after data is loaded into the program and will guide the user through a short series of questions.
Pre-processing features: 
1.	Number of averages – for data that requires averaging of acquisitions to obtain a higher SNR. This option applies a sliding window average of length determined by the user. 
2.	Line broadening (Hz) – best if used for visualization purposes only, as this cuts off high frequency noise and signal content by applying a decaying exponential function to the free induction decay. A “matched-filter” or filter with the same linewidth as that of the peak of interest can be applied to evaluate the highest achievable SNR. This function is not recommended for spectral quantification. 
3.	Zero-padding factor – Zeros can be added to the end of the free induction decay in the time domain to interpolate datapoints in the spectral domain. This gives an increased spectral resolution from the interpolation. Data sizes can quickly become large from this. 
4.	Manual and Automatic Phasing – Spectra can be manually or automatically phased using the bottom two sliders or the checkbox in the lower left of Figure 5. The automatic phase algorithm utilizes the maximum real peak as a starting guess for the correction of the spectra [6].
5.	The FID for an acquisition can be viewed, or subsequent spectra can be plotted in a cascade plot for visual evaluation of trends and metabolite progression over time. 
6.	The peak linewidth, phase, and SNR are incorporated through the default maximum peak calculation or through user-defined regions for signal and noise. 
7.	The units of the x-axis can be switched between MHz and parts-per-million interchangeability for easier isolation of compounds from known chemical shifts. The options are highlighted in Figure 8. 
8.	File subtraction is an included feature for removing macromolecule signals or baseline roll. Note: the subtraction file must be a single acquisition (1 x Num_datapts vector). 
 
Figure 6. X-axis adjustment options of MHz and parts-per-million.
 
Figure 7. The file subtraction function allows for a single file to be subtracted from a file to remove a macromolecule or baseline distortion.
The multi-channel combination load file’s tab allows either the Matlab structure “Starting” with multi-channel data (N_channels x N_acquisitions x N_data_pts) or the Matlab structure “Processed.”  The additional information stored within “Processed” comes from the pre-processing step where peak information, such as the SNR and linewidth can be calculated. All other pre-processing options are stored within “Processed” to help with data traceability. The overall structure of “Processed” is shown in Figure 8. Note: If the structure “Starting” is loaded with this option, the user will be prompted for a region selection for both the noise and the signal content before the program goes back and calculates the SNR-related parameters. 
 
Figure 8. Processed structure information that is stored by the program.
Data Combination Tree
Following successful data loading and/or preprocessing, the multi-channel MRS data will need to be combined in a manner based on the available SNR, additional information, and noise characteristics. The program will prompt the user for a noise region that will be used for the calculation of the noise correlation. Evaluation of the data correlation levels for noise correlation between channels will help to determine if certain methods can be disregards based on their foundational assumptions. The S/N2, S/N, and equal weighting all make the assumption that the channels are not correlated.  
 
Figure 9. Multi-channel spectroscopy combination method decision tree logic utilized within the McMRSGUI.
 
Figure 10. Decision tree for determination of noise correlation between channels.
Next, the program will prompt the user for any 1H unsuppressed data scaling factors, as shown in Figure 11. The unsuppressed water peak has a high SNR and better estimates the weighting coefficients between channels. Although this is not the sole factor in determining the complex weighting factors, it does play a significant role along with the noise correlation and covariance. Methods that utilize the 1H unsuppressed water scan typically better estimate the weighting factors at lower SNR when compared to their counterparts that don’t utilize it. Alternatively, a reference peak that is ever-present within the spectra can be utilized for obtaining complex weighting factors. 
 
Figure 11. Question dialog for determination of 1H data availability.
At this point, the recommended combination has either been selected or a question about whether the combined spectra is expected to be low is asked. The WSVD+Apod method performs better at lower SNR values due to the application of linebroadening for the estimation of the weighting factors. On the opposite side of the decision tree, the SNR weighting performs slightly better than the equal weighting for this scenario.   

Data Exporting
As previously mentioned, the “Export Matlab Data” button, shown in Figure 12, exports a structure named “Processed.” This stores all the associated pre-processing values utilized. Data that has been combined will also be exported within “Processed” with the selection and associated additional files recorded within the structure. Alternatively, the “Export jMRUI Data” button, shown in Figure 13, will export individual acquisition data within the jMRUI Textfile format from Figure 3. This data can then be loaded in to jMRUI for quantification.   
 
Figure 12. The "Export Matlab Data" button exports the loaded data and any associated pre-processing or combination steps for traceability.
 
Figure 13. The “Export jMRUI Data” button exports individual acquisition data within a jMRUI Textfile format.

Resetting of the Program
To reset the GUI, the “Clear Data” button, shown in Figure 12, clears the memory of the main structure used to pass data between functions and resets the graphs. 
 
Figure 14. The clear button cleans out the information stored within the app structure.
Accompanying Programs for Simulations
1.	McMRSGUI_MonteCarlo_data_simulation_creation_file.m – script utilized to create 8-channel data with correlated noise for distortion simulation.
2.	McMRSGUI_noise_covariance_creation_file.m – script that can be utilized for creating a noise covariance file for the WSVD method. An example covariance matrix produced by the code is shown in Figure 15. Alternatively, a text file (.txt) can be created with a single row of headers and then a comma-separated matrix of size Num_channel x Num_channel of the covariance values (Figure 16).
 
Figure 15. Example complex covariance matrix of size Num_channels x Num_channels.
 
Figure 16. Example covariance matrix shown in the .txt format
3.	McMRSGUI_Read_jMRUI_for_S_N2_peak_amplitudes.m – script that loads in jMRUI AMARES results that were saved as a .txt file. The fitted amplitude values are then saved in the proper format for use with the McMRSGUI for the S/N2 combination method reference peak amplitudes. An example of the weighting factors is shown in Figure 17. Alternatively, a text file (.txt) can be saved with a single row header and then a comma separated (Num_channel x Num_acquisitions) matrix of the weights.

 
Figure 17. Weighting factors for S/N2 method saved in a Num_channel x Num_acquisitions matrix.
 



References
[1]	L. L. Wald, S. E. Moyher, M. R. Day, S. J. Nelson, and D. B. Vigneron, "Proton spectroscopic imaging of the human brain using phased array detectors," Magn Reson Med, vol. 34, no. 3, pp. 440-5, Sep 1995, doi: 10.1002/mrm.1910340322.
[2]	S. M. Wright and L. L. Wald, "Theory and Application of Array Coils in MR Spectroscopy," NMR in Biomedicine, vol. 10, pp. 394-410, 1997.
[3]	E. L. Hall, M. C. Stephenson, D. Price, and P. G. Morris, "Methodology for improved detection of low concentration metabolites in MRS: optimised combination of signals from multi-element coil arrays," Neuroimage, vol. 86, pp. 35-42, Feb 1 2014, doi: 10.1016/j.neuroimage.2013.04.077.
[4]	C. T. Rodgers and M. D. Robson, "Coil combination for receive array spectroscopy: Are data-driven methods superior to methods using computed field maps?," Magn Reson Med, vol. 75, no. 2, pp. 473-87, Feb 2016, doi: 10.1002/mrm.25618.
[5]	M. Wu, L. Fang, C. E. Ray, Jr., A. Kumar, and S. Yang, "Adaptively Optimized Combination (AOC) of Phased-Array MR Spectroscopy Data in the Presence of Correlated Noise: Compared with Noise-Decorrelated or Whitened Methods," Magn Reson Med, vol. 78, no. 3, pp. 848-859, Sep 2017, doi: 10.1002/mrm.26504.
[6]	Y. Xi and D. M. Rocke, "Baseline correction for NMR spectroscopic metabolomics data analysis," BMC Bioinformatics, vol. 9, p. 324, Jul 29 2008, doi: 10.1186/1471-2105-9-324.

