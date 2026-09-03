# PKH Lab Project - Detecting calcium transients in fibroblasts with OpenCV

## Highlights
* Generates regions of interest (ROIs) in a fibroblast from fluorescent microscopy data
* Extracts calcium transients and traction force signals from ROIs
* Constructs a preliminary convolutional neural network (CNN) for identifying ROIs with mobile or immobile mitochondria

## Background
Many signaling pathways in the human body require calcium as a secondary messenger. Disruption of calcium in these pathways can contribute to maladies such as cancer and heart disease. Statistical and computational methods currently exist to track and predict calcium signals, specifically relating to its function in cell contraction. However, these models have not fully leveraged information in imaging data that could be observed through computer vision. This pilot project aims to utilize imaging data of fibroblasts treated with ATP to measure calcium signals and movement responses. Python’s OpenCV is implemented to process the data and extract signals, while PyTorch is used to construct a model to identify moving mitochondria. Signal extraction saw promising results for calcium transients and traction force signals, and a convolutional neural network achieved high accuracy in identifying cell regions with moving mitochondria, but with a limited sample size. Once the methods described here are refined and implemented into a larger systems model, calcium signals could be more thoroughly characterized through their effect on cell contraction.

## Methods Overview
* Create motion masks for consecutive frames in the cytosolic Ca channel TIF file to find hotspots of global motion
* Find centroids for each motion mask using cv2.moments()
* Cluster centroids across motion masks using sklearn's DBSCAN; get minimum and maximum coordinates for each cluster to get regions of interest for the cell
* Calculate the average pixel intensities for each ROI for the cytosolic Ca and mitochondrial Ca channels, and the max pixel intensity with a moving average for the traction force channels
* Assess average pixel intensity across frames to identify calcium transients with faceted subplots for each ROI
* Use saved ROIs to stack channels and train a CNN to classify ROIs as having mobile or immobile mitochondria

## Usage
### Key Package Dependencies
* NumPy
* pandas
* OpenCV
* Matplotlib
* scikit-learn
* PyTorch
  
### Running the Pipeline
These scripts require three TIF files as input: cytosolic calcium channel (561_registered.tif), mitochondrial calcium channel (488_registered.tif), and a traction force channel (traction_maps.tif). 

For each experiment/cell, the Gaussian blur in the creation of the motion masks, as well as the eps and min_samples parameters in the DBSCAN centroid clustering, may need adjustments to get the desired ROI size and number.

Running the script to extract calcium transients will save generated ROIs as {experiment}_rois.csv to be read into the CNN script.

## Figure Outputs
* {experiment}_mapped_rois.png: Displays the ROI centroids and bounding boxes on an example frame from the cytosolic channel. ROIs are labeled at the top left corner of the bounding box.
* {experiment}_avg_cyt_int.png: Displays ROIs, like in the mapped_rois.png, with the average pixel intensities for the cytosolic Ca channel across frames for each ROI.
* {experiment}_avg_tract_int.png: Similar to avg_cyt_int.png; displays the average pixel intensities for the traction force channel across frames for each ROI.
* {experiment}_avg_mit_int.png: Similar to avg_cyt_int.png; displays the average pixel intensities for the mitochondrial Ca channel across frames for each ROI.
* {experiment}_cyt_facet.png: Subplots for each ROI showing the average pixel intensity for the cytosolic Ca channel over time.
* {experiment}_tractma_facet.png: Subplots for each ROI showing the maximum pixel intensity for the traction force channel over time.
* {experiment}_mit_facet.png: Subplots for each ROI showing the average pixel intensity for the mitochondrial Ca channel over time.

## Citations
Bradski, G. (2000). The OpenCV Library. Dr. Dobb's Journal of Software Tools, 25, 120-125.

Fang, X., Bogdanov, V., Davis, J. P., & Kekenes-Huskey, P. M. (2023). Molecular Insights into the MLCK Activation by CaM. Journal of chemical information and modeling, 63(23), 7487–7498. https://doi.org/10.1021/acs.jcim.3c00954

Fang, X., Varughese, P., Osorio-Valencia, S., Zima, A. V., & Kekenes-Huskey, P. M. (2025). A Bayesian framework for systems model refinement and selection of calcium signaling. Biophysical journal, 124(14), 2347–2361. https://doi.org/10.1016/j.bpj.2025.06.010

Harris, C. R., Millman, K. J., van der Walt, S. J., Gommers, R., Virtanen, P., Cournapeau, D., ... & Oliphant, T. E. (2020). Array programming with NumPy. Nature, 585(7825), 357-362

Hunter, J. D. (2007). Matplotlib: A 2D graphics environment. Computing in Science & Engineering, 9(3), 90-95.

McKinney, W. (2010). Data structures for statistical computing in Python. In Proceedings of the 9th Python in Science Conference (Vol. 445, pp. 51-56).

Paszke, A., Gross, S., Massa, Francisco., Lerer, A., Bradbury, J., Chanan, G., ... & Chintala, S. (2019). PyTorch: An imperative style, high-performance deep learning library. Advances in Neural Information Processing Systems, 32, 8024-8035.

Pedregosa, F., Varoquaux, G., Gramfort, A., Michel, V., Thirion, B., Grisel, O., ... & Duchesnay, E. (2011). Scikit-learn: Machine learning in Python. Journal of Machine Learning Research, 12, 2825-2830.
