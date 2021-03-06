# sMRI_ChronicPain
 Anatomic Likelihood Estimate (ALE) Meta-Analysis of Structural Imaging Studies in Patients with Chronic Pain versus Healthy Controls


## Project Lead
Alina T. Henn

## Faculty Leads
Theodore D. Satterthwaite

## Analytic Replicator
Lennart Frahm
* Replication was performed using [uploaded scripts](https://github.com/alinahenn/sMRI_ChronicPain/tree/main/Henn_chronicPain_master) as well as [pyALE scripts](https://github.com/LenFrahm/pyALE), an ALE package based on Python

## Collaborators
Bart Larsen, Lennart Frahm, Anna Xu, Azeez Adebimpe, J. Cobb Scott, Sophia Linguiti, Vaishnavi Sharma, Allan I. Basbaum, Gregory Corder, Robert H. Dworkin, Robert R. Edwards, Clifford J. Woolf, Ute Habel, Simon B. Eickhoff, Claudia R. Eickhoff, Lisa Wagels

## Project Start Date
January 2020

## Current Project Status
:arrow_right: Paper entitled "Structural Imaging Studies of Patients with Chronic Pain: An Anatomic Likelihood Estimate Meta-Analysis" submitted at [*PAIN*](https://journals.lww.com/pain/pages/default.aspx), January 2022

## Datasets

1. Main analysis:
    - aberrant.xls
    - pain.xlsx
    - painCoords.xls
2. Feature-specific analysis: gray matter
    - aberrant_GM.xls
    - pain_GM.xlsx 
    - painCoords_GM.xls
3. Feature-specific analysis: cortical thickness
    - aberrant_CT.xls 
    - pain_CT.xlsx
    - painCoords_CT.xls
****************************************************  
4. Sensitivity analysis: Main analysis
    - aberrant_sensitivity_analyses.xls
    - pain_sensitivity_analyses.xlsx
    - painCoords_sensitivity_analyses.xls
5. Feature-specific analysis: gray matter
    - aberrant_GM_sensitivity_analyse.xls
    - pain_GM_sensitivity_analyses.xlsx 
    - painCoords_GM_sensitivity_analyses.xls
6. Feature-specific analysis: cortical thickness
    - aberrant_CT_sensitivity_analyses.xls 
    - pain_CT_sensitivity_analyses.xlsx
    - painCoords_CT_sensitivity_analyses.xls

## Path to Data on Filesystem
:arrow_right: [path](https://github.com/alinahenn/sMRI_ChronicPain/tree/main/Henn_chronicPain_master)

## Publication DOI
:arrow_right: following

## Pre-registration
* Registered on [PROSPERO](https://www.crd.york.ac.uk/prospero/display_record.php?RecordID=176498) on 23/01/2020
* ID: CRD42020176498	
* Title: Meta-Analysis of Structural Imaging Studies in Patients with Chronic Pain

# CODE DOCUMENTATION
The following describes all the steps that need to be performed for replication including set up, statistical main, feature-specific analyses and sensitivity analyses as well figure generation and result interpretation. 

## 1. Setup
The following software  is needed for the analyses:
* [MATLAB](https://www.mathworks.com/products/matlab.html)
* [SPM12](https://www.fil.ion.ucl.ac.uk/spm/software/spm12/)
* [MRIcron](https://www.nitrc.org/projects/mricron)
* [FSL](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FSL)

After you have downloaded the software, proceed as follows: 
1. Download [GitHub repo](https://github.com/alinahenn/sMRI_ChronicPain/tree/main/Henn_chronicPain_master).
2. Move the *spm12 folder* to the **dependencies folder**. 
3. Go to the folder **EickhoffALE**:
    - Create two new subdirectories and name them **DataMatlab** and **DataRaw**.
    - The entered data will be saved here later

If you are running the analyses on a Windows OS computer, please follow the next steps (otherwise go on to **2. ALE Meta-analyses**)
1. Download [Visual Studio for C++](https://visualstudio.microsoft.com/vs/features/cplusplus/)
2. The following Windows-specific documents are located in the **EickhoffALE** folder (they do not affect analyses performed using Linux or Mac OS):
    - *tfceMex_pthread.c*
    - *tfceMex_pthread.m*
    - *tfceMex_pthread.mexw64*
3. Before the actual ALE analysis, run the following commands in MATLAB:
    ```
    mex -setup
    mex 'tfceMex.c'
    mex 'tfceMex_pthread.c'
    ```
4. If you are using Windows OS you need a way to unpack **.gz** files. We recommend [WinRAR](https://winrar.de/downld.php) for this purpose.

***Everything is now prepared to run the ALE scripts!***

## 2. ALE Meta-analyses
+ Open the script *runALE.m* in MATLAB. 
    - You will need this script to perform the analyses. 
+ Total duration approximately 10 hours (at computer center (IZKF) RWTH Aachen University Hospital).

***Description and explanation of the commands in the runALE script:*** 
+ ```curPath=genpath(pwd)``` & ```addpath(curPath)```: 
    - Adds all dependencies to the main directory. 
+ ```cd ale```:
    - Takes you to the **EickhoffALE** folder so that analyses can be started.

### 2.1. Main analysis 
***:arrow_right: approximate duration: 5 hours (at computer center (IZKF) RWTH Aachen University Hospital)***  
+ ```ale_inputCoords('aberrant_all.xls')```: 
    - The coordinate data for the main analyses (aberrant structural changes) located in *data/aberrant_20210617.xls* are read in. 
    - Data will be converted to a .mat format for the analyses.
+ ```ale_inputCoords('painCoords_all.xls')```: 
    - Reads the coordinate data from the document *data/painCoords_20210617.xls* for the subgroup analyses regarding direction-specific group differences in structural data.
    - The coordinate data is read in .mat format for analyses and is located in ale/DataMatlab folder.
    - Description: 
+ ```ale_estimateALE('pain_all.xlsx')```
    - Starts the actual ALE analysis

### 2.2. Feature-specific analyses 
***:arrow_right: approximate duration: 5 hours (at computer center (IZKF) RWTH Aachen University Hospital)*** 
In the context of the subanalysis, the documents listed below are read in in an identical manner as already described in chapter 2.1. The only difference lies in the content and the name of the documents read in. 

**Feature-specific analysis gray matter**
*:arrow_right: approximate duration: 3.5 hours (at computer center (IZKF) RWTH Aachen University Hospital)*

+ ```ale_inputCoords('aberrant_GM.xls')```
+ ```ale_inputCoords('painCoords_GM.xls')```
+ ```ale_estimateALE('pain_GM.xlsx')```

**Feature-specific analysis cortical thickness**
*:arrow_right: approximate duration: 1.5 hours (at computer center (IZKF) RWTH Aachen University Hospital)*

+ ```ale_inputCoords('aberrant_CT.xls')```
+ ```ale_inputCoords('painCoords_CT.xls')```
+ ```ale_estimateALE('pain_CT.xlsx')```

### 2.3. Sensitivity analyses 
**Sensitivity analysis: Main analysis** 
*:arrow_right: approximate duration: 5 hours (at computer center (IZKF) RWTH Aachen University Hospital)* 
+ ```ale_inputCoords('aberrant_all_sensitivity_analysis.xls')```: 
+ ```ale_inputCoords('painCoords_all_sensitivity_analysis.xls')```: 
+ ```ale_estimateALE('pain_all_sensitivity_analysis.xlsx')```

**Sensitivity analysis: gray matter**
*:arrow_right: approximate duration: 3.5 hours (at computer center (IZKF) RWTH Aachen University Hospital)*
+ ```ale_inputCoords('aberrant_GM_sensitivity_analysis.xls')```
+ ```ale_inputCoords('painCoords_GM_sensitivity_analysis.xls')```
+ ```ale_estimateALE('pain_GM_sensitivity_analysis.xlsx')```

**Sensitivity analysis: cortical thickness**
*:arrow_right: approximate duration: 1.5 hours (at computer center (IZKF) RWTH Aachen University Hospital)*
+ ```ale_inputCoords('aberrant_CT_sensitivity_analysis.xls')```
+ ```ale_inputCoords('painCoords_CT_sensitivity_analysis.xls')```
+ ```ale_estimateALE('pain_CT_sensitivity_analysis.xlsx')```

### 2.4 Coding of the sources in the Excel tables:
+ *small letters (a,b,c)*: listed when different pain groups in the paper are compared with a healthy control group.
+ *Capital letters (A,B,C)*: listed when data for different features are listed in the paper.
   + A: gray matter
   + B: white matter
   + C: cortical thickness
   + D: cortical surface area
   + E: cortical volume
+ *Numbers (1,2)*: listed when a first author has published more than one paper in the same year.


## 3. Results
### 3.1. Description of output (ALE) folder 
The results of the analysis are stored in the **"ALE" folder** (Henn_chronicPain_master\EickhoffALE\ALE).

The following folders can be found in the ALE folder:

1. *Contribution*
    - empty: null results
    - format: text files (.txt)
    - contains gravity for significant clusters converging in structural changes  
    - contains %-contribution from each experiment to ALE
2. *Results*
    - format: NIfTI (.nii)
    - contains thresholded ALE maps: use map with suffix ***_cFWE05***: *p*<.05 cluster based family wise error corrected & ***_TFCE***: threshold free cluster enhancement
    - information: all maps are thesholded at voxel-hight *p*<.001 uncorrected and further cluster corrected
3. *Foci*
    - format: NIfTI (.nii)
    - contains foci images (0: regions without significant coordinate results; 1:regions with significant coordinate results)
4. *VolumsZ*
    - format: NIfTI (.nii)
    - contains Z-scored unthresholded ALE maps 
5. *NullDistributions*
    - format: matlab files (.mat) 
    - calculation of required cluster size (*k*) using cFWE at p < .05 using documents with the suffix *_clustP.mat*
        - Matlab code for the cut-off calculation ```NN = sort(NN(~isnan(NN)),'descend'); cut = NN(ceil(numel(NN)*.05))```
 
### 3.2. Figures
A detailed description of how to use MRIcron can be found here: [MRIcron Introducation](https://people.cas.sc.edu/rorden/mricron/main.html)
You have many possibilities to view the NIfTI documents or to generate images with MRIcron. In the following I will only describe how I generated the figures in the paper associated with the data so that you will be able to reproduce them. 

1. **open MRIcron**
2. **select  *OVERLY* :arrow_right: *ADD***
    - go to *Result*-folder within the ALE folder
    - select the NIfTI file you want to display
3. **select *WINDOW* :arrow_right: *MULTISLICES***
    -  You will be shown a series of slices of the currently open volumes.
4. **select *VIEW* :arrow_right: *ORIENT***
    - You can select whether the slices are displayed in sagittal, coronal or axial view
    - In the context of the paper, I have only shown the sagittal and axial view
5. **select *VIEW* :arrow_right: *SLICES***
    - You can specify the slices by means of numbers that you want to display in the multislice figure
    - In addition, you can define how far the slices should overlap in the image



## 4. Annotation
+ Please note that if you want to run the analysis again, you must first empty the **ALE** folder (where all results were saved). Otherwise, the analysis cannot run without errors. 
