# Drum Classification
A Convolutional Neural Network, developed to classifiy different drum samples.

# Introduction

## Description
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

1. Vengeance Sample Packs (House, Electro Essentials, Trance Essentials, Minimal House, Trance Sensation Vol 4)
2. KSHMR sounds (Volume 1)
3. Freaky Loops Future Bass Sessions
4. Freshly Squeezed Samples - Dave Parkinson House Essentials 2
5. Laniakea Sounds Future Bass Waves
6. Production Master Lavish Future Bass
7. Surge Sounds Future Bass

Following is the distribution of my dataset:

<img width="398" alt="Screenshot 2023-02-13 at 5 58 33 PM" src="https://user-images.githubusercontent.com/55674300/218593428-15628d74-95b3-4d35-b062-29038d5a42ab.png">

## Feature Extraction
To make the data ready for the model, I pre-processed the samples using the librosa python package. First, I extracted the audio time series as an array and set all samples to have a sampling rate of 22.05kHz. Then, to ensure that each sample is of the same length (2 seconds), I either trimmed or added padding to all samples. I then used the audio time series vector to compute the Mel Frequency Cepstrum Coefficients (MFCCs). MFCCs are a feature widely used in automatic speech and speaker recognition. They capture certain features and represent the timbre of the signal and mimic how humans differentiate between different sounds. Then, I used a heatmap to plot the MFCCs as a function of time. Consequently, each input became an image.

# Model

## Model Architecture
I use a feedforward Convolutional Neural Network as my model. Since the input is an image representation of the audio sample, the problem becomes an image classification problem. It is well known that CNNs are state of the art when it comes to image classification, which is why I was motivated to use a CNN. After a lot of experimentation, Figure 1 represents my model architecture. My first layer is a convolutional layer with 16 filters with a kernel size of (3,3) and the activation as relu. This is followed by another convolutional layer with 32 filters and the same kernel size and activation function. I then added a MaxPooling layer to make the model invariant to local translation. To prevent overfitting and increase generalizationability, I added a dropout layer with a rate of 50%. Then, my next layer flattened the output which was then fed into a dense layer with 128 hidden units, followed by another dense layer with 64 and then finally the last layer that has 7 units constituting the probability of each class. The first two dense layers used relu as the activation function and were followed by dropout layers while the last layer used a softmax for classification purposes.

<img width="443" alt="Screenshot 2023-02-13 at 6 05 55 PM" src="https://user-images.githubusercontent.com/55674300/218594493-be6818dc-de31-4221-9f74-b70f1fc6eb62.png">

## Model Training
For my loss function, I used the categorical cross-entropy function as I was working with multiple classes and using a softmax function to assign probabilities to each class. I used Adam as my optimization function with a learning rate of 0.001 and used a batch size of 32. My dataset was split into a ratio of 0.8:0.1:0.1 as training, validation, and testing sets. I then trained the model for 100 epochs.

## Model Results
 After training the model for 100 epochs, I converged at a training accuracy of 85%, validation accuracy of 82%, and testing accuracy of 84%. The losses and accuracies are reflected in Figure 3. It could be observed that the model started to overfit on the data. I deduced this because the validation accuracy was bouncing between 80-82 whereas the training accuracy kept increasing.
 
<img width="893" alt="Screenshot 2023-02-13 at 6 09 53 PM" src="https://user-images.githubusercontent.com/55674300/218594980-b37ce16a-29b2-4dc3-b590-a62ab273ad5a.png">

Below, is the confusion matrix for predictions made on the test set.

<img width="820" alt="Screenshot 2023-02-13 at 6 10 38 PM" src="https://user-images.githubusercontent.com/55674300/218595082-4b5d126f-95d6-4c6b-b69b-3c6e3c1e30fb.png">

# Conclusion and Future Work
I successfully reached an accuracy of 83% on my testing set, and upon further investigation, I saw which classes lowered my model performance. As discussed above, most of the misclassification happened due to the subjectivity of how certain sample libraries classify sounds. The implication of this is extremely detrimental to supervised learning models, as the model can be misled by the subjective class labels in the training data.

Therefore, careful auditing of these samples must be done in the dataset to minimize this subjectivity. In other image classification applications, the labels are objectively decided and there is little room for interpretation. However, in our case, some libraries consider certain sounds as hi-hats, whereas others might label them as percussion. Furthermore, the addition of zero padding to all samples also serves as a hurdle in optimizing model performance. Instead of adding zero padding, I could pad the samples with the informative part of the tail. On the contrary, I may also cut all samples to 0.5 seconds, which would probably take care of the zero padding that presently constitutes most of the samples.
With all of the nuances mentioned above, I can still see that CNNs were able to classify most sounds with high accuracy. Future work could entail using a wider variety of features and using an unsupervised deep learning technique to classify sounds appropriately and without bias. The dataset could also go through further vetting, specifically the percussion class, which could be further classified into different classes.



