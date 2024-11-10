# Cell Analysis: Ki-67 Intensity Measurement
## Description
This project involves analyzing microscopy images of U2OS cells to segment and analyze nuclei, as well as quantify the mean Ki-67 intensity in each nucleus. The images are acquired from a Nikon ND2 file and processed using several image processing techniques, such as Gaussian filtering, background subtraction, and thresholding. The primary focus is to evaluate the Ki-67 marker, which is widely used in cell biology to assess cell proliferation.
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
