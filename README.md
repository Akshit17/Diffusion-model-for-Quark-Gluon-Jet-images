# ML4SCI DeepFalcon Tasks

This repository contains evaluation Common Task 1 listed [here](https://docs.google.com/document/d/1bwRaHc0IYIcFOokMcW-mYJv2i24iP1mm08ALTSyQ4EI/edit#)

Common Task 1: https://github.com/Akshit17/Variational-Autoencoder-for-Quark-Gluon-Jet-Event-Images

Common Task 2:  https://github.com/Akshit17/GNN-based-classification

Specific Task 2: https://github.com/Akshit17/Diffusion-model-for-Quark-Gluon-Jet-images

Applying for :- “Diffusion Models for Fast Detector Simulation” project

---
## Jet event images reconstruction

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






