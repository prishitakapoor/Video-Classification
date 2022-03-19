# Video-Classification
Complete guide to train a CNN capable of classifying videos

## About
Human Activity Recognition is a type of time series classification problem where you need data from a series of timesteps to correctly classify the action being performed.

## Dataset used :- 

## Video Classifications methods

### Method 1: Single-Frame CNN
We will run an image classification model on every single frame of the video and then average all the individual probabilities to get the final probabilities vector. This approach does perform really well.

### Method 2: Late Fusion
The Late Fusion approach, in practice, is very similar to the Single-Frame CNN approach but slightly more complicated. 
The only difference is that in the Single-Frame CNN approach, averaging across all the predicted probabilities is performed once the network has finished its work, but in the Late Fusion approach, the process of averaging (or some other fusion technique) is built into the network itself. Due to this, the temporal structure of the frames sequence is also taken into account.
Temporal Structure - spatial location of a current pixel and identifies at least one collocated reference pixel from a previous frame.
A Fusion layer is used to merge the output of separate networks that operate on temporally distant frames. It is normally implemented using the max pooling, average pooling or flattening technique.
This approach enables the model to learn spatial as well as temporal information about the appearance and movement of the objects in a scene. Each stream performs image (frame) classification on its own, and in the end, the predicted scores are merged using the fusion layer.

### Method 3: Early Fusion
This approach is opposite of the late fusion, as, in this approach, the temporal dimension and the channel (RGB) dimension of the video are fused at the start before passing it to the model which allows the first layer to operate over frames and learn to identify local pixel motions between adjacent frames.
An input video of shape (T x 3 x H x W) with a temporal dimension, three RGB channel dimensions, and two spatial dimensions H and W, after fusion, becomes a tensor of shape (3T x H x W).

### Method 4: Using CNN with LSTM’s
The idea in this approach is to use convolutional networks to extract local features of each frame. The outputs of these independent convolutional networks are fed to a many-to-one multilayer LSTM network to fuse this extracted information temporarily.

### Method 5: Using Pose Detection and LSTM
Use an off the shelf pose detection model to get the key points of a person’s body  for each frame in the video and then use those extracted key points and feed them to an LSTM network to determine the activity

### Method 6: Using Optical Flow and CNN’s
Optical flow is the pattern of visible motion of objects, edges and helps calculate the motion vector of every pixel in a video frame. It is effectively used in motion tracking applications. So why not combine this with a CNN to capture motion and spatial context in a video.

### Method 7: Using SlowFast Networks
Similar to the previous method this approach also has two parallel streams. One stream operates on a temporarily low resolution video compared to the other. All operations temporal and spatial are done in a single network.
The stream on top, called the slow branch, operates on a low temporal frame rate video and has a lot of channels at every layer for detailed processing for each frame. On the other hand, the stream on the bottom, also known as the fast branch, has low channels and operates on a high temporal frame rate version of the same video. 
Both streams are connected to merge the information from the fast branch to the slow branch at multiple stages.

### Method 8: Using 3D CNN’s / Slow Fusion
This approach uses a 3D convolution network that allows you to process temporal information and spatial by using a 3 Dimensional CNN. This method is also called the  Slow Fusion approach. Unlike Early and Late fusion, this method fuses the temporal and spatial information slowly at each CNN layer throughout the entire network.
A four-dimensional tensor (two spatial dimensions, one channel dimension and one temporal dimension) of shape H W C T is passed through the model, allowing it to easily learn all types of temporal interactions between adjacent frames.
A drawback with this approach is that increasing the input dimensions also tremendously increases the computational and memory requirements.
