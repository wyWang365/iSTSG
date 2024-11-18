# iSTSG
An improved spatiotemporal savitzky-golay

In this study, we proposed an improved spatiotemporal savitzky-golay method (iSTSG). The new method accounts for the autocorrelation within the VI time series and fills missing values in the VI time series by leveraging spatiotemporal VI data from the current year alone. Furthermore, iSTSG incorporates an indicator to quantify potential overcorrections in the VI time series, aiming to more accurately simulate phenological characteristics.

The iSTSG method utilizes the same input data as Chen-SG method, specifically the VI time-series data for the current year only. The objectives of the iSTSG method are to more effectively address continuous data gaps in the VI time series and simulate vegetation phenological characteristics. The new method accomplishes the objectives by two main steps, which were illustrated in details in the following:
- Step 1 (generating initial VI estimates with autocorrelation of the VI time series)
- Step 2 (preserving phenological characteristics in the iterative SG filter)


# How to use this open source code?
The open-source code is divided into **Google earth engine version (JS)** and **python version** (GEE version is more convenient, python version needs longer running time).

**The Google earth engine version is divided into two files: GEE_interpol and GEE_mian**

Users can sign in to the Google earth engine platform and store the linear interpolation function GEE_interpol in a separate code file.
Filter main when running GEE_mian, it is necessary to change the function call route (require('users/Your_account_path/name_of_the_folder_where_you_store_the_interpol_file:interpol');), and the user can change the ROI range and various parameters in the function.



**The python version of the code has only one file: PYcode**

The running environment is PyCharm Community Edition 2022.1.2
The python version accepts file input and requires input of MODIS data and quality label data when running the code.
The input file is.tif (it is necessary to open a time window and a space window, and the input data needs to be extended in time sequence and expanded in space).

- Accept input as:
Single multi-band tif image data with NDVI time series as the number of bands (for example, there are 23 single-band NDVI images in a year with 16-day time resolution, and the filtering window length needs to be extended by half the window length according to the filtering window length of STEP2, then the accepted input is a tif file with 29(23+3+3) bands).

A single multi-band tif image data with the quality label time series as the number of bands (for example, there are 23 single-band tif images with a 16-day time resolution in one year, and the filtering window length needs to be extended by half the window length according to the filtering window length of STEP2, then the accepted input is a TIF file with 29(23+3+3) bands).

- The spatial window size needs to be considered when dealing with grid boundaries:
The algorithm has the need of opening space window, and the filtering boundary (rowmin,rowmax,colmin,colmax) can be selected and controlled according to the demand and the size of space half window, so as to find enough similar pixels
