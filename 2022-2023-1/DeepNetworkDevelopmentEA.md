# Deep Network Development EA

# 2.L 2022.09.20

## Quiz

- After each 2 classes

## Linear regression with PyTorch

- Tim and Tom want's to find their expected life
- Load the Dataset to Python Pandas
- Find the most important features
  - BMI index and GDP
- Supervised learning
  - We have data and labels
  - Wee want to replicate the function
- Regression - predict the output
- Linear Regression - predict with linear function

  - h(x) = ^y = θx
  - Select the best θ
  - θ\* = argmin_θ J(θ)
  - ^y = θ₁\*x + θ₀

  - Vector format
    - X = [1, x₁, ...]
    - Θ = [θ₀, θ₁, ...]
    - Y = [y₁, y₂, ...]
    - Y = ΘᵀX
    - J(Θ) = (ΘᵀX-Y)ᵀ(ΘᵀX-Y)
    - Θ\* = (XᵀX)⁻¹(XᵀY)

- Different feature will give different model

  - Different result for life expectancy
  - Metrics for how good
    - Root Mean Squared Error

- New features

  - Tim:
    - BMI, Adult mortality, HIV
  - Tom:
    - GDP, Income, School
  - More feature, more theta values
  - 3 feature -> y = θ₃x + θ₂z + θ₁w + θ₀

- Data manipulation for removing dias

  - Data Normalization
    - All feature between 0 and 1
  - Data Standardization
    - Standardize values in different units

- Gradient Descent

  1. Select random θ
  2. θₜ = θₜ₋₁ - a▿J(θ)

  - PyTorch

# 3.L 2022.09.27

## Gradient Descendence

- Start with random θ
- Approximate the optimal Θ

## Artificial neural networks

### Biology

- Neuron has inputs and a output
- Similar structure, but different mechanism
- Fixed architecture in the artificial
  - Body can reorganize and create neurons and connections

### Artificial neuron

- x_j - the inputs
- w_j - the weights, parameters we will train
- b - bias parameter
- g - nonlinear activation function, eg.: sigmoid
- o - output
- Neuron mechanism:
  - o = g(∑ w_j\*x_j + b)
  - If o is not what we wanted, we use a loss function to change the weights
    - W = W - α(dE/)

### Training

- Select random weights
- With loss, we can train them for better weights

## Deep Neural Network

- Lot of layers of neurons
- Each layer can identify different features
- We expect the error to become smaller
- Separate training and test datasets
  - Train
  - Test if its good
  - Not test on the training set
- Hyper parameters:
  - Setup before training
  - Validation set, for changing hyper parameters
- Parameters:
  - Set during training

## Classification

### Binary classification

- Output is between 0 and 1
- Binary cross entrophy loss
  - L_BC(h(x),y) = -y log h(x) - (1-y) log(1-h(x))

### Multiclass classification

- Network has k output nodes
- Result is a k long vector
  - values between 1 and 0
  - values sum up to 1
- Softmax activation function
- Cross-entrophy loss
  - L(h(x),y) = -∑y_i log h_i(x)

## Convolutional Neural Networks

- Filters/kernel that parse the images and extract features
- Gives a smaller representation of a big data
- The filters aze also weights that we try to optimize and learn
- Padding is a edge problem solving technic
  - The sides of the picture are less scanned
  - We add a padding to the picture to extract features at the sides
  - Same padding - padding size that makes the output the size of the input
- Striding
  - How the filter is moving
- Output size can be calculated
  - n - image size
  - f - filter size
  - m - number of filters
- Pooling layer
  - Max pooling
    - extract the dominant value
- Inception / GoogLeNet
  - Not just sequential layers
  - Parallel layers
- Residual Network - ResNet
  - Connections maybe skip layers
  - Motive was to not lost features accidentally
- DenseNet
  - everything is connected, like in neural networks, but with convolutions
- MobileNet
  - Depthwise Separable Convolution
  - Filter for only one channel
  - Apply them separately
  - It is faster

# 4.L 2022.10.04

## Convolution

- Filter is param
- Padding is param
- Stride is param
- Filter/kernel size is a param

### ReLU

- flat zero
- 0 -> 0
- after linear raise

## Transfer Learning

- Traditional ML
  - Dataset
    - Different animals in pictures
    - New dataset of cat breeds
    - We need different models for different datasets
- Transfer Learning
  - Transfer knowledge to another model
  - **Backbone**
    - Major part of feature extraction
  - **Head**
    - Classification and special feature extraction
  - Heads are interchangeable, backbones transfer knowledge
  - Process called: **fine tuning**
  - Backbone can be freezed
  - Useful when:
    - A snd B tasks has common datasets
    - A is a specific version of B
    - you don't want to start with random weights

## Autoencoders

- Input is coded then decoded
- Only take the relevant features for the code
- Selfsupervised learning - output can be compared to the input
- Parts
  - Encoder
  - Latent space
  - Decoder
- Don't lose relevant information
- Not good for data compression
  - Lot of loss of data
- Create:
  - Feed forward neural networks
  - Convolutional networks
  - Recurrent neural networks
- How to train?

  - Input is the supervision for the output
  - Params
    1. Bottleneck size
    2. Number of layers
    3. Number of nodes per layer
    4. Reconstruction Loss
       - Too big can make overlearning

- Convolution
  - Important feature extraction
  - Noise reduction
    - Normal image -> Add noise -> Autoencoder -> compare the original image to the output

### Sparse autoencoders

- Zero out nodes
- Forces the network to learn the concepts not the actual function
- Distribute the learning to all the neurons

### Applications

- Data compression (feature compression)
- Remove the decoder
  - smaller representation
- Image segmentation
- Image generation
  - Learn features
  - Generate img from the features
- Use network instead od decoder and get useful data from big datasets

### Upsampling

- downsample then upsample
- After the upsampler can be used to upsample small images
- Pooling - unpooling
- Transposed Convolutions

# 5.L 2022.10.11

Will upload recording from prev semester.

## Auto encoders

- Recap
- Input data only, labels not needed
- Hyper parameters:
  - Bottleneck size
  - Number of layers
  - Number of nodes
  - Reconstruction loss
    - Not learn the exact function
- Convolutional AE
  - Convolutional layers
  - Pictures
- Denoising
  - Add noise in and try to recreate the input
- Sparse
  - Zero out certain nodes
  - Maximize the output
  - Distribute the learning
- Variational
  - Learn the data

## Upsampling

- Unpooling
  - Max unpooling
    - Save the max index
    - Not learning
- Transposed convolutions
  - Learnable function
  - Output size of convolution
    - (h+2p-f)/s + 1
  - PyTorch
    `conv1d = nn.Conv1D(in_channels=1, out_channels=1, kernel_size=3, stride=2, padding=0)`
  - Output size of trans. convolution
    - (h-1)\*s-2p+(f-1)+1
    - Apply the input to the filter, not the filter to the input
    - Stride means, we move in the output, not on the input
  - PyTorch
    `conv1d = nn.ConvTranspose1D(in_channels=1, out_channels=1, kernel_size=3, stride=2, padding=0)`
  - Padding
    - Conv
      - Add zeroes to the sides, than do the same
    - Trans Conv
      - Padding decrease the output size
      - Remove the padding cells

## Semantic segmentation

- Reconstruct an image by grouped pixels
  - Each pixel is part of a class
  - Every class has a color
  - Car is blue, road is pink, obstacle is red
- Labelling each pixel of the image
  - Channel for each class
  - Everything is 0 except where the class object is
  - What is in the pixel?
    - ArgMax
      - Which channel has the highest value in that pixel
- Naive Approach
  - Patch for every pixel
  - Classify the patch
  - The class will be the pixel's class
  - Lot of computation, lot of data
- Auto encoder structure
  - Try to learn the relevant features
  - Construct image from the features
- Fully convolutional network
  - Remove the final fully connected layer
- Single layer of transposed convolution
  - It is not high res enough for big pictures
- Sequential transposed convolutions
  - Un-pooling - not learnable
  - Small steps - not just un-pooling

# 6.L 2022.10.18

## Semantic segmentation

### U-Net

- Skip connections
- Upsampling
  - Gradually upscale
- Symmetric encoder and decoder
- Maxpooling
- Upsample to reverse maxpooling
- There are Advanced U-Net versions and

### Training

- Supervised
- Label masks for images
- Loss function is important
  - Pixel-wise cross entrophy loss
    - Average of pixel-wise divergence
    - Unballanced classes are a problem
  - Dice loss
    - $\ Dice = 2 \* \frac{|A∩B|}{|A|+|B|} $

## Object detection

- What and where
- Set of detected objects
  - Bounding box for the objects
- Multiple outputs is a problem
  - The result is not a percentage of classes
- Backbone feature extractor
  - Fully connected for classification
    - Softmax loss
  - Fully connected for bounding box
    - L2 loss
  - Weighted sum of losses is the final loss
- General number of objects
  - Naive
    - Slide a bounding box
    - Classify that part
    - Lot of computation
    - Bad
  - Region Proposal
    - Selective search
      - Group potential pixels
    - Classify those groups
    - One pass solution
    - 2 stage
      - R-CNN
    - 1 stage
      - YOLO, SSD

### R-CNN

- Selective search
- Extract regions - ~2k regions
- Compute CNN features
  - Resize regions to a standard size (AlexNet 224x224)
- Classify regions
  - Bounding box transformation back to the original image

### Fast R-CNN

- The whole image is given to the feature extractor ConvNet
- Then work from the feature map
- Selective search on the feature map
- Process only the regions of the feature map

### Faster R-CNN

- Remove the slow selective search and use some internal computations

# 7.L 2022.10.25

## Object detection 2

### Two stage detectors

- R-CNN, Fast and faster

#### Faster R-CNN

- **Region proposal network** instead of selective search
  - Tells if there is an object in the box
  - Transforms the box
- If there is a object -> another CNN will classify it

### Metrics

- Validate predictions
- IoU
  - Intersection over Union
  - Intersection of the ground truth and the prediction
  - 0.5 - bad
  - 0.7 - good
  - 0.9 - very good
- NMS
  - Non-max suppression
  - Many boxes for the same object
    - So we keep the highest of the overlapping boxes
    - Select form the big IoU overlapping boxes
      - Threshold is usually 0.7
- mAP
  - Mean average precision
  - Test
    1. NMS for all test images
    2. Average precision for all classes
    3. Mean of them
  - $ Precision = \frac{True positive?}{Positive?} $
  - $ Recall = \frac{True positive?}{Ground-truth?} $

### One stage detectors

- Modified RPN can do the classification

#### YOLO

- You only look once
- Dived images into cells
- Every cell has these annotations
  - [p, x, y, w, h, c₁, ..., cₙ]
  - p - probability of object in the cell
  - x, y - center of the object
  - w, h - width and height of object bounding box
  - c₁,..,cₙ - classification values

# 8.L 2022.11.08

## Instance segmentation and Human Pose estimation

- Semantic segmentation
  - If there are more of the same object, it will concatenate parts
  - Cannot give instances
- Object Detection
  - Now we have bounding boxes for instances
- We have to mix the above methods
- Things
  - Object categories which can be instanced
  - Countable
- Stuff
  - Cannot be separated to instances
  - Uncountable
- Instance segmentation can separate instances of things
- Panoptic Segmentation can separate anything (Now out of scope)
- Method based on faster R-CNN

  - Add a Semantic segmentation DNN to the end to create masks
  - Which pixel from the proposed region belongs to the object
  - Mask R-CNN
    - Conv
    - Region Proposal
    - ROI
    - Conv for mask, FC for class and box

- Human Key points

  - Add a new small Network to give the x,y points to the key points
  - Regression could solve this, but that is slow
  - Segmentation is faster
    - Every pixel is 0, except the key points and a small radius
    - Keypoint R-CNN

- Human pose estimation

  - Keypoints (Joints), pairs (Bones)
  - People can be different, can have different clothes, some parts are not visible, 3d depth ambiguity
  - Body models
    - Skeleton based model
    - Contour based model
    - Volume based model
  - OpenPose
    - 18 keypoints
  - MediaPipe
    - 32 keypoints
  - Single and Multi Pose methods
  - Top-down
    - Detect people
    - Estimate joints for them
  - Bottom-Up
    - Estimate joints
    - Group points into poses
  - OpenPose
    - 2D bottom-up multi-pose estimator
  - MediaPipe
    - 3D top-down single-pose estimator
    - Joint visibility data
    - Fast - 100 fps
    - Trained on exercises
  - MeTRAbs
    - 3D top-down multi-pose estimator
    - using YOLO

- Related tasks
  - Animal pose estimation
  - Hand pose estimation
  - Head pose estimation
  - Facial landmark detection

# 9.EA 2022.11.15

- Exam
  - Quizzes -> percent to grade
  - Assignment -> Weighted average
  - Mandatory part -> Like the assignments, failed or pass
    - If pass -> average of quizzes and assignments
  - Second part to improve grade or to take part in the Summer AI Lab
    - 1-3: Not affect the grade
    - 4: +1 for the grade
  - First part dates
    - Dec 13, 9-15, 1 hour
    - Dec 20
    - Jan 4

## Object detection (Recap)

- Two stage detectors
  - Fastest R-CNN - 4 loss
- One stage
  - Is this an object and which one is in one stage
  - YOLO
    - Separate to cells
    - Annotate cells
    - The center of the object which matters
  - Single shot detectors
    - Feature extraction
      - VGG without the fully connected
      - Smaller conv with smaller input output
      - 3x3 is the end
      - Extract features at different scales
    - Detection head
      - Heads for all the sizes
      - Scores and bounding boxes
    - NMS
      - Fuse heads output to create the final prediction

## Instance segmentation (Recap)

- Object detection and segmentation mask for each
- Faster R-CNN + Mask prediction = Instance segmentation

## Human pose estimation (Recap)

- Pose of the person with keypoints
- 2D and 3D (z is depth)
- Body models
  - Skeleton, contour, volume
- Single or multiple people
- Multi-pose can be
  - Top-down
    - Find people -> estimate pose
  - Bottom-up
    - Find points and create poses from them
- Keypoint R-CNN
  - Segment the keypoints

## Dept estimation

- Larger objects are closer
- Thing that move slower are further
- Stereo vision
  - The disparity of the object in the stereo cameras are smaller if its further away
- Lidar sensors can help to train networks

## Optical flow

- How objects move, picture to picture

# 11.EA 2022.11.22

- Last quiz next week
- Optional extra quiz
- Assignment 3 will open tomorrow
- Exam First part
  - Dec 6 - Lovarda
    - 3Pm - 4pm
    - 5pm - 6pm
  - January 3 - Lovarda
    - 3Pm - 4pm
    - 5pm - 6pm

## Recurrent Neural Networks

- Process sequential data
  - Like speech recognition
  - Sentiment classification
  - DNA sequence analysis
  - Machine translation
  - Video activity recognition
  - Name entity recognition
    - Vocab from the dataset, encode every word as a number
    - Each word can be represented with a vector: 0 in every dimension except the number of the word in the vocab
    - Model constraints
      - Handle variable length
      - Track long term dependencies
      - Keep the order of the data
      - Share parameters
    - Loop through the data and use the same model with more input from the prev iterations
      - $W_{ax}$ to the inputs
      - $W_{aa}$ to the input from the prev iteration
      - $W_{ya}$ to the output
    - Hidden state
      - $ a _ t = tanh( W _ {aa} a _ {t-1} + W _ {ax} x _ t + b _ a) $
    - Output vector
      - $ y _ t = tanh( W _ {ya} a _ t + b _ y) $
    - Back propagation is present to optimize loss
- RNN forms
  - one to one
  - one to many
  - many to one
  - many to many (same size or different size)

## Embeddings

- One hot vector can be huge with mostly 0 values
  - There is no relationship between words
- Word embedding
  - Represent words as features
  - Attributes for each word
  - Network is learning the words
    - Mostly Deep networks
- Before RNN there is embedding
  - This can improve the understanding of the data

## RNN Architectures

- Vanilla RNN
  - Input, input from prev, output and output to the next
  - Vanishing gradients
  - Short term dependency
- Long Short-term memory
  - Gates used to select what to remember and what to forget
  - Output of sigmoid controls the gate
  - Important memory will pass through
- Gate Recurrent unit
  - Merge the memory and the prev hidden state
- Bidirectional RNN
  - 2 separate RNN go through the data in the opposite direction
  - Combined result is the output
- Encoder - Decoder (Seq2Seq)
  - Sequence from a sequence
  - Translation, question answer
  - Encoder - Many to one
  - Decoder - One to many
  - Creates encoded sequence
    - Context vector
    - Create sequence from the context
  - Problems
    - Bottleneck
    - Context size
    - Can lose important information
    - Forget information

## Attention mechanism

- Context vector should include information from all timestamps

# 12.EA 2022.11.29

- Last quiz
- Final lecture is online
- Last assignment
- Exam
  - Network description
  - Implement the network
  - Implement one function
    - Forward, training, etc
  - No communications

## Recurrent Neural Networks

- Sequence of data
- RNN -> LST, GRU -> Bidirectional

## Attention mechanism

- Context vector should include information from all timestamps
- Direct connection from the input to the context vector **z**
- $ e _ i = attention _ {net}(y _ {i-1},h) \in \mathbb{R}^n _. $

## Image captioning

- Input is encoded with a CNN - get feature map
- Feature map is the context for the Attention Network
- Downside
  - Computational complexity

## Transformers prerequisites

- Attention + CNN
- Parallel processing
- Big matrix from the whole sentence - CNN on that "image"
- Self-Attention
  - Key, value, query
  - From the embedding matrix
  - Relationship in the input sequences
- A head learns a query ie: what is happening there? when it is happening?
- Multi-Head for more queries
  - Different relations between words

## Transformers

- Encoder
  - Multi-head self-attention -> forward neural network
- Decoder
  - Multi-head but only the queries
  - And the keys and values come from the encoder
  - Those are the context
  - What is the right question to ask to get the best key-values from the context
- Positional encoding
  - Where is the word in the sentence
- Skip connection and normalization blocks
- Linear and softmax at the end
- Train with incomplete sentences
