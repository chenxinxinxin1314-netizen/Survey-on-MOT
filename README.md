# 🎯 Awesome Multi-Object Tracking (MOT) Survey

> A comprehensive survey of Multi-Object Tracking (MOT) methods, datasets, and benchmarks.

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
![Last Updated](https://img.shields.io/github/last-commit/你的用户名/仓库名)

---

## 📖 Contents

- [📦 Datasets](#-datasets)
- [📏 Metrics](#-metrics)
- [🔬 Methods](#-methods)
  - [Traditional Object Tracking Methods](#traditional-object-tracking-methods)
    - [Generative Methods](#generative-methods)
    - [Discriminative Methods](#discriminative-methods)
    - [Correlation Filter Tracking](#correlation-filter-tracking)
    - [Handcrafted Features](#handcrafted-features)
  - [Deep Learning-based MOT](#deep-learning-based-mot)
    - [Tracking-by-Detection Pipeline](#tracking-by-detection-pipeline)
    - [Joint Detection and Embedding](#joint-detection-and-embedding)
    - [Graph-based Association](#graph-based-association)
    - [End-to-End Transformer-based Tracking](#end-to-end-transformer-based-tracking)
- [📝 Citation](#-citation)

---

## 📦 Datasets

| Dataset | Year | Domain | Target Type | Key Challenges | Link |
|---------|------|--------|-------------|----------------|------|
| MOT15 | 2015 | Pedestrian | Indoor / Outdoor | Varying camera motion, low resolution | [Official](https://motchallenge.net/data/MOT15/) |
| MOT16 | 2016 | Pedestrian | Street scenes | Occlusion, detection noise | [Official](https://motchallenge.net/data/MOT16/) |
| MOT17 | 2017 | Pedestrian | Multi-view street | Multiple detectors (DPM, FRCNN, SDP) | [Official](https://motchallenge.net/data/MOT17/) |
| MOT20 | 2020 | Pedestrian | Crowded scenes | Extreme density, heavy occlusion | [Official](https://motchallenge.net/data/MOT20/) |
| DanceTrack | 2022 | Dance / Performance | Similar-looking persons | Uniform appearance, non-linear motion | [Official](https://github.com/DanceTrack/DanceTrack) |
| SportsMOT | 2023 | Sports | Athletes (Basketball / Football / Volleyball) | Fast motion, frequent interaction | [Official](https://deeperaction.github.io/datasets/sportsmot.html) |
| BDD100K | 2020 | Autonomous Driving | Multi-class (car, pedestrian, truck, etc.) | Large scale, diverse weather & lighting | [Official](https://www.bdd100k.com/) |

---

## 📏 Metrics

| Metric | Full Name | Formula | Description |
|--------|-----------|---------|-------------|
| MOTA | Multiple Object Tracking Accuracy | $1 - \frac{\vert\text{FP}\vert + \vert\text{FN}\vert + \vert\text{IDSW}\vert}{\vert\text{gtDet}\vert}$ | Jointly penalizes FP, FN, and identity switches; can be negative |
| MOTP | Multiple Object Tracking Precision | $\frac{1}{\vert\text{TP}\vert} \sum_{m \in \text{TP}} \text{IoU}_m$ | Mean IoU over all true positives; measures localization quality |
| IDF1 | Identity F1 Score | $\frac{\vert\text{IDTP}\vert}{\vert\text{IDTP}\vert + 0.5\vert\text{IDFN}\vert + 0.5\vert\text{IDFP}\vert}$ | Trajectory-level metric; sensitive to prolonged identity switches |
| HOTA | Higher Order Tracking Accuracy | $\sqrt{\text{DetA}_{\alpha} \times \text{AssA}_{\alpha}}$ | Geometric mean of detection and association accuracy |
| MT | Mostly Tracked | — | % of GT trajectories covered > 80% of lifespan |
| ML | Mostly Lost | — | % of GT trajectories covered < 20% of lifespan |
| IDs | Identity Switches | — | Total count of incorrect identity changes |
| FPS | Frames Per Second | — | Inference speed; reflects real-time applicability |

---

## 🔬 Methods

### Traditional Object Tracking Methods

> Classical tracking approaches prior to deep learning, relying on probabilistic models and handcrafted representations.

#### Generative Methods

> Model the target appearance directly using probabilistic or density estimation approaches.

| Year | Method | Venue | Title | Link |
|------|--------|-------|-------|------|
| 1960 | Kalman Filter | J. Basic Engineering | A New Approach to Linear Filtering and Prediction Problems | [Paper](https://ieeexplore.ieee.org/abstract/document/5311910) |
| 2002 | Particle Filter | IEEE Trans. Signal Processing | A tutorial on particle filters for online nonlinear/non-Gaussian Bayesian tracking | [Paper](https://ieeexplore.ieee.org/document/978374) |
| 2003 | Mean Shift | IEEE TPAMI | Kernel-based object tracking | [Paper](https://ieeexplore.ieee.org/document/1195991) |

#### Discriminative Methods

> Learn a decision boundary between target and background.

| Year | Method | Venue | Title | Link |
|------|--------|-------|-------|------|
| 2004 | SVM Tracker | IEEE TPAMI | Support vector tracking | [Paper](https://ieeexplore.ieee.org/document/1307012) |
| 2009 | MILTrack | CVPR | Visual tracking with online Multiple Instance Learning | [Paper](https://ieeexplore.ieee.org/document/5206737) |
| 2015 | Struck | IEEE TPAMI | Struck: Structured Output Tracking with Kernels | [Paper](https://ieeexplore.ieee.org/document/7360205) |

#### Correlation Filter Tracking

> Exploit the circular correlation in frequency domain for efficient tracking.

| Year | Method | Venue | Title | Link |
|------|--------|-------|-------|------|
| 2010 | MOSSE | CVPR | Visual object tracking using adaptive correlation filters | [Paper](https://ieeexplore.ieee.org/document/5539960) |
| 2014 | KCF | IEEE TPAMI | High-Speed Tracking with Kernelized Correlation Filters | [Paper](https://ieeexplore.ieee.org/document/6870486) \| [Code](https://github.com/joaofaro/KCFcpp) |
| 2017 | ECO | CVPR | ECO: Efficient Convolution Operators for Tracking | [Paper](https://openaccess.thecvf.com/content_cvpr_2017/papers/Danelljan_ECO_Efficient_Convolution_CVPR_2017_paper.pdf) \| [Code](https://github.com/martin-danelljan/ECO) |
| 2017 | CSR-DCF | CVPR | Discriminative Correlation Filter with Channel and Spatial Reliability | [Paper](https://openaccess.thecvf.com/content_cvpr_2017/papers/Lukezic_Discriminative_Correlation_Filter_CVPR_2017_paper.pdf) \| [Code](https://github.com/alanlukezic/csr-dcf) |

#### Handcrafted Features

> Rely on manually engineered features such as HOG, LBP, and color histograms.

| Year | Feature | Venue | Type | Title | Link |
|------|---------|-------|------|-------|------|
| 2002 | LBP | IEEE TPAMI | Texture | Multiresolution gray-scale and rotation invariant texture classification with local binary patterns | [Paper](https://ieeexplore.ieee.org/document/1017623) |
| 2005 | HOG | CVPR | Shape / Gradient | Histograms of oriented gradients for human detection | [Paper](https://ieeexplore.ieee.org/document/1467360) |
| 2009 | Color Names | IEEE TIP | Color / Appearance | Learning Color Names for Real-World Applications | [Paper](https://ieeexplore.ieee.org/document/4982667) |

---

### Deep Learning-based MOT

> Methods leveraging deep neural networks for detection, appearance modeling, and data association.

#### Tracking-by-Detection Pipeline

> Separate detection and association stages; association typically uses IoU or ReID features.

| Year | Method | Venue | Title | Link |
|------|--------|-------|-------|------|
| 2020 | UnsupTrack | arXiv | Simple Unsupervised Multi-Object Tracking | [Paper](https://arxiv.org/abs/2006.02609) |
| 2020 | PointTrack | ECCV | Segment as Points for Efficient Online Multi-Object Tracking and Segmentation | [Paper](https://arxiv.org/abs/2007.01550) |
| 2020 | PointTrack++ | arXiv | PointTrack++ for Effective Online Multi-Object Tracking and Segmentation | [Paper](https://arxiv.org/abs/2007.01549) |

#### Joint Detection and Embedding

> Unify detection and ReID feature extraction in a single network.

| Year | Method | Venue | Title | Link |
|------|--------|-------|-------|------|
| 2020 | JDE | ECCV | Towards Real-Time Multi-Object Tracking | [Paper](https://arxiv.org/abs/1909.12605) |
| 2020 | CTracker | ECCV | Chained-Tracker: Chaining Paired Attentive Regression Results for End-to-End Joint Multiple-Object Detection and Tracking | [Paper](https://arxiv.org/abs/2007.14557) |
| 2020 | TubeTK | CVPR | TubeTK: Adopting Tubes to Track Multi-Object in a One-Step Training Model | [Paper](https://openaccess.thecvf.com/content_CVPR_2020/papers/Pang_TubeTK_Adopting_Tubes_to_Track_Multi-Object_in_a_One-Step_Training_CVPR_2020_paper.pdf) |
| 2021 | FairMOT | IJCV | FairMOT: On the Fairness of Detection and Re-Identification in Multiple Object Tracking | [Paper](https://arxiv.org/abs/2004.01888) |
| 2021 | SiamMOT | CVPR | SiamMOT: Siamese Multi-Object Tracking | [Paper](https://arxiv.org/abs/2105.11595) |
| 2021 | TraDeS | CVPR | Track to Detect and Segment: An Online Multi-Object Tracker | [Paper](https://arxiv.org/abs/2103.08808) |
| 2021 | TADAM | CVPR | Online Multiple Object Tracking with Cross-Task Synergy | [Paper](https://openaccess.thecvf.com/content/CVPR2021/papers/Guo_Online_Multiple_Object_Tracking_With_Cross-Task_Synergy_CVPR_2021_paper.pdf) |
| 2021 | SOTMOT | CVPR | Improving Multiple Object Tracking with Single Object Tracking | [Paper](https://openaccess.thecvf.com/content/CVPR2021/papers/Zheng_Improving_Multiple_Object_Tracking_With_Single_Object_Tracking_CVPR_2021_paper.pdf) |
| 2022 | CSTrack | TIP | Rethinking the competition between detection and ReID in Multi-Object Tracking | [Paper](https://arxiv.org/abs/2010.12138) |
| 2022 | RelationTrack | TMM | RelationTrack: Relation-aware Multiple Object Tracking with Decoupled Representation | [Paper](https://arxiv.org/abs/2105.04322) |
| 2024 | PASTA | NeurIPS | Is Multiple Object Tracking a Matter of Specialization? | [Paper](https://arxiv.org/abs/2411.00553) |
| 2025 | CrowdTrack | arXiv | CrowdTrack: A Benchmark for Difficult Multiple Pedestrian Tracking in Real Scenarios | [Paper](https://arxiv.org/abs/2507.02479) |

#### Graph-based Association

> Model detections and tracklets as graph nodes; use GNN or attention for association.

| Year | Method | Venue | Title | Link |
|------|--------|-------|-------|------|
| 2018 | GAT | ICLR | Graph Attention Networks | [Paper](https://arxiv.org/abs/1710.10903) |
| 2019 | EDA_GNN | arXiv | Graph Neural Based End-to-end Data Association Framework for Online Multiple-Object Tracking | [Paper](https://arxiv.org/abs/1907.05315) |
| 2020 | MPNTracker | CVPR | Learning a Neural Solver for Multiple Object Tracking | [Paper](https://arxiv.org/abs/1912.07515) |
| 2020 | GNMOT | WACV | Graph Networks for Multiple Object Tracking | [Paper](https://openaccess.thecvf.com/content_WACV_2020/papers/Li_Graph_Networks_for_Multiple_Object_Tracking_WACV_2020_paper.pdf) |
| 2020 | TPAGT | arXiv | Tracklets Predicting Based Adaptive Graph Tracking | [Paper](https://arxiv.org/abs/2010.09015) |
| 2021 | GMTracker | CVPR | Learnable Graph Matching: Incorporating Graph Partitioning with Deep Feature Learning for Multiple Object Tracking | [Paper](https://arxiv.org/abs/2103.16178) |
| 2021 | TrackMPNN | arXiv | TrackMPNN: A Message Passing Graph Neural Architecture for Multi-Object Tracking | [Paper](https://arxiv.org/abs/2101.04206) |
| 2021 | GSDT | ICRA | Joint Object Detection and Multi-Object Tracking with Graph Neural Networks | [Paper](https://arxiv.org/abs/2006.13164) |
| 2021 | CorrTracker | CVPR | Multiple Object Tracking with Correlation Learning | [Paper](https://arxiv.org/abs/2104.03541) |
| 2022 | LPT | CVPR | Learning of Global Objective for Network Flow in Multi-Object Tracking | [Paper](https://openaccess.thecvf.com/content/CVPR2022/papers/Li_Learning_of_Global_Objective_for_Network_Flow_in_Multi-Object_Tracking_CVPR_2022_paper.pdf) |
| 2023 | TransMOT | WACV | TransMOT: Spatial-Temporal Graph Transformer for Multiple Object Tracking | [Paper](https://arxiv.org/abs/2104.00194) |
| 2023 | MotionTrack | CVPR | MotionTrack: Learning Robust Short-term and Long-term Motions for Multi-Object Tracking | [Paper](https://arxiv.org/abs/2303.10404) |
| 2023 | TrackFlow | ICCV | TrackFlow: Multi-Object Tracking with Normalizing Flows | [Paper](https://arxiv.org/abs/2308.11513) |

#### End-to-End Transformer-based Tracking

> Formulate tracking as a sequence-to-sequence problem using Transformer architectures.

| Year | Method | Venue | Title | Link |
|------|--------|-------|-------|------|
| 2021 | TransTrack | arXiv | TransTrack: Multiple Object Tracking with Transformer | [Paper](https://arxiv.org/abs/2012.15460) |
| 2021 | PermaTrack | ICCV | Learning to Track with Object Permanence | [Paper](https://arxiv.org/abs/2103.14258) |
| 2022 | TrackFormer | CVPR | TrackFormer: Multi-Object Tracking with Transformers | [Paper](https://arxiv.org/abs/2101.02702) |
| 2022 | MOTR | ECCV | MOTR: End-to-End Multiple-Object Tracking with Transformer | [Paper](https://arxiv.org/abs/2105.03247) |
| 2022 | GTR | CVPR | Global Tracking Transformers | [Paper](https://arxiv.org/abs/2203.13250) |
| 2022 | MeMOT | CVPR | MeMOT: Multi-Object Tracking with Memory | [Paper](https://arxiv.org/abs/2203.16761) |
| 2022 | TransCenter | TPAMI | TransCenter: Transformers with Dense Representations for Multiple-Object Tracking | [Paper](https://arxiv.org/abs/2103.15145) |
| 2022 | P3AFormer | ECCV | Tracking Objects as Pixel-wise Distributions | [Paper](https://arxiv.org/abs/2207.05518) |
| 2022 | UTT | CVPR | Unified Transformer Tracker for Object Tracking | [Paper](https://arxiv.org/abs/2203.15175) |
| 2022 | Unicorn | ECCV | Towards Grand Unification of Object Tracking | [Paper](https://arxiv.org/abs/2207.07078) |
| 2023 | MeMOTR | ICCV | MeMOTR: Long-Term Memory-Augmented Transformer for Multi-Object Tracking | [Paper](https://arxiv.org/abs/2307.15700) |
| 2024 | MASA | CVPR | Matching Anything by Segmenting Anything | [Paper](https://arxiv.org/abs/2406.04221) |
| 2024 | GeneralTrack | CVPR | Towards Generalizable Multi-Object Tracking | [Paper](https://arxiv.org/abs/2406.00429) |
| 2024 | SambaMOTR | arXiv | Samba: Synchronized Set-of-Sequences Modeling for Multiple Object Tracking | [Paper](https://arxiv.org/abs/2410.01806) |
| 2025 | CO-MOT | ICLR | Bridging the Gap Between End-to-end and Non-End-to-end Multi-Object Tracking | [Paper](https://arxiv.org/abs/2305.12724) |
| 2025 | MOTIP | CVPR | Multiple Object Tracking as ID Prediction | [Paper](https://arxiv.org/abs/2403.16848) |

---

## 📝 Citation

If you find this survey helpful, please consider citing:

```bibtex
@article{yourname2025mot,
  title   = {A Survey on Multi-Object Tracking},
  author  = {Your Name},
  journal = {arXiv preprint arXiv:xxxx.xxxxx},
  year    = {2025}
}
```

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request or open an Issue.
