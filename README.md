# Computer Vision CNN Classification for Golf Swing Sequencing
The objective of this project is to experiment with various Convolutional Neural Network (CNN) model architectures and hyperparameters to classify the sequence of a golf swing. This builds upon [previous work done by William McNally and his team that created the GolfDB dataset](https://github.com/wmcnally/golfdb) used for this project. Additionally, the
work of [Marc Marais](https://www.researchgate.net/profile/Marc-Marais/publication/358900228_Golf_Swing_Sequencing_using_Computer_Vision/links/621c81bb2542ea3cacb7149b/Golf-Swing-Sequencing-using-Computer-Vision.pdf) and the [Kaggle](https://www.kaggle.com/code/marcmarais/experiment-1-three-viewing-angles-only) code shared was extremely helpful in understanding how to get and process the images from the GolfDB dataset.

## Data and Processing
The [GolfDB](https://github.com/wmcnally/golfdb) dataset contains over 1,400 golf swing videos convering over 390,000 frames. These are labeled with event frames, bounding boxes, player names, sex, club type, and view type. These videos originated from YouTube videos 
and annotaters labeled 10 frames for each videos, signaling the events within the swing and drew boundary boxes to include the clubhead and golf ball for the entirety of the sequence. A sample of the csv file is shown below.

![](/images/_golfdb_data.png)

This analysis looks into finding the best performing model to classify the correct sequence of the golf swing. The first step is preprocessing the data from a video clip to a sequence of images. This step relied n the code shared from Marc Marais on [Kaggle](https://www.kaggle.com/code/marcmarais/experiment-1-three-viewing-angles-only).
Preprocessing the data begins with scaling the events to start at 0. Initially, the events start at a nonzero number (like 408) due to the movements before the swing starts. Once these are set to 0, all swings are starting at the same time, and eventually only eight of the 
events are included: 1) 'address', 2) 'toe-up', 3) 'mid-backswing', 4) 'top', 5) 'mid-downswing', 6) 'impact', 7) 'mid-follow-through', and 8) 'finish'. The images are then resized to 30x30 pixels as shown in these images below:

|![](/images/_golf_swing_1.png)|![](/images/_golf_swing_2.png)|
|:-:|:-:|


## Results
After running through 12 experiments that tested various CNN architectures and hyperparameters, the top performing model was a VGG model that incorporated data augmentated. This had two series of convolutional layers with the first layer set at 60 neurons and a kernel size of (3, 3) and a dropout rate of 0.5 throughout. The model had the best performance of all the models across validation and test loss and accuracy. Below are the 


![](/images/_golf_conf_matrix.png)
![](/images/golf_results.png)
![](/images/_golf_accuracy_loss.png)
