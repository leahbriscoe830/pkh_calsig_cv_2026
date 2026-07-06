# PKH Lab Project - Detecting calcium transients in fibroblasts with OpenCV

## Background

## Methods
* Create motion masks for consecutive frames in the cytosolic Ca channel TIF file to find hotspots of global motion
* Find centroids for each motion mask using cv2.moments()
* Cluster centroids across motion masks using sklearn's DBSCAN; get minimum and maximum coordinates for each cluster to get regions of interest for the cell
* Calculate the average pixel intensities for each ROI for the cytosolic Ca, traction force, and mitochondrial Ca channels
* Assess average pixel intensity across frames to identify calcium transients with faceted subplots for each ROI

## Usage
