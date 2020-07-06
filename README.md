# CAPTCHA Recognition using Convolutional Neural Networks

### Introduction:
CAPTCHAs may be referred to those infuriating images containing the text that needs to be typed in before a person can access a particular website. The full form of CAPTCHA is "Completely Automated Public Turing test to tell Computers and Humans Apart" and as the name suggests it is a way to avert the computer to fill out the form on its own, automatically. However using the concept of deep learning and computer vision, the very purpose of the CAPTCHAs can be defeated. This test can be passed automatically with the help of Convolutional Neural networks(CNN) - a class of the deep neural networks. A CNN is an algorithm of deep learning which takes in an image as input and then assigns some value to various features in the image which further helps to differentiate one feature from the other.

### Dataset Description:
The dataset used for this project consists of 1070 .png images of text based CAPTCHA. The dataset has been taken from https://www.researchgate.net/publication/248380891_CAPTCHA_dataset. Each dataset image is of 5 character set and the character set is defined as all English small letters and digits from 0 to 9. To train the model to read this CAPTCHA efficiently, 970 images are used for training purposes and the remaining 100 images are used for testing purposes. 

### Code:
![Workflow](/Images/Workflow.JPG)

### Data Preprocessing:
The dataset consists of images of size 50 height and 200 width. Each image consists of five letters consisting of small English alphabets (26) and digits (0-9 viz 10), thus making the total characters possible to 36. These images first need to be pre-processed before developing the model. For the purpose of training, the images in the dataset have a filename same as the CAPTCHA possessed by the image.
The images are first pre-processed by reading them in grayscale. This helps us to remove the noise to some extent as the images get invariant of the background color. The grayscale image consists of only one channel which makes it easier to further develop the model instead of using the three channels for RGB. Simultaneously, the file name is also stored in a string. From this filename, we drop the last four characters which are the “.png” characters containing the file extension, such that the remaining filename contains only the CAPTCHA. Now, if the length of this modified filename is less than six, it means that the CAPTCHA in the image does not have five characters and that particular image is not used further in the model.
Each grayscale image is then scaled and reshaped to the size: height- 50, width-200 and the number of channels as 1. Then we create an array of dimension 5*36(5 denotes the number of characters in the CAPTCHA and 36 denotes all the possible characters) for each image containing all entries as zeroes. This array is used to store the character present at each position in the CAPTCHA. At each position, through filename we find which characters are present at each position of the CAPTCHA and update the corresponding location to one in this array. This array will thus be used for training the model.
Thus, after pre-processing we obtain all the grayscale images and the target array containing information regarding the characters present in each CAPTCHA image
.
### Model Development

The model developed for this CAPTCHA dataset uses Convolutional Neural Network. It consists of a total twenty four layers comprising the input layer, convolutional layers, max pooling layers, dense layers, flatten layers and dropout layers. The total numbers of parameters is 1,818,196 where 1,818,132 parameters are trainable and 64 are non-trainable parameters. A brief architecture of the layers is depicted in figure.

![epoch_loss](/Images/Layers_Architecture.JPG)

The first layer is the input layer which takes the image of shape 50 height, 200 width and number of channels 1 as an input. The input layer is connected to the convolutional layer 1 which consists of 16 filters each of size (3,3) . The layer uses the stride of 1 and the padding is ‘same’ which means that padding is applied such that the output size and the input size is the same. The activation function deployed for this layer is ‘relu’. Relu is a rectified linear activation function which gives returns same as input if the input is positive else it returns zero. This convolutional layer 1 contains a total of 160 parameters. This layer transforms the shape from (50, 200, 1) to (50,200,16).  
The convolutional layer 1 is connected to the max pooling layer 1. The padding used is ‘same’. This layer chooses the most prominent feature thus reducing the computational size to (25, 100,16). This also helps to reduce over fitting. Followed by the max pool layer 1 is again a convolutional layer. This convolutional layer now uses 32 filters instead of 16 where each filter size is (3,3). The padding used is ‘same’ and the activation function is ‘relu’. The parameters trained in this layer are 4640 and this layer changes the shape by increasing the number of channels and yields the output as (25, 100, 32). Now, this convolutional layer is again followed by the max pooling layer 2 which has the same hyper parameters as max pool layer 1 and it reduces the dimensions to (13, 50, 32). This layer is again followed by the convolutional layer 3 which has the same hyper parameters as convolutional layer 2 and it does not alter the shape. The numbers of parameters in this layer are 9248.
The next layer is the batch normalization layer. This is used to improve the stability of the model. This layer is used to normalize the activations of the convolutional layer 3 at each batch. This layer uses a transformation in such a way that the mean activation is maintained close to zero and the activation standard deviation is close to one. The numbers of parameters trained in this layer are 128 and the shape is not altered. Following this layer is again a max pooling layer which uses padding as ‘same’ and changes the output shape to (7, 25, 32). 
After the max pooling layer, we have a flatten layer which converts the input from max pool layer to a long vector of 5600 dimensions. This is done so as the further neural network is easily processed and the back propagation is carried out easily. Further there are five dense layers in this neural network each of which is connected to the flatten layer. Each of these dense layers has the dimension 64 and deploys the activation function ‘relu’ to train a total of 358464 parameters each. Further to each of these dense layers is connected a dropout layer. The dropout layer drops 0.5 fraction of the nodes at the dense layer so that the model does not learn from the noise present in the dataset as well as the nodes probabilistically tries to learn from the inputs. Following the dropout layer is again a dense layer which uses the activation function ‘sigmoid’. The sigmoid function is also called a logistic function and it transforms the input to values between 0 and 1. The sigmoid function is a s-shaped curve such that as x approaches negative infinity, y approaches zero; as x approaches to infinity, y approaches one and at x equals to zero, y is 0.5. Each dense layer trains 2340 parameters and gives an output of dimension 36. All these layers and parameters are represented in tabular form in the figure.


![epoch_loss](/Images/Layers.JPG)

Thus, the model uses an image of dimension (50, 200, 1) as input and gets output from 5 layers each having dimension 36. The model uses the optimizer ‘Adam’ which is a stochastic gradient descent method that uses parameter learning rates based on the average of first moment and second moment of the gradients. The model uses loss function as ‘categorical cross entropy’. Categorical cross entropy is a version of Binary cross entropy which determines the variation between the targeted distribution and normal distribution. Categorical cross entropy is used when one sample has various classes or labels as in this case the character set consists of 36 labels.The metrics used is ‘accuracy’.
The dataset consists of 1070 sample images out of which 970 images have been used for training and the remaining images for testing purpose. Further, for training the model, a validation split of 0.2 is used which splits the training set such that 80% of the training data is used for training and the remaining 20% for testing. The batch size used is 32 which denote the number of samples per gradient update and the number of epochs used is 60. The results of this training are discussed in further sections.





### Results 

After training the above model for 60 epochs, the following graph was obtained for loss with respect to the number of epochs as shown in figure 6. We see that as the number of epoch’s increases, the loss decreases exponentially. The loss at the end of 60 epochs is 0.5932. The loss obtained on training set is 0.2391 while the loss on test set is 2.123.

![epoch_loss](/Images/epoch_loss.JPG)

Next, we analyze how the accuracy obtained at each last dense layer varies with the number of epochs. The graph for accuracy of the output dense layers, namely dense layer 2,4,6,8 and 10 with respect to number of epochs is shown in figures 7,8,9,10,11. Thus we see that as the number of epochs increases, the accuracy of the layers improves and hence the system can predict the CAPTCHA more efficiently. The accuracy obtained after 60 epochs for dense layer 2 is 0.9897, dense layer 4 is 0.9794,  dense layer 6 is 0.9227, dense layer 8 is 0.8969 and for dense layer 10 is 0.9278.

![epoch_loss2](/Images/epoch_loss_2.JPG)
![epoch_loss4](/Images/epoch_loss_4.JPG)
![epoch_loss6](/Images/epoch_loss_6.JPG)
![epoch_loss8](/Images/epoch_loss_8.JPG)
![epoch_loss10](/Images/epoch_loss_10.JPG)

Now, we predict the CAPTCHA. For predicting the CAPTCHA, we provide the image path and then the image is scaled. After that the model uses the image and then the output from the layers of model is mapped with the character set and the CAPTCHA is predicted. As a sample, an image from the dataset is passed to the model separately after renaming the file to some random name. The figure and the predicted CAPTCHA are shown

![output1](/Images/snippet1.JPG)


![output2](/Images/snippet2.JPG)

Thus, we see that our model predicts the CAPTCHA efficiently for small letters of English language and digits. 

### Conclusion:
CAPTCHA was designed to improve the security of the systems but deep learning algorithms defeated its very purpose. In this project, we used Convolutional Neural networks for CAPTCHA recognition. The dataset consisted of 1070 sample images and consisted of 5 lettered CAPTCHA. The model has been trained for CAPTCHA containing small English alphabets and digits, thus for a total of 36 characters. For training a purpose 970 samples have been utilized. The images in the dataset have been preprocessed and converted into grayscale for the further training. While training a convolutional neural network of twenty four layers has been developed consisting of input layer, convolutional layers, max pooling layers, flatten layer, dense layers and dropout layers. The model outputs five layers corresponding to each character of CAPTCHA and each has dimension 36 corresponding to the total number of characters possible. The model is trained using 60 epochs and it works well to predict any 5 lettered CAPTCHA containing small English alphabets and digits. The loss obtained after 60 epochs is 0.5932 and the accuracy of the output layers obtained is as dense layer 2 - 0.9897, dense layer 4 - 0.9794, dense layer 6 - 0.9227, dense layer 8 - 0.8969 and for dense layer 10 - 0.9278. The loss on training set is 0.2391 while the loss on test set is 2.123. The future scope of this work lies to expand this CAPTCHA recognition system for larger and more noisy CAP
TCHA containing all the symbols possible.  






