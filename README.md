# MatLab-DeepLearning
Examples of Advanced Machine Learning on Matlab


## Transfer Learning Example Script

The code below implements transfer learning for the flower species example in this chapter. It is available as the script trainflowers.mlx in the course example files. You can download the course example files from the help menu in the top-right corner. You can find more information on this dataset at the [17 Category Flower Dataset](http://www.robots.ox.ac.uk/~vgg/data/flowers/17/index.html) page from the University of Oxford. 

Note that this example can take some time to run if you run it on a computer that does not have a supported GPU. 

### Get training images
```Matlab
flower_ds = imageDatastore('Flowers','IncludeSubfolders',true,'LabelSource','foldernames');
[trainImgs,testImgs] = splitEachLabel(flower_ds,0.6);
numClasses = numel(categories(flower_ds.Labels)); 
```
### Create a network by modifying AlexNet
```Matlab
net = alexnet;
layers = net.Layers;
layers(end-2) = fullyConnectedLayer(numClasses);
layers(end) = classificationLayer; 
``` 
### Set training algorithm options
```Matlab
options = trainingOptions('sgdm','InitialLearnRate', 0.001); 
 ```
### Perform training
```Matlab
[flowernet,info] = trainNetwork(trainImgs, layers, options); 
 ```
### Use trained network to classify test images
```Matlab
testpreds = classify(flowernet,testImgs);
```

## Transfer Learning Function Summary

### Create a network
| Function       | Description           | 
| ------------- |:-------------:| 
| alexnet      | Load pretrained network “AlexNet”| 
| supported networks     |View list of available pretrained networks     |   
| fullyConnectedLayer | Create new fully connected network layer      |
| classificationLayer | Create new output layer for a classification network     |

### Get training images
| Function       | Description           | 
| ------------- |:-------------:| 
| imageDatastore      | Create datastore reference to image files| 
| augmentedImageDatastore    |Preprocess a collection of image files     |   
| splitEachLabel| Divide datastore into multiple datastores      |
 
### Set training algorithm options
| Function       | Description           | 
| ------------- |:-------------:| 
| trainingOptions      | Create variable containing training algorithm options| 
  
### Perform training
| Function       | Description           | 
| ------------- |:-------------:| 
| trainNetwork      | Perform training| 

### Use trained network to perform classifications
| Function       | Description           | 
| ------------- |:-------------:| 
| classify     | Obtain trained network's classifications of input images| 

### Evaluate trained network
| Function       | Description           | 
| ------------- |:-------------:| 
| nnz     | Count non-zero elements in an array| 
| confusionchart    |Calculate confusion matrix    |   
| heatmap| Visualize confusion matrix as a heatmap     |

## Documentation
[Matlab DeepLearning Documentation](https://www.mathworks.com/help/deeplearning/index.html)



