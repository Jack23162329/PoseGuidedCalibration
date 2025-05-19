# PoseGuidedCalibration

**Human Pose–Guided Joint Optimization for Camera Auto‑Calibration with Unknown Intrinsics**

Authors: Nathaniel Rensly, Zheng‑Kai Chen, Hsuan‑Cheng Chu, and Huang‑Chia Shih (Yuan Ze University, Taiwan)

[Download the full paper (PDF)](stamped.pdf)

---

## Table of Contents

1. [Abstract](#abstract)
2. [Key Contributions](#key-contributions)
3. [Features](#features)
4. [Method Overview](#method-overview)
5. [Prerequisites](#prerequisites)
6. [Installation](#installation)
7. [Usage](#usage)
8. [Results & Evaluation](#results--evaluation)
9. [Citation](#citation)

---

## Abstract

Traditional camera calibration relies on specialized patterns (checkerboards, spheres) and can be cumbersome or infeasible in dynamic scenes. Our repository implements the method described in Rensly *et al.* (ICCE 2025), which uses detected human joint keypoints as reference points for multi‑camera self‑calibration. By combining state‑of‑the‑art 2D pose estimation (HigherHRNet) with deep feature matching (SuperGlue) and an iterative joint optimization scheme in PyTorch, we achieve accurate intrinsics/extrinsics without physical calibration targets.

## Key Contributions

* **Pattern‑free Calibration**: Eliminates the need for checkerboards or printed patterns—just a person performing a slow, controlled spin.
* **Pose‑Based Correspondences**: Uses high‑confidence human joint detections (HigherHRNet) as calibration anchors.
* **Deep Feature Matching**: Adapts SuperGlue’s 256‑D descriptors to refine joint correspondences across views.
* **Joint Optimization**: Alternating Adam‑based optimization of intrinsics and extrinsics, with one camera anchored (identity pose) for stability.
* **PyTorch & CUDA**: End‑to‑end GPU acceleration enables iterative refinement and near‑real‑time performance.

## Features

* 📷 **Multi‑camera Support**: Calibrate any synchronized pair (or network) of cameras.
* 🤖 **Pose‑Estimation**: Integration with HigherHRNet for robust 2D joint detection.
* 🔗 **Feature Matching**: SuperGlue adaptation for precise keypoint matching.
* ⚙️ **Optimization Pipeline**: Scripts and notebooks for DLT baseline and PyTorch joint optimization.
* 📊 **Visualization**: Auto‑generated reprojection error plots and 3D reconstruction previews.

## Method Overview

1. **Capture**: Two cameras record a subject slowly rotating with arms extended.
2. **2D Joint Detection**: Detect 17 COCO‑standard keypoints with HigherHRNet; filter by confidence thresholds.
3. **Feature Matching**: Use SuperGlue to extract 256‑D descriptors near each joint; match across views.
4. **Initial Calibration**: Compute fundamental matrix (8‑point + SVD rank‑2 enforcement) → essential matrix → four candidate extrinsics.
5. **Triangulation & Selection**: Triangulate points, choose R, t combination with positive depths and minimal error.
6. **Joint Optimization**: Alternate between fixing intrinsics/extrinsics and optimize the other via Adam to minimize reprojection loss.
7. **Evaluation**: Compute Average Reprojection Error (ARE) and compare against Zhang’s method.

## Prerequisites

* **Python** ≥ 3.8
* **Jupyter Notebook** / **JupyterLab**
* **Git** and **pip** (or **conda**)

### Python Packages

Install via `requirements.txt` or manually:

```bash
pip install numpy opencv-python torch torchvision vidgear matplotlib scipy
```

* `higherhrnet` & `mediapipe` (optional alternatives)
* `superglue` weights in `models/`
* `torch.cuda` enabled for performance

## Installation

```bash
# Clone repository
git clone https://github.com/Jack23162329/PoseGuidedCalibration.git
cd PoseGuidedCalibration

# Create & activate virtual environment
python3 -m venv venv
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

## Usage

1. **Launch Jupyter**:

   ```bash
   jupyter notebook
   ```
2. **Open a demo notebook**:

   * `calibration_numpy.ipynb`: DLT + normalization baseline.
   * `calibration_torch_Jack.ipynb`: End‑to‑end PyTorch joint optimization.
   * `multicamera.ipynb`: Multi‑camera synchronization & keypoint aggregation.
   * `superglue_multi.ipynb`: SuperGlue feature matching pipeline.

> **Tip**: Edit path variables (`DATA_DIR`, `MODEL_DIR`) at the top of each notebook to point at your local data and model files.

## Results & Evaluation

* **Average Reprojection Error**: Typically < 0.5 px across test rotations, matching or exceeding Zhang’s checkerboard method.
* **3D Reconstruction**: Visualization of triangulated human skeleton (please see `output/visualizations/` for examples).

Charts and comparisons are auto‑generated in the notebooks (see Fig. 2–6 in the original paper).

## Citation

If you use this code for your research, please cite:

> Rensly, N., Chen, Z.‑K., Chu, H.‑C., & Shih, H.‑C. (2025). *Human Pose–Guided Joint Optimization for Camera Auto‑Calibration System with Unknown Intrinsics*. ICCE 2025.

```bibtex
@inproceedings{rensly2025pose,
  title={Human Pose–Guided Joint Optimization for Camera Auto‑Calibration System with Unknown Intrinsics},
  author={Rensly, Nathaniel and Chen, Zheng‑Kai and Chu, Hsuan‑Cheng and Shih, Huang‑Chia},
  booktitle={ICCE 2025},
  year={2025}
}
```

---

*For detailed algorithmic derivations, refer to the PDF linked above.*
