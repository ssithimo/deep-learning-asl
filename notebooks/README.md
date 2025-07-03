# ASL Sign Language Classification using Transfer Learning

This folder contains a single Jupyter notebook that consolidates the entire workflow for the deep-learning-asl project.

This project applies transfer learning using InceptionV3, VGG16, and ResNet50 to classify American Sign Language (ASL) hand signs for both English alphabet (A–Z) and numeric digits (0–9). The model is trained on a custom dataset of 2,515 RGB images, with ~70 images per class.

## Contents

- `deep-learning-asl.ipynb`:  
  Contains all code for:
  - Data loading and cleaning  
  - Exploratory data analysis (EDA)  
  - Feature engineering
  - Model training and testing
  - Model evaluation and selection
    
## How to run

### Clone the repository:

```bash
git clone https://github.com/ssithimo/deep-learning-asl.git
cd deep-learning-asl
```

### Install dependencies:

```bash
pip install -r requirements.txt
```

### Run the notebook:
```bash
jupyter notebook notebooks/deep-learning-asl.ipynb
```
