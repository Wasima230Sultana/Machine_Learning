
# ANN (MNIST) Quick Notes

> Load MNIST dataset here.

### Size of the dataset


|Variable | Meaning (Shape) |
 |--|--| 
 | X_train | Training images (60000, 28, 28)| 
 | y_train | Training labels (60000,)| | 
 | X_test | Test images (10000, 28, 28)|
  | y_test | Test labels (10000,)|

> 60000 training images.

> Each image has:

-   28 rows
    
-   28 columns
    

> `matshow()` displays the matrix as an image.

----------
# ANN (MNIST) Quick Notes

> Load MNIST dataset here.

### Size of the dataset

Variable

Meaning (Shape)

X_train

Training images (60000, 28, 28)

y_train

Training labels (60000,)

X_test

Test images (10000, 28, 28)

y_test

Test labels (10000,)

> 60000 training images.

> Each image has:

-   28 rows
-   28 columns

> `matshow()` displays the matrix as an image.

----------

## Normalize Data (Scaling)

> Neural networks learn better when numbers are small.

Training becomes:

-   Faster
-   More stable
-   More accurate

Before normalization

Pixels

```
0, 50, 120, 255
```

After dividing by 255

Pixels

```
0, 0.19, 0.47, 1.00
```

> Pixel values are now between **0 and 1** instead of **0 and 255**.

> `astype("float32")` converts integer pixel values into floating-point numbers because deep learning libraries work faster with floating-point values.

----------

## Input Layer

```
Input(shape=(28,28))
```

> Every input image has:

-   28 rows
-   28 columns

> It tells Keras the size of each input image.

----------

## Reshape (Flatten)

> A Dense neural network expects a **1-dimensional vector**, not a **2D image**.

> Convert each image:

```
28 × 28
      ↓
784
```

> Shape changes:

```
(60000, 28, 28)
          ↓
(60000, 784)
```

> `Input(shape=(28,28))` tells Keras the input image size.

> `Flatten()` converts the **2D matrix** into a **1D vector (784 features)**.

> **Only the shape changes. Pixel values remain the same.**

----------

## Sequential Model

> Sequential means layers are connected one after another.

```
Input
   ↓
Hidden
   ↓
Output
```

> Data flows only in the forward direction, so it is called a **Feedforward Neural Network (FFNN)**.

----------

## ReLU Activation Function

Formula

```
f(x)=max(0,x)
```

Example

```
Input : -5 → Output : 0

Input : 7 → Output : 7
```

Advantages

-   Fast
-   Simple
-   Prevents vanishing gradient
-   Most commonly used hidden-layer activation function

----------

## Dense Layer

> Dense means every neuron connects to every neuron in the previous layer.

> `Dense(128)` → Hidden layer with **128 neurons**.

> `Dense(64)` → Hidden layer with **64 neurons**.

> `Dense(10)` → Output layer with **10 neurons**, one for each digit.

```
0 1 2 3 4 5 6 7 8 9
```

----------

## Softmax Activation

> Softmax converts outputs into probabilities.

-   Every probability is between **0 and 1**.
-   All probabilities add up to **1**.
-   The largest probability becomes the predicted digit.

----------

## Compile

> Compile prepares the model for training.

### Optimizer = Adam

> Adam updates the model's weights after each mistake.

Advantages

-   Fast convergence
-   Stable learning
-   Works well for most deep learning problems

----------

### Loss Function

> The loss function measures **how wrong** the model's predictions are.

For MNIST with integer labels:

```
sparse_categorical_crossentropy
```

If labels are one-hot encoded:

```
categorical_crossentropy
```

----------

### Metrics

```
metrics=['accuracy']
```

> Accuracy = Percentage of correctly classified images.

----------

## Model Summary

```
model.summary()
```

Displays

-   Model architecture
-   Output shape of each layer
-   Number of trainable parameters
-   Total parameters

----------

## Training

```
history = model.fit(
    X_train,
    y_train,
    epochs=10,
    batch_size=32,
    validation_split=0.1
)
```

-   `X_train` → Training images (28 × 28)
-   `y_train` → Correct labels
-   `epochs=10` → The model sees the entire training dataset 10 times.
-   `batch_size=32` → The model learns from 32 images at a time.
-   `validation_split=0.1` → 10% of the training data is used for validation.

During training, the network repeatedly:

1.  Makes predictions.
2.  Compares predictions with true labels.
3.  Calculates the loss.
4.  Updates the weights using Adam.
5.  Repeats until the epoch finishes.

----------

## Evaluate

```
model.evaluate(X_test, y_test)
```

> Tests the trained model on unseen data.

Returns

-   Test Loss
-   Test Accuracy

----------

## Predict

```
model.predict(X_test)
```

> Predicts the probability of every digit (0–9) for each test image.

Output Shape

```
(10000,10)
```

Example

```
[0.01, 0.00, 0.02, ..., 0.95, ...]
```

----------

## argmax()

```
np.argmax(predictions[0])
```

> Returns the index of the largest probability.

Example

```
[0.01, 0.02, 0.90, 0.03, ...]

        ↓

Predicted digit = 2
```

----------

## Confusion Matrix

```
tf.math.confusion_matrix()
```

> Compares the **actual labels** with the **predicted labels**.

-   Rows → Actual labels
-   Columns → Predicted labels
-   Diagonal values → Correct predictions
-   Off-diagonal values → Incorrect predictions

A larger diagonal means better model performance.

----------

## ANN Architecture

```
28 × 28 Image
       │
       ▼
Input Layer
       │
       ▼
Flatten
(784 Features)
       │
       ▼
Dense(128)
ReLU
       │
       ▼
Dense(64)
ReLU
       │
       ▼
Dense(10)
Softmax
       │
       ▼
Prediction
```

----------

## Complete Flow

```
Load MNIST Dataset
        │
        ▼
Normalize Images
        │
        ▼
Build ANN Model
(Input → Flatten → Dense → Dense → Softmax)
        │
        ▼
Compile Model
        │
        ▼
Train Model
        │
        ▼
Evaluate Model
        │
        ▼
Predict Digits
        │
        ▼
Calculate Accuracy
```


# CNN (MNIST) Quick Notes

> Load MNIST dataset here.

----------

## Size of the Dataset

>#Like ANN
----------

# Normalize Data (Scaling)

> Neural networks learn better when numbers are small.

Training becomes:

-   Faster
-   More stable
-   More accurate

### Before normalization

Pixels

0, 50, 120, 255

### After dividing by 255

Pixels

0, 0.19, 0.47, 1.00

> Pixel values are now between **0 and 1** instead of **0 and 255**.

> `astype("float32")` converts integer pixel values into floating-point numbers because deep learning libraries work faster and more efficiently with floating-point values.

----------

# Add Channel Dimension

CNN expects **3D image data**.

Image format:

```
Height × Width × Channels
```

MNIST images are **grayscale**, so each image has **1 channel**.

### Before

```
(60000, 28, 28)
```

↓

### After reshape

```
(60000, 28, 28, 1)
```

```
X_train.reshape(-1, 28, 28, 1)
```

Explanation

-   `-1` → Automatically calculates the number of images.
-   `28` → Height
-   `28` → Width
-   `1` → One grayscale channel

----------

# Input Layer

```
Input(shape=(28,28,1))
```

Input image size:

-   Height = 28
-   Width = 28
-   Channels = 1 (Grayscale)

----------

# CNN Architecture

```
Input Image
      │
      ▼
Conv2D(32)
      │
      ▼
ReLU
      │
      ▼
MaxPooling2D
      │
      ▼
Conv2D(64)
      │
      ▼
ReLU
      │
      ▼
MaxPooling2D
      │
      ▼
Flatten
      │
      ▼
Dense(64)
      │
      ▼
Dense(10)
      │
      ▼
Prediction
```

----------

# Conv2D Layer

```
layers.Conv2D(32, (3,3), activation='relu')
```

> Convolution extracts important features from the image.

Examples of learned features

-   Edges
-   Lines
-   Curves
-   Corners
-   Shapes

----------

## Filters

```
Conv2D(32, ...)
```

Means:

-   The layer learns **32 different filters**.
-   Each filter detects a different feature.
-   Produces **32 feature maps**.

----------

## Kernel Size

```
(3,3)
```

A **3 × 3 kernel (filter)** slides across the image and detects patterns.

Example

```
Image

□□□□□
□□□□□
□□□□□
□□□□□
□□□□□

↓

3 × 3 Kernel

■■■
■■■
■■■
```

A kernel looks at one small region of the image at a time.

----------

# ReLU Activation

Formula

```
f(x) = max(0, x)
```

Example

```
Input : -8
↓
0
Input : 6
↓
6
```

Advantages

-   Fast
-   Simple
-   Prevents vanishing gradient
-   Most commonly used activation function

----------

# MaxPooling Layer

```
MaxPooling2D((2,2))
```

Pooling reduces the size of the feature maps while keeping the most important information.

Example

```
4   2

1   3

↓

4
```

The largest value is selected.

Advantages

-   Reduces computation
-   Reduces memory usage
-   Reduces overfitting
-   Keeps important features

----------

# Second Convolution Layer

```
Conv2D(64, (3,3), activation='relu')
```

Learns more complex features than the first convolution layer.

Examples

-   Curves
-   Circles
-   Digit shapes
-   Complex patterns

64 filters mean

```
64 Feature Maps
```

----------

# Flatten Layer

```
Flatten()
```

Converts all feature maps into a **1D vector**.

```
Feature Maps
↓
1D Vector
```

This vector becomes the input to the Dense layer.

----------

# Dense Layer

```
Dense(64, activation='relu')
```

Hidden layer containing

```
64 Neurons
```

Learns high-level patterns before classification.

----------

# Output Layer

```
Dense(10, activation='softmax')
```

MNIST contains

```
Digits
0
1
2
3
4
5
6
7
8
9
```
10 Classes
```

Softmax converts outputs into probabilities.

-   Every probability is between **0 and 1**.
-   All probabilities add up to **1**.
-   The highest probability becomes the predicted digit.

----------
```
# Compile

```
modelCNN.compile(...)
```

Compile prepares the CNN for training.

----------


## Optimizer

```
optimizer='adam'
```

Updates the model weights after each mistake.

Advantages

-   Fast
-   Stable
-   Most commonly used optimizer

----------

## Loss Function

```
loss='sparse_categorical_crossentropy'
```

Used because labels are integers.

Example

```
7
2
5
```

If labels are one-hot encoded, use

```
categorical_crossentropy
```

----------

## Metrics

```
metrics=['accuracy']
```

Accuracy

```
Correct Predictions-------------------Total Predictions
```

----------

# Model Summary

```
modelCNN.summary()
```

Displays

-   Model architecture
-   Output shape of each layer
-   Number of trainable parameters
-   Total parameters

Useful for checking whether the CNN is built correctly.

----------

# Training

```
historyCNN = modelCNN.fit(
    X_train,
    y_train,
    epochs=5,
    batch_size=32,
    validation_data=(X_test, y_test)
)
```

-   `X_train` → Training images
-   `y_train` → Correct labels
-   `epochs=5` → The model sees the complete training dataset 5 times.
-   `batch_size=32` → The model learns from 32 images at a time before updating its weights.
-   `validation_data=(X_test, y_test)` → Evaluates the model on the test dataset after each epoch to monitor performance.

During training, the CNN repeatedly:

1.  Extracts image features.
2.  Makes predictions.
3.  Calculates the loss.
4.  Updates the weights using Adam.
5.  Repeats until training finishes.

----------

# Evaluate

```
modelCNN.evaluate(X_test, y_test)
```

Tests the trained CNN on unseen images.

Returns

-   Test Loss
-   Test Accuracy

----------

# CNN Advantages

Compared to ANN

-   Automatically extracts image features.
-   Learns edges, curves, corners, and shapes.
-   Preserves spatial relationships between pixels.
-   Requires fewer parameters than a fully connected ANN.
-   Usually achieves higher accuracy for image classification.
-   More efficient for image data.

----------

# Complete CNN Flow

```
Load MNIST Dataset
        │
        ▼
Normalize Images
        │
        ▼
Add Channel Dimension
        │
        ▼
Build CNN
(Input → Conv → ReLU → Pool → Conv → ReLU → Pool → Flatten → Dense → Softmax)
        │
        ▼
Compile Model
        │
        ▼
Train Model
        │
        ▼
Evaluate Model
        │
        ▼
Predict Digits
```

----------

# ⭐ ANN vs CNN (Quick Revision)
| ANN | CNN |
|--|--|
| Uses Flatten layer |  Uses Convolution layer|
| Learns from all pixels directly |  Learns image features automatically|
| More parameters| Fewer parameters|
| Lower accuracy on images|  Higher accuracy on images|
| Best for tabular data |  Best for image data|
| Ignores spatial relationships |  Preserves spatial relationships|

----------

# ⭐ Exam Tip

**Q. Why is CNN better than ANN for image classification?**

**Answer:**

-   CNN automatically extracts important features (edges, lines, curves, corners, and shapes) using convolution filters.
-   It preserves the spatial relationship between neighboring pixels.
-   It requires fewer parameters than a fully connected ANN.
-   It usually achieves higher accuracy and trains more efficiently on image datasets such as MNIST.