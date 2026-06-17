# AquaDetect: Aquarium Object Detection using Faster R-CNN

## Project Overview
This project focuses on implementing an object detection model for underwater images using the Faster R-CNN architecture. The primary goal is to detect and classify marine animals from images in the *Aquarium Dataset* sourced from Roboflow. The dataset contains images of fish, jellyfish, penguins, puffins, sharks, starfish, and stingrays, with labeled bounding boxes for each object.

---

## Table of Contents
- [Project Overview](#project-overview)
- [Directory Structure](#directory-structure)
- [Dataset](#dataset)
- [Environment Setup](#environment-setup)
- [Model Architecture](#model-architecture)
- [Training](#training)
- [Evaluation](#evaluation)
- [Usage](#usage)
- [Results](#results)
- [References](#references)
- [Acknowledgments](#acknowledgments)

---

## Directory Structure
```
aquarium_pretrain
├── train
│   ├── images  # Training images
│   └── labels  # Corresponding YOLO-style labels for images
├── valid
│   ├── images  # Validation images
│   └── labels  # Corresponding YOLO-style labels for images
├── test
│   ├── images  # Test images
│   └── labels  # Corresponding YOLO-style labels for images
└── data.yaml    # Configuration file specifying paths, class names, and number of classes
```

---

## Dataset
**Source:** Roboflow — *Aquarium Dataset (raw-1024)*

The dataset contains labeled images of underwater marine animals. The dataset is organized into `train`, `valid`, and `test` folders, each containing images and their corresponding YOLO-style label files.

**Classes:**
1. Fish  
2. Jellyfish  
3. Penguin  
4. Puffin  
5. Shark  
6. Starfish  
7. Stingray  

**data.yaml**
```yaml
train: ../train/images
val: ../valid/images
nc: 7
names: ['fish', 'jellyfish', 'penguin', 'puffin', 'shark', 'starfish', 'stingray']
```

---

## Environment Setup
To set up the environment, follow these steps:

1. **Create a virtual environment:**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows use `venv\Scripts\activate`
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```
   > **Note:** The `requirements.txt` file should list all necessary libraries such as `tensorflow`, `keras`, `numpy`, `opencv-python`, and `seaborn`.

3. **Clone the dataset:**
   - Download the *Aquarium Dataset* from Roboflow.
   - Place it in the `aquarium_pretrain` directory with the structure outlined above.

---

## Model Architecture
This project implements the **Faster R-CNN** architecture, a widely used object detection model. The key components of the architecture are:

1. **Feature Extractor:** A CNN backbone (like ResNet) extracts feature maps from images.
2. **Region Proposal Network (RPN):** Proposes candidate object regions.
3. **ROI Pooling:** Pools features from candidate regions into a fixed size.
4. **Fully Connected Layers:** Classifies and refines the bounding box coordinates for each detected object.

---

## Training
To train the model, follow these steps:

1. **Activate the virtual environment:**
   ```bash
   source venv/bin/activate  # On Windows use `venv\Scripts\activate`
   ```

2. **Run the training script:**
   ```bash
   python train.py --data data.yaml --weights weights/faster_rcnn.pth --epochs 50
   ```
   > **Arguments:**
   - `--data`: Path to the `data.yaml` file.
   - `--weights`: Pretrained weights for Faster R-CNN (optional).
   - `--epochs`: Number of training epochs.

3. **Monitor training:**
   - Loss and accuracy are logged for each epoch.
   - Early stopping is used to prevent overfitting.

---

## Evaluation
To evaluate the trained model on the test set, run the following command:

```bash
python evaluate.py --data data.yaml --weights weights/faster_rcnn.pth
```

The evaluation script calculates metrics like **mAP (mean Average Precision)** and **F1-score** to assess model performance.

---

## Usage
To use the model to detect objects in new underwater images, follow these steps:

1. **Place your images** in the `test/images/` directory.
2. **Run the inference script:**
   ```bash
   python detect.py --weights weights/faster_rcnn.pth --source test/images/
   ```
3. **Output:**
   - The detected objects will be saved as images with bounding boxes and class labels.

---

## Results
- **Precision, Recall, and mAP** are reported for each class (e.g., fish, jellyfish, penguin, etc.).
- **Loss curve** is plotted to visualize model convergence.
- **Sample predictions** from the test set are visualized to showcase the model's accuracy.

---

## References
- [Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks](https://arxiv.org/abs/1506.01497)
- [Roboflow: Aquarium Dataset](https://roboflow.com/)
- [TensorFlow Object Detection API](https://github.com/tensorflow/models/tree/master/research/object_detection)

---

## Acknowledgments
This project is powered by:
- **Roboflow** for providing the Aquarium Dataset.
- **TensorFlow** and **Keras** for model training and evaluation.
- **OpenCV** for image processing and augmentation.

---

For questions or support, feel free to open an issue or reach out to the maintainers.

