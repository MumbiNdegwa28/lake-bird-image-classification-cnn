## Project Overview

This project focuses on building a multiclass image classifier to automatically identify **ducks, geese, and swans** from images.  
The classifier is based on a deep convolutional neural network (CNN) using transfer learning, trained on a labeled dataset of bird images, and evaluated on a separate held-out test set.  
The aim is to predict the correct bird species with high accuracy while handling class imbalance and visual similarity between classes.



## Model Architecture

The model uses **MobileNetV2** as a frozen feature extractor, with a custom classification head:

- **Input:** 224x224 RGB images  
- **Base:** MobileNetV2 pretrained on ImageNet (frozen)  
- **Classifier head:**  
  - GlobalAveragePooling2D  
  - BatchNormalization  
  - Dense(128) + ReLU + Dropout(0.5)  
  - Dense(3) + Softmax  

The model is compiled with:

- Optimizer: **Adam** (learning rate = 1e-4)  
- Loss: **Categorical cross-entropy**  
- Metric: **Accuracy**  



## Training

- **Epochs:** 30  
- **Data augmentation:** rotation, width/height shift, zoom, horizontal flip  
- **Validation split:** 20% of training data  
- **Early stopping:** monitor `val_loss`, patience=5  
- **Batch size:** 32  
- **Image size:** 224x224  

The training process applies real-time data augmentation to improve generalization and prevent overfitting.



## Evaluation

The trained model was evaluated on a held-out test set:

- **Overall accuracy:** ~83%  
- **Metrics computed:** Confusion matrix, precision, recall, and F1-score  
- **Observations:** The goose class shows the highest recall, while some confusion exists between ducks and geese due to visual similarity.



## Results

- **Training & validation accuracy:** stabilized at ~82–83%  
- **Loss curves:** decrease steadily, indicating stable learning and effective regularization  
- **Confusion matrix:** minor misclassifications between ducks and geese  
- **Class-wise metrics:** F1-scores indicate balanced performance across all classes  

Overall, the model generalizes well to unseen data and demonstrates effective use of transfer learning for multiclass image classification.
