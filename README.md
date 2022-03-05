# McMRSGUI
Multi-channel, magnetic resonance spectroscopy combination GUI.  
Summary: The McMRSGUI is a MATLAB-based graphical user interface that is utilized for evaluating and determining the proper multi-channel combination technique based on the spectra and additional information/scans that are available. A decision tree that is based on literature recommendations is available for the user to expedite the selection of the proper multi-channel combination between equal weighting, SNR weighting [1, 2], S/N2 [3], WSVD [4], WSVD+Apod [4], and AOC [5]. The program currently accepts Varian, .mat, and jMRUI text files as inputs. It can likewise export data files in .mat files for recording keeping of operations performed on data, or it can be exported in a jMRUI text format for quantification with jMRUI or other 3rd party software. It provides the user with several pre-processing steps: averaging, linebroadening, zero-padding, automatic/manual 0-order and 1st-order phasing, linewidth calculation, and viewing of spectra/free induction decays. 

Refer to the McMRSGUI User Manual for more detailed use of the program. 

McMRSGUI_final - Matlab AppDesigner GUI

McMRSGUI.exe - compiled GUI that can be used on any computer as long as version 9.11 (R2021B) of the Matlab RunTime is installed 
