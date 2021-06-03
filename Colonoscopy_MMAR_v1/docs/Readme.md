# Description
A pre-trained model for volumetric (3D) segmentation of the liver and lesion in portal venous phase CT image.

# Model Overview
This model is trained using the runnerup [1] awarded pipeline of the "Medical Segmentation Decathlon Challenge 2018" using the AHnet architecture [2].

## Data
This model was trained with Liver dataset, as part of "Medical Segmentation Decathlon Challenge 2018".  It consists of 
131 labelled data and 70 unlabelled data.  The labelled data was partitioned, based on our own split, into
 104 training images and 27 validation images for this training task, as shown in config/dataset_0.json.

For more detailed description of "Medical Segmentation Decathlon Challenge 2018,"
please see 
http://medicaldecathlon.com/.

The training dataset is Task03_Liver.tar from the link above.

The data must be converted to 1mm resolution before training:

    tlt-dataconvert -d ${SOURCE_IMAGE_ROOT} -r 1 -s .nii.gz -e .nii -o ${DESTINATION_IMAGE_ROOT}

NOTE: to match up with the default setting, we suggest that ${DESTINATION_IMAGE_ROOT}
match DATA_ROOT as defined in environment.json in this MMAR's config folder.

## Training configuration
The provided training configuration required 12GB GPU memory.

Data Conversion: convert to resolution 1mm x 1mm x 1mm

Model Input Shape: dynamic

Training Script: train.sh


## Input and output formats
### Input:
 Single channel CT image
### Output:
 Three channels
 * Label 1: liver
 * Label 2: tumor
 * Label 0: everything else

## Scores
This Dice scores on the validation data achieved by this model are: 
1. Liver: 0.924
1. Tumor: 0.465

# Availability
In order to access this model, please apply for general availability access at
https://developer.nvidia.com/clara

This model is usable only as part of Transfer Learning & Annotation Tools in Clara Train SDK container.
You can download the model from NGC registry as described in Getting Started Guide.

# Disclaimer
The content of this model is only an example.  It is not intended to be a substitute for professional medical advice, diagnosis, or treatment. 

# References
[1] Xia, Yingda, et al. "3D Semi-Supervised Learning with Uncertainty-Aware Multi-View Co-Training." arXiv preprint arXiv:1811.12506 (2018). https://arxiv.org/abs/1811.12506.

[2] Liu, Siqi, et al. "3d anisotropic hybrid network: Transferring convolutional features from 2d images to 3d anisotropic volumes." International Conference on Medical Image Computing and Computer-Assisted Intervention. Springer, Cham, 2018. https://arxiv.org/abs/1711.08580.