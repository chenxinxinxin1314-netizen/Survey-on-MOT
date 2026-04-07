# Survey-on-MOT
# 🎯 Awesome Multi-Object Tracking (MOT) Survey

> A comprehensive survey of Multi-Object Tracking (MOT) methods, datasets, and benchmarks.  
> 持续更新中 | Continuously updated.


[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
![Last Updated](https://img.shields.io/github/last-commit/你的用户名/仓库名)

---

## 📖 Contents

- [Datasets](#datasets)
- [Metrics](#metrics)
- [Methods](#methods)
  - [Traditional Object Tracking Methods](#traditional-object-tracking-methods)
    - [Generative Methods](#generative-methods)
    - [Discriminative Methods](#discriminative-methods)
    - [Correlation Filter Tracking](#correlation-filter-tracking)
    - [Handcrafted Features](#handcrafted-features)
    - [Limitations of Traditional Methods](#limitations-of-traditional-methods)
  - [Deep Learning-based MOT](#deep-learning-based-mot)
    - [Tracking-by-Detection Pipeline](#tracking-by-detection-pipeline)
    - [Joint Detection and Embedding](#joint-detection-and-embedding)
    - [Graph-based Association](#graph-based-association)
    - [End-to-End Transformer-based Tracking](#end-to-end-transformer-based-tracking)
- [Citation](#citation)

---
## Datasets
| Dataset | Year | Domain | Target Type | Key Challenges | Link |
|---------|------|--------|-------------|----------------|------|
| MOT15 | 2015 | Pedestrian | Indoor / Outdoor | Varying camera motion, low resolution | [Official](https://motchallenge.net/data/MOT15/) |
| MOT16 | 2016 | Pedestrian | Street scenes | Occlusion, detection noise | [Official](https://motchallenge.net/data/MOT16/) |
| MOT17 | 2017 | Pedestrian | Multi-view street | Multiple detectors (DPM, FRCNN, SDP) | [Official](https://motchallenge.net/data/MOT17/) |
| MOT20 | 2020 | Pedestrian | Crowded scenes | Extreme density, heavy occlusion | [Official](https://motchallenge.net/data/MOT20/) |
| DanceTrack | 2022 | Dance / Performance | Similar-looking persons | Uniform appearance, non-linear motion | [Official](https://github.com/DanceTrack/DanceTrack) |
| SportsMOT  | 2023 | Sports | Athletes (Basketball / Football / Volleyball) | Fast motion, frequent interaction | [Official](https://deeperaction.github.io/datasets/sportsmot.html) |
| BDD100K    | 2020 | Autonomous Driving | Multi-class (car, pedestrian, truck, etc.) | Large scale, diverse weather & lighting | [Official](https://www.bdd100k.com/) |

---

## Metrics

| Metric | Full Name | Formula | Description |
|--------|-----------|---------|-------------|
| MOTA | Multiple Object Tracking Accuracy  | $1 - \frac{\vert\text{FP}\vert + \vert\text{FN}\vert + \vert\text{IDSW}\vert}{\vert\text{gtDet}\vert}$ | Jointly penalizes FP, FN, and identity switches; can be negative when errors exceed ground truth count |
| MOTP | Multiple Object Tracking Precision | $\frac{1}{\vert\text{TP}\vert} \sum\_{m \in \text{TP}} \text{IoU}\_m$ | Mean IoU over all true positive matches; measures localization quality independently of MOTA |
| IDF1 | Identity F1 Score                  | $\frac{\vert\text{IDTP}\vert}{\vert\text{IDTP}\vert + 0.5\vert\text{IDFN}\vert + 0.5\vert\text{IDFP}\vert}$ | Trajectory-level matching metric; more sensitive to prolonged identity switches than MOTA |
| HOTA | Higher Order Tracking Accuracy     | $\sqrt{\text{DetA}\_{\alpha} \times \text{AssA}\_{\alpha}}$ | Geometric mean of detection and association accuracy; averaged over IoU thresholds for threshold-agnostic evaluation |
| MT   | Mostly Tracked                     | — | Percentage of ground truth trajectories covered for more than 80% of their lifespan |
| ML   | Mostly Lost                        | — | Percentage of ground truth trajectories covered for less than 20% of their lifespan |
| IDs  | Identity Switches                  | — | Total number of times a tracked identity incorrectly changes during tracking |
| FPS  | Frames Per Second                  | — | Inference speed; reflects the real-time applicability of the tracker |

---

## Methods
### Traditional Object Tracking Methods
#### Generative Methods
 
> Model target appearance to locate objects (e.g., Mean Shift, Particle Filter).

| Year | Method | Venue | Highlights | Link |
|------|--------|-------|------------|------|
| 1960 | <nobr> Kalman Filter </nobr>  | Journal of Basic Engineering  | Recursive Bayesian estimation under Gaussian noise and linear dynamics; foundational motion prediction component in modern trackers | [Paper](https://asmedigitalcollection.asme.org/fluidsengineering/article/82/1/35/397706) |
| 2002 | <nobr> Particle Filter </nobr> | IEEE Trans. Signal Processing | Sequential Monte Carlo sampling; handles nonlinear motion and non-Gaussian noise via weighted particle representation | [Paper](https://ieeexplore.ieee.org/document/978374) |
| 2003 | <nobr> Mean Shift  </nobr>     | IEEE TPAMI                    | Iterative mode-seeking in color histogram feature space; efficient gradient-free optimization for appearance-based localization | [Paper](https://ieeexplore.ieee.org/document/1197078) |

---

#### Discriminative Methods
  
> Treat tracking as foreground/background classification with online classifier updates.

| Year | Method | Venue | Highlights | Link |
|------|--------|-------|------------|------|
| 2004 | SVM Tracker | IEEE TPAMI | Margin-maximizing SVM decision boundary; strong theoretical generalization but quadratic support vector growth limits real-time use | [Paper](https://ieeexplore.ieee.org/document/1315094) |
| 2009 | MILTrack    | CVPR       | Multiple Instance Learning replaces hard binary labels with bag-level supervision, substantially reducing model drift | [Paper](https://ieeexplore.ieee.org/document/5206737) |
| 2015 | Struck      | IEEE TPAMI | Structured output prediction over kernelized SVM; directly optimizes bounding-box loss, eliminating error-prone intermediate binary labeling | [Paper](https://ieeexplore.ieee.org/document/7360205) |

---

#### Correlation Filter Tracking
  
> Efficient target response map computation via circulant matrices and Fourier transform.

| Year | Method | Venue | Highlights | Link |
|------|--------|-------|------------|------|
| 2010 | MOSSE | CVPR | First correlation filter tracker; learns filters in Fourier domain via FFT for real-time performance | [Paper](https://ieeexplore.ieee.org/document/5539960) |
| 2014 | KCF   | IEEE TPAMI | Kernel trick + multi-channel HOG features; circulant matrix formulation reduces ridge regression complexity from cubic to log-linear | [Paper](https://ieeexplore.ieee.org/document/6870486) \| [Code](https://github.com/joaofaro/KCFcpp) |
| 2017 | ECO   | CVPR | Factorized convolution operators + compact sample representation; significantly reduces model complexity and computational overhead | [Paper](https://openaccess.thecvf.com/content_cvpr_2017/papers/Danelljan_ECO_Efficient_Convolution_CVPR_2017_paper.pdf) \| [Code](https://github.com/martin-danelljan/ECO) |
| 2017 | CSR-DCF | CVPR | Spatial reliability weights to suppress boundary effects from circular convolution; channel-wise feature selection for robustness | [Paper](https://openaccess.thecvf.com/content_cvpr_2017/papers/Lukezic_Discriminative_Correlation_Filter_CVPR_2017_paper.pdf) \| [Code](https://github.com/alanlukezic/csr-dcf) |

---

#### Handcrafted Features
  
> Rely on manually engineered features such as HOG, LBP, and color histograms.

| Year | Feature | Venue | Type | Highlights | Link |
|------|---------|-------|------|------------|------|
| 2002 | LBP         | IEEE TPAMI | Texture            | Binary pixel comparison encoding; invariant to monotonic illumination changes with low computational cost | [Paper](https://ieeexplore.ieee.org/document/1017623) |
| 2005 | HOG         | CVPR       | Shape / Gradient   | Local edge and gradient orientation histograms; highly discriminative for pedestrian silhouette boundaries | [Paper](https://ieeexplore.ieee.org/document/1467360) |
| 2009 | Color Names | IEEE TIP   | Color / Appearance | Probabilistic mapping from RGB to linguistic color terms; robust to illumination variation | [Paper](https://ieeexplore.ieee.org/document/4774359) |

---

#### Limitations of Traditional Methods

| Limitation | Description |
|------------|-------------|
| **Weak Representation**       | Handcrafted features (HOG, LBP, Color Names) require extensive domain expertise and generalize poorly across diverse object categories and conditions |
| **Model Drift**               | Online classifiers with fixed learning rates and limited temporal memory accumulate errors during prolonged occlusions or rapid appearance changes |
| **Boundary Effects**          | Circular convolution assumptions in correlation filters introduce artificial boundary artifacts, requiring separate scale pyramids that increase computational cost |
| **Occlusion Sensitivity**     | Shallow representations fail to capture semantic information needed to distinguish targets from background clutter under heavy occlusion or severe deformation |
| **Limited Detection Quality** | Sliding window detection approaches provide significantly lower accuracy than modern deep detectors, creating a performance ceiling for the full tracking pipeline |

---

### Deep Learning-based MOT

---

#### Tracking-by-Detection Pipeline

> Classic two-stage framework: detect first, then associate.

##### Detection and Feature Extraction

| 年份 | 方法 | 会议/期刊 | 亮点 | 链接 |
|------|------|-----------|------|------|
| 2023 | YOLOv8 | — | 实时检测骨干 | [Code](链接) |
| ... | ... | ... | ... | ... |

##### Appearance Modeling and Re-identification

| 年份 | 方法 | 会议/期刊 | 亮点 | 链接 |
|------|------|-----------|------|------|
| 2017 | Deep SORT | ICIP | 深度外观描述子 | [Paper](链接) \| [Code](链接) |
| ... | ... | ... | ... | ... |

##### Motion Modeling and Data Association

| 年份 | 方法 | 会议/期刊 | 亮点 | 链接 |
|------|------|-----------|------|------|
| 2016 | SORT | ICIP | 卡尔曼滤波 + 匈牙利算法 | [Paper](链接) \| [Code](链接) |
| 2022 | ByteTrack | ECCV | 利用低置信度检测框 | [Paper](链接) \| [Code](链接) |
| ... | ... | ... | ... | ... |

---

#### Joint Detection and Embedding

> Shared backbone for simultaneous detection and Re-ID in a single network.

##### Shared Backbone Architectures

| 年份 | 方法 | 会议/期刊 | 亮点 | 链接 |
|------|------|-----------|------|------|
| 2020 | FairMOT | IJCV | 平衡检测与 ReID 分支 | [Paper](链接) \| [Code](链接) |
| ... | ... | ... | ... | ... |

##### Multi-task Learning and Optimization

| 年份 | 方法 | 会议/期刊 | 亮点 | 链接 |
|------|------|-----------|------|------|
| ... | ... | ... | ... | ... |

---

#### Graph-based Association
 
> Model detections and trajectories as graph nodes; learn association weights via GNN.

##### Graph Neural Networks for Data Association

| 年份 | 方法 | 会议/期刊 | 亮点 | 链接 |
|------|------|-----------|------|------|
| 2020 | MPNTrack | CVPR | 消息传递网络 | [Paper](链接) \| [Code](链接) |
| ... | ... | ... | ... | ... |

##### Spatial-Temporal Graph Modeling

| 年份 | 方法 | 会议/期刊 | 亮点 | 链接 |
|------|------|-----------|------|------|
| ... | ... | ... | ... | ... |

---

#### End-to-End Transformer-based Tracking

> Attention-based end-to-end tracking without hand-crafted post-processing.

##### Self-Attention for Global Context

| 年份 | 方法 | 会议/期刊 | 亮点 | 链接 |
|------|------|-----------|------|------|
| ... | ... | ... | ... | ... |

##### Query-based Tracking Paradigm

| 年份 | 方法 | 会议/期刊 | 亮点 | 链接 |
|------|------|-----------|------|------|
| 2021 | TrackFormer | CVPR | Track Query 持续追踪 | [Paper](链接) \| [Code](链接) |
| 2022 | MOTR | ECCV | 端到端 Transformer MOT | [Paper](链接) \| [Code](链接) |
| ... | ... | ... | ... | ... |

##### Unified Detection and Association

| 年份 | 方法 | 会议/期刊 | 亮点 | 链接 |
|------|------|-----------|------|------|
| ... | ... | ... | ... | ... |

---


## Citation






## Contributing

Feel free to open a PR or Issue to add papers or fix errors!

---

