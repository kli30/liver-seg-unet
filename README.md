# Liver segmentation with unet+resnet
<p>Performs liver segmetnation with neural networks, specificly, with UNet and a pre-trained encoder using resnet. 
<p>liver images as described in this <a href='https://arxiv.org/pdf/1702.05970.pdf'>research paper</a>.</p>

## Datasets
The raw data is in nifti format (nii.gz), is from <a href='https://www.dropbox.com/s/8h2avwtk8cfzl49/ircad-dataset.zip?dl=0'>here</a>, and is put under folder data/{train,test}/nii/.

The program first convers slices of 3D nifti images into 2D png images (each slice corresponds to a png image), for easy data augmentation.

### Training, validation, and testing datasets
There are 20 subjects in total, 18 of them will be used for training and validation, resulting in ~1980 slices/images for training and 494 images for validation.
Two subjects (349 slices/images) will be used for independent testing.
An example batch from training dataset: 
<p align="center"><img src="img/batch.png" style></img></p>


## Model and trainning
<p>The neural network is build on the fastai platform with unet_learner. The encoder of the unet is a pretrained resnet34 neural network. Context information of a hirachical layer is used in the corresponding layer of the decoder through hook mechanism. </p>
<p>Loss function: CrossEntropyLossFlat</p>
<p align="center"><img src="img/loss.png" style></img></p>
 

## Segmentation performance
<a href='https://en.wikipedia.org/wiki/S%C3%B8rensen%E2%80%93Dice_coefficient'>Dice coefficient</a> was used for evaluation. 

## Results
Validation dataset, dice coefficient: 97.2%; 
<p align="center"><img src="img/prediction.png" style></img></p>

Independent testing dataset: dice coefficient: 95.2%; 
<p align="center"><img src="img/test.png" style></img></p>

## TODOs: 
1. Testing time augmentation.
2. Imbalance of liver/non-liver tissues.