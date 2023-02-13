# Drum_Classification
 Classifying percussion samples using CNNs

# Description

In recent decades, music production has progressively experienced a tectonic shift. This shift is
best described by the ease of access of professional quality sounds, coupled with the
advancement in Digital Audio Workstation (DAWs) that enable music hobbyists to produce
professional soundtracks using their personal computers. Easily accessible sound packs come
with studio recorded or professionally synthesized instruments that allow producers to simply
drag and drop samples onto their DAWs and manipulate them as they please. Consequently, most
producers end up with a wealth of different samples, which can quickly become tedious to
organize.

## Motivation
As mentioned above, a producer's sound library can exponentially grow and reach thousands of
different instrument samples. Manually going through such samples can quickly get very tedious,
especially if the sample packs in question are poorly organized. This poses an opportunity to
automate such a task, specifically when the audio data is poorly labelled. The motivation behind
such a classification task is to help group similar sounds together, so that the user can easily
select sounds that they are looking for. The development of a Machine Learning model can then
be deployed in the form of a plug-in which may have a GUI similar to that of a bubble graph.
This has the potential to further streamline the music production pipeline and make
it more desirable and faster to complete soundtracks.

## Problem Description
The aim is to implement a deep learning model that can classify drum samples into its respective
categories. I restrict myself to drum samples because if a model can learn to differentiate
within an instrument, it can easily differentiate between different sounding instruments. To
classify these drum samples, I must first extract meaningful features from the audio clips that
the network can be trained on. In recent years, there has been a lot of work involving deep neural
networks in the audio domain such as Automatic Speech Recognition (ASR), Music Genre
Classification and Automatic Music Generation to name a few. Many of these applications
perform some sort of feature extraction that the neural network can work with. These features
may include information about the pitch, tone, loudness etc. which the model can then use to
classify different sounds.

# Dataset
The dataset I used for this project was my personal own collection of samples that I've gathered over the years. Following are some of the libraries I included:

● Vengeance Sample Packs (House, Electro Essentials, Trance Essentials, Minimal House, Trance Sensation Vol 4)
● KSHMR sounds (Volume 1)
● Freaky Loops Future Bass Sessions
● Freshly Squeezed Samples - Dave Parkinson House Essentials 2
● Laniakea Sounds Future Bass Waves
● Production Master Lavish Future Bass
● Surge Sounds Future Bass

Following is the distribution of my dataset:
<img width="398" alt="Screenshot 2023-02-13 at 5 58 33 PM" src="https://user-images.githubusercontent.com/55674300/218593428-15628d74-95b3-4d35-b062-29038d5a42ab.png">


 
