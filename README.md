# ML4SCI DeepFalcon Tasks

This repository contains evaluation Common Task 1 listed [here](https://docs.google.com/document/d/1bwRaHc0IYIcFOokMcW-mYJv2i24iP1mm08ALTSyQ4EI/edit#)

Common Task 1: https://github.com/Akshit17/Variational-Autoencoder-for-Quark-Gluon-Jet-Event-Images

Common Task 2:  https://github.com/Akshit17/GNN-based-classification

Specific Task 2: https://github.com/Akshit17/Diffusion-model-for-Quark-Gluon-Jet-images

Applying for :- “Diffusion Models for Fast Detector Simulation” project

---
## Jet events reconstruction

The accurate and efficient simulation of particle physics processes is crucial for the high-energy physics community, as simulating particle interactions in the detector is time-consuming and computationally expensive.  Jet event images reconstruction is needed to pave the way for full detector level fast simulation, as it can potentailly provide effective reconstruction of LHC events on the level of calorimeter deposits and tracks. 

For this particular task Diffusion model was used. Diffusion models are a type of generative models that work by destroying training data by adding noise and learn to recover the data by reversing this noising process. They have proved to be good at capturing the underlying structure of complex data like image and audio. The process of diffusion can be thought of as two steps: a forward process and a backward process. In the forward process, the model takes the input image and gradually "blurs" it to generate a series of new images until it becomes completely unrecognizable. In the backward process, the model takes the last image in the series (which is completely unrecognizable i.e pure noise) and gradually "unblurs" it to generate a series of new images that become progressively clearer. The goal of the backward process is to generate an image that is as close to the original input image as possible. 

---
## Dataset
[Dataset](https://drive.google.com/file/d/1WO2K-SfU2dntGU4Bb3IYBp9Rh7rtTYEr/view?usp=sharing) given consists of four keys X_jets(image), m0(mass), pt(transverse momentum), y(labels for quark and gluon jet). 
Each image is 125x125 consisting of three channels Track, ECAL and HCAL respectively.

#### Combined channels image samples :-
![Combined channels samples](https://github.com/Akshit17/Variational-Autoencoder-for-Quark-Gluon-Jet-Event-Images/blob/master/assets/Combined_3channels_Samples.PNG?raw=true)

---

## Model building and training

#### Forward Process :-

The forward process of diffusion models can be thought of as a Markov chain, where the current state depends only on the previous state. In this case, the current state is the image at time t, denoted as x_t, and the previous state is the image at time t-1, denoted as x_{t-1}. Each image at step t would be progressively more noisy than image at step t-1, determined by the new mean and variance using this equation :-  

![t-1_image](./assets/forward_process_t-1_eqn.PNG?raw=true)

Noisy version of image for specific time t can also be calculated by pre calculating closed form of mean and variance based on cummulative variance schedules which boils above equation to this :-

![image](./assets/forward_process_eqn.PNG?raw=true)

For q/g events it would be like this :-

![forward process sample images](https://github.com/Akshit17/Diffusion-model-for-Quark-Gluon-Jet-images/blob/master/assets/forward%20process.PNG?raw=true)

#### Backward Process :-

The backward process is an important component of DDPM that allows us to sample from the learned probability distribution. It consists of two main parts: the noise scheduling and the reverse diffusion process. The noise scheduling is responsible for generating noise vectors that are used during the reverse diffusion process. 
Model tries to learn probability density of earlier timestamp given the current timestamp as follows :-
![](./assets/backward_process_eqn.PNG?raw=true)

The reverse diffusion process is where we actually generate the samples from the learned probability distribution. It uses a U-Net architecture, takes the noise vectors generated by the noise scheduling as input and uses them to predict the values of the latent variables at each step in the reverse diffusion process. By iterating this process backwards through the diffusion steps, we can generate a sample from the learned probability distribution.

![UNET](./assets/unet_ARCH.png?raw=true)

## Discussion

* As dataset images contain physical data rather than RGB values seen in classical images, data preprocessing steps need to be carefully chosen to ensure that the physical properties of the data are not lost during the conversion process. For example, in our case, we had to be careful in scaling the pixel values to avoid losing the relative important features of the image.

*  Given the challenges with using classical image representations for physical data of quark/gluon jet events, alternative representations such as point clouds can be considered which can capture the spatial relationships between the points in a more natural way. 

*  Choice of beta scheduler is crucial, we used linear beta schedule and adjusted start and end values as per manual inspection of step wise forward processed images.

*  Another challenge was in visualizing the intermediate images generated at each step of the diffusion process. Normalization techniques had to be carefully choosen to obtain clear and informative visualizations.

*  For comparison of original and reconstructed events evaluation metrics like structural similarity index (SSIM), or peak signal-to-noise ratio (PSNR) can be used however in my case backward process didnt generate meaningful representations.

*  Further exploration and optimization to achieve high-quality diffusion models for physical data of quark/gluon represented as images is needed. More research is required to investigate different diffusion schedules, data pre-processing techniques, and other model architectures that can better capture the underlying features of the data.

## References

* Denoising Diffusion Probabilistic Models :- https://arxiv.org/pdf/2006.11239.pdf

*  https://github.com/lucidrains/denoising-diffusion-pytorch

*  https://colab.research.google.com/github/huggingface/notebooks/blob/main/examples/annotated_diffusion.ipynb#scrollTo=a30368b2

*  https://medium.com/mlearning-ai/enerating-images-with-ddpms-a-pytorch-implementation-cef5a2ba8cb1



