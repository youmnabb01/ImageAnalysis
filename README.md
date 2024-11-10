# Cell Analysis: Ki-67 Intensity Measurement
## Description
This project involves analyzing microscopy images of U2OS cells to segment and analyze nuclei, as well as quantify the mean Ki-67 intensity in each nucleus. The images are acquired from a Nikon ND2 file and processed using several image processing techniques, such as Gaussian filtering, background subtraction, and thresholding. The primary focus is to evaluate the Ki-67 marker, which is widely used in cell biology to assess cell proliferation.
## Notebooks
- **Image Processing Notebook** (ABBOUD_HW_Image_Processing.ipynb):
This notebook handles the image processing steps required to segment the nuclei in the microscopy images.
It processes the images in the Hoechst channel (for nuclei detection) and Ki-67 channel (for quantifying Ki-67 intensity).
The steps involve Gaussian filtering, background subtraction, Otsu thresholding, and the labeling of detected nuclei.
The processed data is then saved as a CSV file containing the mean Ki-67 intensity values for each nucleus across different wells.

- **Data Analysis Notebook** ([ABBOUD_HW_Data_Analysis.ipynb]():
This notebook performs the data analysis on the output from the image processing step.
The CSV file containing the mean Ki-67 intensity data is loaded and grouped by well to calculate the average Ki-67 intensity for each well.
The data is reshaped to match the experimental conditions, and standard errors of the mean (SEM) are calculated.
Various models were then fitted to the data, including:
1. Linear Model
2. Exponential Model
3. Logarithmic Model
4. Square Root Model
   
The models were evaluated using the Sum of Squared Errors (SSE), both weighted (considering SEM) and unweighted.
The analysis concluded that the square root model provided the best fit for the data, although no clear plateau in the Ki-67 intensity with respect to FBS concentration was observed. This suggests that further studies and more complex models may be needed to better understand the relationship between FBS concentration and cell proliferation.

## Requirements
Before running the code, make sure you have the following Python libraries installed:
- matplotlib
- pandas
- numpy
- scipy
- skimage
- iaf (custom library)
## Usage
1. **Load the ND2 file**: The code reads a Nikon ND2 file using the NikonND2Reader from the iaf.io.readers module. Make sure to update the file path in the code to point to your ND2 file.
2. **Image Processing**:
The code processes each frame (well) in the ND2 file and extracts the Hoechst (nucleus) and Ki-67 channels.
Gaussian filtering is applied to smooth the images.
Background subtraction is performed using morphological opening.
Otsu's method is used for thresholding the nuclei from the Hoechst channel.
The separate_neighboring_objects function from iaf.morph.watershed is used to handle overlapping or neighboring nuclei.
3. **Measurement**: After segmentation, the number of segmented nuclei is counted.
The mean intensity of Ki-67 signal within each nucleus is calculated by masking the corresponding region in the Ki-67 channel.
4. **Results**:The number of segmented nuclei and their corresponding mean Ki-67 intensities are stored in a Pandas DataFrame.
The results are saved as a CSV file ki67_intensity_results_new.csv.
5. **Visualization**: The processed image can be visualized using imshow from the iaf.plot module.
## Results
The results file ki67_intensity_results_new.csv contains the following columns:
- **Well**: The index of the well/frame in the ND2 file.
- **Nucleus**: The label of the segmented nucleus.
- **Mean_Ki67_Intensity**: The mean intensity of the Ki-67 signal within the corresponding nucleus.
