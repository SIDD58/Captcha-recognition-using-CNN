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

### Results And Conclusion

After training the above model for 60 epochs, the following graph was obtained for loss with respect to the number of epochs as shown in figure 6. We see that as the number of epoch’s increases, the loss decreases exponentially. The loss at the end of 60 epochs is 0.5932. The loss obtained on training set is 0.2391 while the loss on test set is 2.123.

![epoch_loss](/Images/epoch_loss.JPG)

Next, we analyze how the accuracy obtained at each last dense layer varies with the number of epochs. The graph for accuracy of the output dense layers, namely dense layer 2,4,6,8 and 10 with respect to number of epochs is shown in figures 7,8,9,10,11. Thus we see that as the number of epochs increases, the accuracy of the layers improves and hence the system can predict the CAPTCHA more efficiently. The accuracy obtained after 60 epochs for dense layer 2 is 0.9897, dense layer 4 is 0.9794,  dense layer 6 is 0.9227, dense layer 8 is 0.8969 and for dense layer 10 is 0.9278.

![epoch_loss2](/Images/epoch_loss_2.JPG)
![epoch_loss4](/Images/epoch_loss_4.JPG)
![epoch_loss6](/Images/epoch_loss_6.JPG)
![epoch_loss8](/Images/epoch_loss_8.JPG)
![epoch_loss10](/Images/epoch_loss_10.JPG)


