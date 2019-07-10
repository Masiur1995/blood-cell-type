# Blood-cell-identification


## Problem Statement

When an antigen enters the human body, the body responds with white blood cells. In the case of allergies, there is an immediate response of basophils however, in the case of an inflammation, there is an immediate response of neutrophils. Using a convolutional neural network, a model was constructed to help identify the type of blood cell from a certain microscopic image of the cell. This model would aid research, students, and even doctors when looking for infections, allergies, or inflammations.

## Executive summary

### Loading and describing Data

There are two datasets that are loaded. The original dataset consists of images of five different cell types (Neutrophils, Eosinophils, Neutrophils, Basophils, and Lymphocytes). These images are in jpeg and xml files along with labels that correspond to the cell-class of the images. There are 367 images in this dataset. In the second dataset, there are a total of approximately 10,000 images in the train dataset (2500 for each cell type) and approximately 2,400 images in the test dataset (600 for each cell type). Although the second dataset is more augmented with images, it consists of one less class; there are no basophils in this dataset.

### Exploratory Data Analysis

##### Exploring the original Dataset
The labels csv file within the original dataset was used to construct a dataframe. A few rows in the dataframe with labels had two identifications with a comma in between. Since the label was given two identifications, those rows were dropped. The cleaned dataframe was then be used to count the number of objects within the classes. When executing a value count on these objects, the data was very imblanced. Value counts of the objects were translated into a bar graph. Here in this bar graph, it is very evident that the data is extremely imbalanced.

![Imbalanced Classes in first dataset](Imbalanced Classes.jpg)

##### Exploring the augmented dataset
This dataset had a lot more images however, it only had 4 classes (eosinophils, neutrophils, lymphocytes, and monocytes). In trying to check for imblanaced classes between the four white blood cell types, a dataframe was constructed with each white blood cell's class. After doing a value count, there were approximately 25% of each class; this is indicative of balanced classes.

[Balanced classes in augmented dataset](Balanced Classes.jpg)


### Pre-Processing

These images had to be resized into a (30,30) format so when being trained, the process was more efficient. The number of samples in the train dataset were also condensed from 10,000 images to 4,000 for efficiency (1000 for each blood cell type). After both of these steps were done, the image was finally ready to be converted into an array. Turning our X-variable into an array of arrays for which the images were, we now had an array of pixels that ranged from 0-255. To standardize this wide range of pixel values in the arrays, we divided our X-values (both train and set) by 255. Our y-values were the four classes of white blood cells we are trying to distinguish. These values also had to be standardized because a range of values were distributed between 0-3 (numpy is 0-indexed). This was going to intefere with our model because one class might hold more weight than another class just for being labeled 3 for class 3. Using keras' to categorical package, these hot vectors were converted into labels. The same concept was applied to the z-variables. We are now ready to input our data into a convolutional neural network!

### Modeling

There are three layers in a convolutional neural network; the convolutional layer, the pooling layer, and dense layers. The convolutional layer was instantiated as sequential. In the convolutional layer, the filter size was 32, the kernel size was (3,3), and the activation function here was relu. The pooling layer was then set up as (2,2). There were two of these convolutional layers in the model. The pooling layer consisted of a pool size of (2,2). In attempting to decrease chances of the model being overfit, a dropout layer was added with a value of 0.25. Following the filtering and pooling, the model was then flattened. The dense layers were next added to the model. The dense layer prior to the output layer has 128 layers and an activation function of relu. Another dropout layer was added with a value of 0.5. Then came the final layer with four output neurons for the four classes. The activation function used here was softmax since this is a multi-classification problem.
When compiling the model, the loss function used was categorical crossentropy. Adadelta was used as the optimizer and the metric measured was accuracy. Following compiling the model, an image data generator was implemented to further train the data. With a run through 80 epochs, the accuracy of the model was relatively high.

## Conclusion

With the use of hyperparameter tuning in convolutional neural networks, the model has proved to be accurate when identifying the class of a given white blood cell. There can always be better accuracy scores produced. For further modeling, I plan to incorporate my Z data which identifies between mononuclear and polynuclear. 
