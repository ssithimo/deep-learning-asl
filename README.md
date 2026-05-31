# 🤟 Deep Learning ASL Recognition

> *36 hand gesture classes, 3 architectures, 1 clear winner. VGG16 correctly classified 328 of 377 test images — outperforming two larger pretrained models by learning what actually matters for static ASL recognition.*

---

## 🧩 Motivation

American Sign Language is the primary language for millions of Deaf and Hard-of-Hearing individuals in the United States. Accurate gesture classification from static images is a foundational step toward building tools that improve communication accessibility — from educational applications to assistive technology that bridges ASL and text in real time.

This project evaluates three pretrained CNN architectures on a 36-class ASL gesture classification task covering the full alphabet (A to Z) and digits 0 through 9.

---

## 📊 Dataset

- 2,515 labeled hand gesture images across 36 classes
- 26 alphabet signs (A to Z) and 10 digit signs (0 to 9)
- Train / Validation / Test split: 70% / 15% / 15%

**Data Augmentation (TensorFlow ImageDataGenerator):**
- Pixel rescaling (1/255)
- Rotation up to 40 degrees
- Horizontal and vertical shifts (20%)
- Shear and zoom transformations
- Horizontal flipping
- Nearest neighbor fill mode

---

## 🏗️ Architectures Evaluated

Three pretrained CNNs were fine-tuned with custom dense layers 
and dropout on the ASL dataset:

1. VGG16
2. InceptionV3
3. ResNet50

All models were trained for up to 50 epochs with early stopping 
patience of 10, Adam optimizer, categorical cross-entropy loss, 
learning rate of 0.01, batch size of 16, and dropout of 0.20.

---

## 📈 Results

| Model | Test Accuracy | Correct | Misclassified | Macro F1 |
|-------|--------------|---------|--------------|----------|
| **VGG16** | **87%** | **328** | **49** | **0.87** |
| InceptionV3 | 79% | 296 | 81 | 0.78 |
| ResNet50 | 34% | 130 | 247 | 0.34 |

VGG16 outperformed InceptionV3 by 8 percentage points and ResNet50 by 53 percentage points on the test set.

---

## ✅ Model Selection: VGG16

VGG16 was selected as the final model based on four criteria:

1. **Highest test accuracy** 

    — 87% on 377 unseen test images, correctly classifying 328 gestures across 36 classes.

2. **Strongest convergence** 

    — lowest training and validation loss across all 50 epochs with consistent improvement.

3. **Better generalization**

    — InceptionV3 initially outperformed VGG16 during early validation epochs, but VGG16 surpassed it after approximately 30 to 35 epochs and maintained that advantage through the end of training.

4. **ResNet50 failed to learn the task**

   — at 34% accuracy on a 36-class problem (random chance is approximately 2.8%), ResNet50 showed that deeper architecture does not guarantee better performance on specialized image domains with limited data.

---

## 🔍 Key Findings

**Simpler architecture outperformed deeper ones**

  - VGG16 is architecturally simpler than both InceptionV3 and ResNet50 yet produced the best results. This mirrors the finding from the Thyroid TI-RADS project: on specialized image domains with limited training data, a well-tuned simpler architecture often outperforms a more complex one. ImageNet pretrained features in deeper models do not always transfer cleanly to domain-specific classification tasks.

**InceptionV3 showed early promise but plateaued**

  - InceptionV3 leading early in validation then falling behind VGG16 after epoch 30 to 35 suggests its multi-scale feature extraction provides an early advantage but does not generalize as well to the fine-grained hand gesture distinctions required for 36-class ASL classification.

**ResNet50 underperformed significantly**

  - 34% accuracy on a task where random chance is 2.8% confirms ResNet50 learned something, but its residual connections and depth did not translate to useful feature extraction for this dataset size and domain. This is likely a combination of dataset size constraints and the mismatch between ImageNet features and hand gesture imagery.

---

## ⚠️ Limitations

**Static classification only**
 
  - this model classifies individual hand gesture images and does not support real-time or video-based ASL recognition. Deployment as an accessibility tool would require extension to sequential gesture recognition using RNNs or transformer-based architectures.

**Dataset size**
  - 2,515 images across 36 classes averages roughly 70 images per class for training, which is limited for deep learning. Larger labeled ASL datasets would likely improve performance meaningfully.

**No deployment or latency evaluation**

  - inference speed, model size optimization, and edge device compatibility were not assessed. Production accessibility applications would require these considerations before deployment.

---

## 🚀 Future Work

- Extend to real-time video-based gesture recognition using RNNs or transformer architectures on sequential frames
- Evaluate RadImageNet or domain-specific pretrained weights as alternatives to ImageNet initialization
- Expand dataset size through additional data collection or synthetic augmentation to improve per-class sample counts
- Assess model compression techniques (pruning, quantization) for mobile or edge deployment in accessibility applications

---

## 🔧 Tools
Python, TensorFlow, Keras, VGG16, InceptionV3, ResNet50, Transfer Learning, ImageDataGenerator, Adam Optimizer, Early Stopping, Pandas, NumPy, Matplotlib
