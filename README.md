# Uncertainty-Aware Monocular Visual Odometry Inspired by D3VO

## Project Overview

This project presents an uncertainty-aware monocular visual odometry framework inspired by the concepts introduced in D3VO (Deep Direct Visual Odometry). The system estimates camera motion from monocular image sequences while integrating depth prediction and uncertainty-based filtering to improve robustness under challenging driving scenarios.

The framework combines classical visual odometry techniques with deep-learning-based scene understanding to reduce the influence of unreliable image regions such as:

- Dynamic objects
- Motion blur
- Shadows
- Reflections
- Texture-less regions
- Low-light conditions

The primary goal is to improve trajectory estimation stability and localization performance in autonomous driving environments.

---

## Motivation

Traditional monocular visual odometry systems often assume all image regions contribute equally during camera motion estimation.

In real-world driving scenes:

- Moving vehicles introduce incorrect correspondences
- Shadows create unstable features
- Reflective surfaces produce noisy measurements
- Motion blur affects feature extraction

D3VO introduced uncertainty modeling within visual odometry to address this problem.

Inspired by that idea, this project attempts to:

1. Estimate scene depth
2. Generate uncertainty maps
3. Identify reliable image regions
4. Filter unreliable features
5. Improve camera trajectory estimation

---

## Paper Inspiration

This project is inspired by:

📄 D3VO: Deep Depth, Deep Pose and Deep Uncertainty for Monocular Visual Odometry

Authors:

- Nan Yang
- Lukas von Stumberg
- Daniel Cremers
- Rui Wang

Conference:

IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR), 2020

Paper Link:

https://arxiv.org/abs/2003.01060

---

## Objectives

The main objectives of this project are:

- Build a monocular visual odometry system
- Integrate deep-learning-based depth prediction
- Generate uncertainty heatmaps
- Filter unreliable image regions
- Estimate camera trajectories
- Evaluate trajectory quality
- Analyze failure cases

---

## System Architecture

Pipeline:

```text
Driving Image Sequence
            ↓
Preprocessing
            ↓
Depth Estimation
            ↓
Uncertainty Estimation
            ↓
Reliable Region Selection
            ↓
ORB Feature Extraction
            ↓
Feature Matching
            ↓
Pose Recovery
            ↓
Trajectory Estimation
            ↓
ATE/RPE Evaluation
```

---

## Dataset

Dataset Used:

KITTI Vision Benchmark Suite

Dataset Link:

http://www.cvlibs.net/datasets/kitti/

Dataset contains:

- Stereo driving images
- Camera calibration data
- Ground truth trajectories
- Urban road environments

Example sequence:

```text
sequence_00/
    image_0/
        000000.png
        000001.png
        ...
    poses.txt
```

---

## Technologies Used

Programming Language:

- Python

Libraries:

- OpenCV
- PyTorch
- Transformers
- NumPy
- Matplotlib
- Scikit-learn
- PIL

Models:

- Intel DPT Hybrid MiDaS

---

## Folder Structure

```text
D3VO_Project/

├── data/
│   └── sequence_00/
│       ├── image_0/
│       └── poses.txt
│
├── outputs/
│   ├── depth/
│   ├── uncertainty/
│   ├── masks/
│   ├── matches/
│   ├── trajectories/
│   ├── trajectory_comparison.png
│   ├── project_dashboard.png
│   └── results.txt
│
├── main.py
├── requirements.txt
└── README.md
```

---

## Methodology

### Step 1: Feature Extraction

ORB features are extracted from consecutive image frames.

Purpose:

- Detect keypoints
- Generate descriptors
- Establish correspondences

Methods used:

- ORB detector
- Brute-force matching

---

### Step 2: Camera Motion Estimation

Feature correspondences are used to estimate camera movement.

Methods:

- Essential Matrix computation
- RANSAC
- Pose Recovery

Mathematical representation:

Essential matrix:

E = [t]×R

Where:

- R = rotation matrix
- t = translation vector

---

### Step 3: Monocular Depth Prediction

Depth maps are generated using pretrained DPT/MiDaS.

Input:

```text
RGB image
```

Output:

```text
Depth map
```

Purpose:

- Capture scene geometry
- Understand object distances

---

### Step 4: Uncertainty Estimation

Uncertainty is approximated from depth gradients.

High uncertainty regions:

- Moving cars
- Shadows
- Motion blur
- Reflective objects

Low uncertainty regions:

- Stable road surfaces
- Static structures

Formula:

```text
Uncertainty = |dx| + |dy|
```

where:

dx:

```text
Depth(x+1)-Depth(x)
```

dy:

```text
Depth(y+1)-Depth(y)
```

---

### Step 5: Reliable Region Filtering

Reliable regions are selected using thresholding.

Condition:

```text
uncertainty < threshold
```

Purpose:

Remove noisy image regions before feature extraction.

---

### Step 6: Trajectory Estimation

Estimated poses are accumulated over time:

```text
Tt = Tt−1 × ΔT
```

Output:

```text
Predicted camera trajectory
```

---

## Evaluation Metrics

### 1. Absolute Trajectory Error (ATE)

Measures overall trajectory deviation.

Formula:

```text
ATE = √(1/N Σ ||Pi−Qi||²)
```

where:

- Pi = predicted trajectory
- Qi = ground truth trajectory

---

### 2. Relative Pose Error (RPE)

Measures local motion estimation error.

Formula:

```text
RPE = mean(||ΔP−ΔQ||)
```

---

## Outputs Generated

### Depth Maps

```text
outputs/depth/
```

### Uncertainty Heatmaps

```text
outputs/uncertainty/
```

### Reliable Region Masks

```text
outputs/masks/
```

### Feature Matching Images

```text
outputs/matches/
```

### Camera Trajectories

```text
outputs/trajectories/
```

### Dashboard

```text
outputs/project_dashboard.png
```

---

## Challenges Faced

- Monocular scale ambiguity
- Dynamic object interference
- Feature instability
- Low-light scenes
- Motion blur
- Computational cost

---

## Future Improvements

Possible extensions:

### Deep uncertainty prediction

Replace gradient-based uncertainty with learned uncertainty estimation.

### Dynamic object segmentation

Integrate:

- Mask R-CNN
- YOLO

### Real-time optimization

- TensorRT
- Quantization
- GPU acceleration

### SLAM integration

Integrate with:

- ORB-SLAM
- Visual-Inertial SLAM

---

## Conclusion

This project demonstrates how uncertainty modeling can improve monocular visual odometry systems by reducing the influence of unreliable scene regions.

The proposed framework combines:

- Classical computer vision
- Deep learning
- Geometric reasoning
- Autonomous driving concepts

to improve trajectory robustness.

---

## References

[1] Wang Y, Yuan W, Pan X, Lu C.

D3VO: Deep Depth, Deep Pose and Deep Uncertainty for Monocular Visual Odometry

CVPR 2020

https://arxiv.org/abs/2003.01060

---

[2] Geiger A, Lenz P, Urtasun R.

Are We Ready for Autonomous Driving?

KITTI Vision Benchmark Suite

CVPR 2012

http://www.cvlibs.net/datasets/kitti/

---

[3] Ranftl R et al.

Vision Transformers for Dense Prediction

ICCV 2021

---

[4] Rublee E et al.

ORB: An Efficient Alternative to SIFT or SURF

ICCV 2011

---

## Author

Bhavika Pandya

B.Tech Data Science and Artificial Intelligence  
Indian Institute of Technology Guwahati


