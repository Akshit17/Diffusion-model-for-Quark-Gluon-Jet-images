# ML4SCI DeepFalcon Tasks

This repository contains evaluation Common Task 1 listed [here](https://docs.google.com/document/d/1bwRaHc0IYIcFOokMcW-mYJv2i24iP1mm08ALTSyQ4EI/edit#)

Common Task 1: https://github.com/Akshit17/Variational-Autoencoder-for-Quark-Gluon-Jet-Event-Images

Common Task 2:  https://github.com/Akshit17/GNN-based-classification

Specific Task 2: https://github.com/Akshit17/Diffusion-model-for-Quark-Gluon-Jet-images

Applying for :- “Diffusion Models for Fast Detector Simulation” project

---
## Jet events reconstruction

#change this intro part as already written in VAE task
The accurate and efficient simulation of particle physics processes is crucial for the high-energy physics community, as simulating particle interactions in the detector is time-consuming and computationally expensive.  Jet event images reconstruction is needed to pave the way for full detector level fast simulation, as it can potentailly provide effective reconstruction of LHC events on the level of calorimeter deposits and tracks. 

#give bit background about diffusion models here

---
## Dataset
[Dataset](https://drive.google.com/file/d/1WO2K-SfU2dntGU4Bb3IYBp9Rh7rtTYEr/view?usp=sharing) given consists of four keys X_jets(image), m0(mass), pt(transverse momentum), y(labels for quark and gluon jet). 
Each image is 125x125 consisting of three channels Track, ECAL and HCAL respectively.

#### Combined channels image samples :-
![Combined channels samples](https://github.com/Akshit17/Variational-Autoencoder-for-Quark-Gluon-Jet-Event-Images/blob/master/assets/Combined_3channels_Samples.PNG?raw=true)

---

## Model building and training

#### Forward Process :-

![](.PNG?raw=true)

#### Backward Process :-

![](.PNG?raw=true)


## Discussion

* As dataset images contain physical data rather than RGB values seen in classical images, data preprocessing steps need to be carefully chosen to ensure that the physical properties of the data are not lost during the conversion process. For example, in our case, we had to be careful in scaling the pixel values to avoid losing the relative important features of the image.

*  Given the challenges with using classical image representations for physical data of quark/gluon jet events, alternative representations such as point clouds can be considered which can capture the spatial relationships between the points in a more natural way. 

*  Choice of beta scheduler is crucial, we used linear beta schedule and adjusted start and end values as per manual inspection of step wise forward processed images.

*  Another challenge was in visualizing the intermediate images generated at each step of the diffusion process. Normalization techniques had to be carefully choosen to obtain clear and informative visualizations.

*  For comparison of original and reconstructed events evaluation metrics like structural similarity index (SSIM), or peak signal-to-noise ratio (PSNR) can be used however in my case backward process didnt generate meaningful representations.

*  Further exploration and optimization to achieve high-quality diffusion models for physical data of quark/gluon represented as images is needed. More research is required to investigate different diffusion schedules, data pre-processing techniques, and other model architectures that can better capture the underlying features of the data.








