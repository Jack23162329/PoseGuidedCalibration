# PoseGuidedCalibration

Human Pose–Guided Joint Optimization for Camera Auto-Calibration with Unknown Intrinsics  
(ICCE 2025, Oral Presentation)

## Table of Contents
1. [Introduction](#introduction)  
2. [Directory Structure](#directory-structure)  
3. [Prerequisites](#prerequisites)  
4. [Installation](#installation)  
5. [Usage](#usage)  
6. [Data & Output](#data--output)  
7. [License](#license)  

---

## Introduction
This repository implements a novel camera self-calibration pipeline that leverages detected human joint keypoints as calibration targets. The core steps are:

- **DLT** + normalization → compute **intrinsics** & **extrinsics**  
- **PyTorch** implementation for joint optimization  
- Multi-camera fusion via **SuperPoint/SuperGlue** feature matching  

---

## Directory Structure
PoseGuidedCalibration/
├── asset/ # pretrained model weights or example images
├── data/ # calibration images & pose files
├── data_archive/ # archived datasets from older experiments
├── models/ # SuperPoint / SuperGlue weights
├── output/ # calibration results & visualizations
│ └── visualizations/ # generated plots and images
├── calibration_numpy.ipynb # numpy-based DLT demo
├── calibration_torch_Jack.ipynb # PyTorch optimization demo
├── multicamera.ipynb # multi-camera synchronization & calibration
├── superglue_multi.ipynb # SuperGlue-based feature matching demo
├── requirements.txt # Python dependencies
├── LICENSE
└── README.md
---

## Prerequisites

1. **Python**  
   - Version 3.8 or higher  

2. **Jupyter Notebook / JupyterLab**  
   - To run the `.ipynb` demos  

3. **System tools**  
   - `git`  
   - `pip` (or `conda`)  

4. **Python packages**  
   It’s recommended to use a virtual environment. Then install:
   ```bash
   pip install -r requirements.txt
If you don’t have a requirements.txt, install:
```bash
pip install numpy opencv-python torch torchvision vidgear matplotlib scipy
numpy

opencv-python

torch, torchvision

vidgear (for multi-stream capture)

matplotlib, scipy
```

# 1. Clone this repo
git clone https://github.com/Jack23162329/PoseGuidedCalibration.git
cd PoseGuidedCalibration

# 2. Create and activate a virtual environment
python3 -m venv venv
source venv/bin/activate

# 3. Install dependencies
```bash
pip install -r requirements.txt
```
Usage
Launch Jupyter

jupyter notebook
Then open one of the notebooks:

calibration_numpy.ipynb
Classic DLT + normalization calibration flow

1. multicamera.ipynb
Multi-camera capture & calibration

2. superglue_multi.ipynb
Feature matching with SuperPoint / SuperGlue

3. calibration_torch_Jack.ipynb
PyTorch-based joint optimization


Tip: At the top of each notebook you’ll find editable paths like DATA_DIR and MODEL_DIR. Adjust them to your local setup.

Data & Output
Input data

Place raw calibration images (checkerboards or pose images) under data/

Put pretrained model files into asset/ or models/

Output

Calibrated intrinsics & extrinsics saved to output/

Visualization figures saved to output/visualizations/

License
This project is released under the MIT License.

