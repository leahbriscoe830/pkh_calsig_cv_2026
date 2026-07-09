# PKH Lab Project - Detecting calcium transients in fibroblasts with OpenCV

## Background

## Methods Overview
* Create motion masks for consecutive frames in the cytosolic Ca channel TIF file to find hotspots of global motion
* Find centroids for each motion mask using cv2.moments()
* Cluster centroids across motion masks using sklearn's DBSCAN; get minimum and maximum coordinates for each cluster to get regions of interest for the cell
* Calculate the average pixel intensities for each ROI for the cytosolic Ca, traction force, and mitochondrial Ca channels
* Assess average pixel intensity across frames to identify calcium transients with faceted subplots for each ROI

## Usage
### Package Dependencies
* NumPy
* pandas
* OpenCV
* Matplotlib
* scikit-learn
  
### Running the Pipeline
This script requires three TIF files as input: cytosolic calcium channel (561_registered.tif), mitochondrial calcium channel (488_registered.tif), and a traction force channel (traction_maps.tif). 

For each experiment/cell, the Gaussian blur in the creation of the motion masks, as well as the eps and min_samples parameters in the DBSCAN centroid clustering, may need adjustments to get the desired ROI size and amount.

## Outputs
