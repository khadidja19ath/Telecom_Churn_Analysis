# ML-Lab-OCT-Classifier
This repository contains a beginner-friendly deep learning project for classifying retinal diseases from OCT images, implemented in Google Colab using transfer learning with DenseNet.
# Deep Learning for Retinal Disease Classification from OCT Images

## Project Overview

This project implements a simplified deep learning model for classifying retinal diseases (Choroidal Neovascularization (CNV), Diabetic Macular Edema (DME), Drusen, and Normal) from Optical Coherence Tomography (OCT) images. It's designed as a hands-on introduction to concepts from recent machine learning research papers in medical imaging, using Google Colab.

The project emphasizes **Transfer Learning** with a pre-trained **DenseNet201** architecture, showcasing how powerful models can be adapted for specific tasks even with limited data.

---

## Background: Key ML Concepts

### Image Classification

**Image Classification** is the primary task here: assigning a single category (e.g., 'CNV' or 'NORMAL') to an entire input image. Our model learns to distinguish between different retinal conditions.

### Convolutional Neural Networks (CNNs)

**CNNs** are a specialized type of neural network extremely effective for image analysis. They automatically learn to detect patterns (like edges or textures) and complex features directly from pixel data.

* **TensorFlow:** An open-source machine learning framework by Google.
* **Keras:** A user-friendly API running on TensorFlow, simplifying neural network creation.

### Transfer Learning

<img width="643" height="220" alt="image" src="https://github.com/user-attachments/assets/d03ef4b4-cfda-4a17-bb9b-55ef2f77f01f" />

**Transfer Learning** is a powerful technique where we take a deep learning model pre-trained on a vast, general dataset (like ImageNet) and adapt it for our specific, often smaller, task. This saves significant training time and resources, and helps achieve high accuracy even with limited domain-specific data.

### Detection and Selection (Implicit)

While our project focuses on **classification**, concepts of **detection** (identifying features) and **selection** (prioritizing important features) are implicitly handled:

<img width="709" height="423" alt="image" src="https://github.com/user-attachments/assets/293c9634-a66b-48a6-9540-56a2974ad7ce" />

* **Detection:** The pre-trained DenseNet201 acts as a feature extractor, detecting various patterns and structures within the OCT images.
* **Selection:** Layers like `GlobalAveragePooling2D` and the initial `Dense` layer in our custom head condense and emphasize the most relevant features for classification. This is conceptually linked to the "attention mechanisms" discussed in research, allowing the model to focus on important information.

### Activation Functions: ReLU and Softmax

* **ReLU (Rectified Linear Unit):** Defined as $f(x) = \max(0, x)$. It introduces non-linearity, allowing the model to learn complex relationships, and is computationally efficient. In our model, it's used in the hidden `Dense` layer of the classification head.
* **Softmax:** Used in the output layer for multi-class classification. It converts raw scores into a probability distribution where all probabilities sum to 1, indicating the likelihood of an image belonging to each class. The class with the highest probability is the model's prediction.

---

## Research Paper Insights

This project draws inspiration from three papers on deep learning for retinal disease classification using OCT images:

1.  **"A Multi-branch and Attention Based CNN Architecture for the Classification of Retinal Diseases from OCT Images"** by S.F. Rabbi et al., 2023
    * **Core Concepts:** Multi-branch CNN architecture, Convolutional Block Attention Module (CBAM).
    * **Relevance:** Our DenseNet201 serves as a multi-branch architecture. While we don't implement explicit CBAM, the concept of attention is implicitly achieved through pre-trained features.
    [![Conceptual architecture of a multi-branch CNN with attention mechanism.]](https://ieeexplore.ieee.org/document/10303384)

         <img width="600" height="350" alt="image" src="https://github.com/user-attachments/assets/1743d0c8-125b-4ebe-8945-b340d81d1388" />
   
   *Figure: Conceptual architecture of a multi-branch CNN with attention mechanism. (Ref. Rabbi et al., 2023)*

2.  **"Multi-Stage Classification of Retinal OCT Using Multi-Scale Ensemble Deep Architecture"** by O. Akinniyi et al., 2023
    * **Core Concepts:** Multi-stage classification, multi-scale (pyramidal) feature ensemble architecture, DenseNet backbone.
    * **Relevance:** We use DenseNet201 as our backbone, aligning with the architectural choices for robust feature extraction.
    [![Schematic of the proposed multi-stage and multi-resolution deep architecture.]](https://www.mdpi.com/2073-8994/10/7/823)

         <img width="600" height="350" alt="image" src="https://github.com/user-attachments/assets/77e2b514-acad-4756-a8a8-cabe199922be" />
   
   *Figure: Schematic of the proposed multi-stage and multi-resolution deep architecture. (Ref. Akinniyi et al., 2023)*

3.  **"Classification of Retinal Disorders from OCT Images using Attention based CNN"** by G. Gupta, 2024
    * **Core Concepts:** Attention mechanisms, CNN, autoencoder for feature encoding and anomaly detection.
    * **Relevance:** The project demonstrates the foundational CNN and transfer learning for classification, which can be extended with explicit attention layers as a future step.
    [![Model architecture integrating auto-encoder, attention mechanism, and CNN.]](https://www.nepjol.info/index.php/jbss/article/download/78753/60327/226422)

         <img width="600" height="350" alt="image" src="https://github.com/user-attachments/assets/816c53da-0f12-41e9-835c-a869b40ce228" />

   *Figure: Model architecture integrating auto-encoder, attention mechanism, and CNN. (Ref. Gupta, 2024)*

---

## Google Colab Implementation

The project is implemented in a Google Colab notebook, making it easy to run without local setup.

### Dataset

A **small, synthetic dataset** is generated dynamically within the Colab notebook. This dataset contains OCT-like grayscale images for four classes: 'CNV', 'DME', 'DRUSEN', and 'NORMAL'. Each class has subtle, artificially embedded patterns to mimic disease characteristics, allowing for visual distinction and demonstration of the model's learning capabilities.

**Dataset Split:** The dataset is split into `train` and `val` (validation) directories. The `ImageDataGenerator.flow_from_directory()` method is used to load images specifically from these pre-arranged folders, effectively creating separate training and validation sets at the filesystem level.

#### Sample Synthetic OCT Images

Here are examples of the synthetic images generated, illustrating the basic visual patterns for each class.
<img width="738" height="308" alt="image" src="https://github.com/user-attachments/assets/49999d2f-2013-4a85-a553-52ec071b6630" />

---

## Model Architecture
<img width="213" height="443" alt="image" src="https://github.com/user-attachments/assets/2f9d4127-dafd-41ff-bf78-6dcc00b37873" />




