# Note
- The complete dataset folder used in the Jupyter notebooks will not be uploaded as the file sizes are too large already. Only the csv files for the image data that has gone through FFT are in the dataset folder.
- To obtain the original dataset, please download it from:https://data.mendeley.com/datasets/5y9wdsg2zt/2
- The pretrained models are also quite large and hence was uploaded to my Google Drive, please download from here: https://drive.google.com/drive/folders/14yXcx0uEnvMSRJ0rQDtmyFWXSgQR9pH1?usp=sharing

# Problem Statement
- Build a classifier model that can **reliably and accurately detect cracks** in typical concrete surfaces.
- Cracks in  concrete are one of the most common defects, and has in the past required manual inspection.
- Areas where it is inaccessble/hard to access for humans can instead use crack recognition and classification technology.

# Executive summary
**Data pre-processing**
- Image dataset taken from https://data.mendeley.com/datasets/5y9wdsg2zt/2
- Image in RGB format of size 227 x 227
- Dataset contains 40,000 images, split equally between Class 0 (no cracks) and Class 1 (cracks)
- Dataset was shuffled and split into train and test set, then saved as hp5y files


**Model construction**
- Initially, a CNN model was constructed. The initial CNN model performed badly. The 2nd one performed significantly better with tuned hyperparemeters. It was deemed a validation accuracy of ~0.98 was good enough.
- It was realized that the CNN model performed badly on thin and narrow cracks.
- The image data was pre-processed using Fast Fourier Transform (FFT) and azimuthal averaging to reduce data dimensionality, so that machine learning classification models could be constructed.
- Generally, there were 2 scenarios which commonly resulted in misclassification:
    - Surfaces with many small craters led to models misclassifying the image as Class 1
    - Surfaces with very thin and narrow cracks led to models misclassifying the image as Class 0
    
**Model prediction on unseen data**
- It was found that in general the machine learning models were better at detecting thin and narrow cracks as compared to the CNN model.
- A meta classifier (voting classifier) model was constructed to increase reliability in detecting small cracks
    - Pockmarked surfaces were still a problem, however this was deemed more desirable than unreliable detection of small cracks (i.e. higher recall was more desirable compared to specificity)
    
# Conclusion
- Models constructed were able to detect obvious cracks with very high degree of accuracy
- CNN model unable to detect thin/small cracks, but machine learning models are quite good at this
- Machine learning models tend to misclassify Class 0 surfaces with certain characteristics (variations in color/pockmarked surfaces), whereas CNN model is relatively good at picking up these nuances
- Meta classifier (voting classifier) used to increase reliability

**Limitations**
- Generally, 2 scenarios that caused misclassification:
    - Thin, narrow cracks
    - Surfaces with a lot of small craters
- Cracks are only 1 type of defect

**Future work**
- Extend to other types of defect