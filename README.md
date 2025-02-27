# iSTSG
An improved spatiotemporal savitzky-golay (iSTSG) method to improve the quality of vegetation index time-series data on the Google Earth Engine

- link: https://ieeexplore.ieee.org/document/10843791
- You can cite our papers in the following format：
  > **GB/T 7714**   Wang W, Cao R, Liu L, et al. An improved spatiotemporal savitzky-golay (iSTSG) method to improve the quality of vegetation index time-series data on the Google Earth Engine[J]. IEEE Transactions on Geoscience and Remote Sensing, 2025.
  > **MLA**  Wang, Weiyi, et al. "An improved spatiotemporal savitzky-golay (iSTSG) method to improve the quality of vegetation index time-series data on the Google Earth Engine." IEEE Transactions on Geoscience and Remote Sensing (2025).
  > **APA**   Wang, W., Cao, R., Liu, L., Zhou, J., Shen, M., Zhu, X., & Chen, J. (2025). An improved spatiotemporal savitzky-golay (iSTSG) method to improve the quality of vegetation index time-series data on the Google Earth Engine. IEEE Transactions on Geoscience and Remote Sensing.

# Abstract
MODIS vegetation index (VI) time-series data are among the most widely utilized remote sensing datasets. To improve the quality of MODIS VI time-series data, most prior methods have focused on correcting negatively biased VI noise by approaching the upper envelope of the VI time series. Such treatment, however, may cause overcorrections on some true local low VI values, resulting in inaccurate simulations of vegetation phenological characteristics. Additionally, another challenge in reconstructing MODIS VI time series is to fill temporally continuous gaps. The earlier spatiotemporal savitzky-golay (STSG) method tackled this problem by utilizing multi-year VI data, but its performance heavily relies on the consistency of data across different years. In this study, we proposed an improved spatiotemporal savitzky-golay method (iSTSG). The new method accounts for the autocorrelation within the VI time series and fills missing values in the VI time series by leveraging spatiotemporal VI data from the current year alone. Furthermore, iSTSG incorporates an indicator to quantify potential overcorrections in the VI time series, aiming to more accurately simulate phenological characteristics. The experiments to reconstruct MODIS NDVI time-series product (MOD13A2) at four typical sites (a million square kilometers for each site) suggest two clear advantages in iSTSG over the iterative SG (called Chen-SG) and STSG methods. First, iSTSG more accurately reconstruct the annual NDVI time series, exhibiting smallest mean absolute differences (MAD) between the smoothed and the simulated reference NDVI time series (0.012, 0.018, and 0.020 for iSTSG, STSG, and Chen-SG); Second, iSTSG more effectively simulates phenological characteristics in the NDVI time series, including the onset dates for vegetation greenup and dormancy, as well as the crop harvest period. The advantages of iSTSG were also demonstrated when applied to the successor of MODIS, the Visible Infrared Imaging Radiometer Suite (VIIRS) VI time-series product (VNP13A1). iSTSG can be implemented on the Google Earth Engine, offering significant benefits for various applications, particularly in crop mapping and vegetation/crop phenology studies.


# How to use this open source code?
The open-source code is divided into **Google earth engine version (JS)** and **python version** (GEE version is more convenient, python version needs longer running time).

**The Google earth engine version is divided into two files: GEE_interpol and GEE_mian**

After logging in to the Google earth engine platform, the user needs to complete a required modification before running the filter main function GEE_mian.

- Required modification:
  - Store the linear interpolation function GEE_interpol in a Scripts code file. Then change the function call path ( line480 (require('users/Your_account_path/name_of_the_folder_where_you_store_the_interpol_file:Scripts_name_of_interpol_saved_in_the_folder');) ) according to where it is stored.

- Modification of optional parameters:
  > The user can change the ROI range and various parameters within the function. (Note that when modifying the SG filtering coefficient of STEP2, the filtering parameters corresponding to the window length and order need to be entered)

- Output file format:
  >  A multi-band tif image data with NDVI time series as the band.

**The python version of the code has only one file: PYcode**

The running environment is PyCharm Community Edition 2022.1.2
The python version accepts file input and requires input of MODIS data and quality label data when running the code.
The input file is .tif (it is necessary to open a time window and a space window, and the input data needs to be extended in time sequence and expanded in space).

- Accept input as:
  - A multi-band tif image data with NDVI time series as the band (for example, there are 23 single-band NDVI images in a year with 16-day time resolution, and the filtering window length needs to be extended by half the window length according to the filtering window length of STEP2, then the accepted input is a tif file with 29(23+3+3) bands).
  - A multi-band tif image data with the quality label time series as the band (for example, there are 23 single-band quality label images with a 16-day time resolution in one year, and the filtering window length needs to be extended by half the window length according to the filtering window length of STEP2, then the accepted input is a tif file with 29(23+3+3) bands).

- The spatial window size needs to be considered when dealing with grid boundaries:
  > The algorithm has the need of opening space window, and the filtering boundary (rowmin,rowmax,colmin,colmax) can be selected and controlled according to the demand and the size of space half window, so as to find enough similar pixels.
