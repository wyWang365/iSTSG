# iSTSG
An improved spatiotemporal savitzky-golay

In this study, we proposed an improved spatiotemporal savitzky-golay method (iSTSG). The new method accounts for the autocorrelation within the VI time series and fills missing values in the VI time series by leveraging spatiotemporal VI data from the current year alone. Furthermore, iSTSG incorporates an indicator to quantify potential overcorrections in the VI time series, aiming to more accurately simulate phenological characteristics.

The iSTSG method utilizes the same input data as Chen-SG method, specifically the VI time-series data for the current year only. The objectives of the iSTSG method are to more effectively address continuous data gaps in the VI time series and simulate vegetation phenological characteristics. The new method accomplishes the objectives by two main steps, which were illustrated in details in the following:
- Step 1 (generating initial VI estimates with autocorrelation of the VI time series)
- Step 2 (preserving phenological characteristics in the iterative SG filter)
