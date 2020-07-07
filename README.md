# CAPTCHA Recognition using Convolutional Neural Networks

### Introduction:
CAPTCHAs may be referred to those infuriating images containing the text that needs to be typed in before a person can access a particular website. The full form of CAPTCHA is "Completely Automated Public Turing test to tell Computers and Humans Apart" and as the name suggests it is a way to avert the computer to fill out the form on its own, automatically. However using the concept of deep learning and computer vision, the very purpose of the CAPTCHAs can be defeated. This test can be passed automatically with the help of Convolutional Neural networks(CNN) - a class of the deep neural networks. A CNN is an algorithm of deep learning which takes in an image as input and then assigns some value to various features in the image which further helps to differentiate one feature from the other.

### Dataset Description:
The dataset used for this project consists of 1070 .png images of text based CAPTCHA. The dataset has been taken from https://www.researchgate.net/publication/248380891_CAPTCHA_dataset. Each dataset image is of 5 character set and the character set is defined as all English small letters and digits from 0 to 9. To train the model to read this CAPTCHA efficiently, 970 images are used for training purposes and the remaining 100 images are used for testing purposes. 

### Model Development:
The model is developed using Convolutional Neural Network for detecting the Captcha present in the image. For this purpose, the training sample dataset is first pre-processed and then the model is developed consisting of twenty four layers.
<p align="center">
<img src="/Images/Workflow.JPG" alt="Workflow" width="200"/>
 </p>
#### Data Preprocessing:
The dataset consists of images of size 50 height and 200 width. These images first need to be pre-processed before developing the model. For the purpose of training, the images in the dataset have a filename same as the CAPTCHA possessed by the image. The images are first pre-processed by reading them in grayscale. This helps us to remove the noise to some extent as the images get invariant of the background color. Simultaneously, the file name is also stored in a string.
Each grayscale image is then scaled and reshaped. Then we create an array of dimension 5*36, used to store the character present at each position in the CAPTCHA. At each position, through filename we find which characters are present at each position of the CAPTCHA and update the corresponding location to one in this array. This array will thus be used for training the model.Thus, after pre-processing we obtain all the grayscale images and the target array containing information regarding the characters present in each CAPTCHA image
.
#### Model Development

The model developed for this CAPTCHA dataset uses CNN. It consists of a total twenty four layers comprising the input layer, convolutional layers, max pooling layers, dense layers, flatten layers and dropout layers. The total numbers of parameters is 1,818,196 where 1,818,132 parameters are trainable and 64 are non-trainable parameters. A brief architecture of the layers is depicted in figure.
<p align="center">
<img src="/Images/Layers_Architecture.JPG" alt="Layers" width="50%"/>
 </p>
The first layer is the input layer which takes the image as input. Then we have convolutional layers and the max pooling layers which extracts the most prominent feautures from the images. The next layer is the batch normalization layer, used to improve the stability of the model.Then we have a flatten layer which converts the input from max pool layer to a long vector of desired dimensions. This is done so as the further neural network is easily processed and the back propagation is carried out easily. Further there are five dense layers in this neural network each of which is connected to the flatten layer. Each of these dense layers deploys the activation function ‘relu’ to train the parameters. Further to each of these dense layers is connected a dropout layer used for regularisation. Following the dropout layer is again a dense layer which uses the activation function ‘sigmoid’. The sigmoid function is also called a logistic function and it transforms the input to values between 0 and 1. 

Thus, the model uses an image of dimension (50, 200, 1) as input and gets output from 5 layers each having dimension 36. The model uses the optimizer ‘Adam’. The model uses loss function as ‘categorical cross entropy’. 

### Results 

After training the model for 60 epochs, the following graph was obtained for loss with respect to the number of epochs. We see that as the number of epoch’s increases, the loss decreases exponentially. The loss at the end of 60 epochs is 0.5932. The loss obtained on training set is 0.2391 while the loss on test set is 2.123.

<p align="center">
<img src="/Images/epoch_loss.JPG" alt="epoch_loss" width="50%"/>
 </p>
Next, we analyze how the accuracy obtained at each last dense layer varies with the number of epochs. The graph for accuracy of the output dense layers, namely dense layer 2,4,6,8 and 10 with respect to number of epochs is shown in figures 7,8,9,10,11. Thus we see that as the number of epochs increases, the accuracy of the layers improves and hence the system can predict the CAPTCHA more efficiently. The accuracy obtained after 60 epochs for dense layer 2 is 0.9897, dense layer 4 is 0.9794,  dense layer 6 is 0.9227, dense layer 8 is 0.8969 and for dense layer 10 is 0.9278.
<p align="center">
<img src="/Images/epoch_loss_2.JPG" alt="epoch_loss_2" width="50%"/>
</p>
<p align="center">
<img src="/Images/epoch_loss_4.JPG" alt="epoch_loss_4" width="50%"/>
</p>
<p align="center">
<img src="/Images/epoch_loss_6.JPG" alt="epoch_loss_6" width="50%"/>
</p>
<p align="center">
<img src="/Images/epoch_loss_8.JPG" alt="epoch_loss_8" width="50%"/>
 </p>
<p align="center">
<img src="/Images/epoch_loss_10.JPG" alt="epoch_loss_10" width="50%"/>
 </p>



Now, we predict the CAPTCHA using the trained model.

<p align="center">
<img src="/Images/snippet1.JPG" alt="snippet1" width="50%"/>
</p>

<p align="center">
<img src="/Images/snippet2.JPG" alt="snippet2" width="50%"/>
</p>

Thus, we see that our model predicts the CAPTCHA efficiently for small letters of English language and digits. 

### Conclusion:
CAPTCHA was designed to improve the security of the systems but deep learning algorithms defeated its very purpose. In this project, we used Convolutional Neural networks for CAPTCHA recognition. The dataset consisted of 1070 sample images of which 970 samples have been utilized for training purpose . The images in the dataset have been preprocessed and converted into grayscale for the further training. While training a convolutional neural network of twenty four layers has been developed. The model outputs five layers corresponding to each character of CAPTCHA. The model is trained using 60 epochs and it works well to predict any 5 lettered CAPTCHA. The loss obtained after 60 epochs is 0.5932 and the accuracy of the output layers obtained is as dense layer 2 - 0.9897, dense layer 4 - 0.9794, dense layer 6 - 0.9227, dense layer 8 - 0.8969 and for dense layer 10 - 0.9278. The loss on training set is 0.2391 while the loss on test set is 2.123. The future scope of this work lies to expand this CAPTCHA recognition system for larger and more noisy CAPTCHA containing all the possible symbols.  

## Learn more about our model and its working at
[Our blog](https://medium.com/@manvi./d191ef91330e)






