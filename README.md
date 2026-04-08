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

| Year | Method | Publication | Title | Link |
|------|--------|-------|-------|------|
| 1960 | Kalman Filter | J. Basic Engineering | A New Approach to Linear Filtering and Prediction Problems | [Paper](https://ieeexplore.ieee.org/abstract/document/5311910) |
| 2002 | Particle Filter | IEEE Trans. Signal Processing | A tutorial on particle filters for online nonlinear/non-Gaussian Bayesian tracking | [Paper](https://ieeexplore.ieee.org/document/978374) |
| 2003 | Mean Shift | IEEE TPAMI | Kernel-based object tracking | [Paper](https://ieeexplore.ieee.org/document/1195991) |
| 2004 | SVM Tracker | IEEE TPAMI | Support vector tracking | [Paper](https://ieeexplore.ieee.org/document/1307012) |
| 2009 | MILTrack | CVPR | Visual tracking with online Multiple Instance Learning | [Paper](https://ieeexplore.ieee.org/document/5206737) |
| 2015 | Struck | IEEE TPAMI | Struck: Structured Output Tracking with Kernels | [Paper](https://ieeexplore.ieee.org/document/7360205) |
| 2010 | MOSSE | CVPR | Visual object tracking using adaptive correlation filters | [Paper](https://ieeexplore.ieee.org/document/5539960) |
| 2014 | KCF | IEEE TPAMI | High-Speed Tracking with Kernelized Correlation Filters | [Paper](https://ieeexplore.ieee.org/document/6870486) \| [Code](https://github.com/joaofaro/KCFcpp) |
| 2017 | ECO | CVPR | ECO: Efficient Convolution Operators for Tracking | [Paper](https://openaccess.thecvf.com/content_cvpr_2017/papers/Danelljan_ECO_Efficient_Convolution_CVPR_2017_paper.pdf) \| [Code](https://github.com/martin-danelljan/ECO) |
| 2017 | CSR-DCF | CVPR | Discriminative Correlation Filter with Channel and Spatial Reliability | [Paper](https://openaccess.thecvf.com/content_cvpr_2017/papers/Lukezic_Discriminative_Correlation_Filter_CVPR_2017_paper.pdf) \| [Code](https://github.com/alanlukezic/csr-dcf) |

#### Handcrafted Features

> Rely on manually engineered features such as HOG, LBP, and color histograms.

| Year | Feature | Publication | Type | Title | Link |
|------|---------|-------|------|-------|------|
| 2002 | LBP | IEEE TPAMI | Texture | Multiresolution gray-scale and rotation invariant texture classification with local binary patterns | [Paper](https://ieeexplore.ieee.org/document/1017623) |
| 2005 | HOG | CVPR | Shape / Gradient | Histograms of oriented gradients for human detection | [Paper](https://ieeexplore.ieee.org/document/1467360) |
| 2009 | Color Names | IEEE TIP | Color / Appearance | Learning Color Names for Real-World Applications | [Paper](https://ieeexplore.ieee.org/document/4982667) |

---

### Deep Learning-based MOT

> Methods leveraging deep neural networks for detection, appearance modeling, and data association.

#### Tracking-by-Detection Pipeline

> Separate detection and association stages; association typically uses IoU or ReID features.

| Year | Method | Publication | Category | Title | Link |
|------|--------|-------|----------|-------|------|
| 2005 | Siamese Network | CVPR | Appearance | Learning a Similarity Metric Discriminatively, with Application to Face Verification | [Paper](https://ieeexplore.ieee.org/document/1467314) |
| 2015 | Faster R-CNN | NeurIPS | Detection | Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks | [Paper](https://arxiv.org/abs/1506.01497) |
| 2016 | YOLO | CVPR | Detection | You Only Look Once: Unified, Real-Time Object Detection | [Paper](https://arxiv.org/abs/1506.02640) |
| 2016 | Social LSTM | CVPR | Motion | Social LSTM: Human Trajectory Prediction in Crowded Spaces | [Paper](https://ieeexplore.ieee.org/document/7780479) |
| 2016 | Deep SORT | ICIP | Appearance | Simple Online and Realtime Tracking with a Deep Association Metric | [Paper](https://arxiv.org/abs/1703.07402) |
| 2017 | FPN | CVPR | Detection | Feature Pyramid Networks for Object Detection | [Paper](https://arxiv.org/abs/1612.03144) |
| 2017 | Triplet Loss | arXiv | Appearance | In Defense of the Triplet Loss for Person Re-Identification | [Paper](https://arxiv.org/abs/1703.07737) |
| 2017 | Deep Network Flow | CVPR | Association | Deep Network Flow for Multi-Object Tracking | [Paper](https://arxiv.org/abs/1706.08482) |
| 2017 | MobileNets | arXiv | Detection | MobileNets: Efficient Convolutional Neural Networks for Mobile Vision Applications | [Paper](https://arxiv.org/abs/1704.04861) |
| 2018 | Cascade R-CNN | CVPR | Detection | Cascade R-CNN: Delving into High Quality Object Detection | [Paper](https://arxiv.org/abs/1712.00726) |
| 2018 | SE-Net | CVPR | Detection | Squeeze-and-Excitation Networks | [Paper](https://arxiv.org/abs/1709.01507) |
| 2018 | Non-local NN | CVPR | Detection | Non-Local Neural Networks | [Paper](https://arxiv.org/abs/1711.07971) |
| 2018 | Social GAN | CVPR | Motion | Social GAN: Socially Acceptable Trajectories with Generative Adversarial Networks | [Paper](https://arxiv.org/abs/1803.10892) |
| 2018 | PCB | ECCV | Appearance | Beyond Part Models: Person Retrieval with Refined Part Pooling | [Paper](https://arxiv.org/abs/1711.09349) |
| 2018 | HA-Net | CVPR | Appearance | Harmonious Attention Network for Person Re-Identification | [Paper](https://arxiv.org/abs/1802.08122) |
| 2018 | SGGNN | ECCV | Appearance | Person Re-Identification with Deep Similarity-Guided Graph Neural Network | [Paper](https://arxiv.org/abs/1807.09975) |
| 2019 | EfficientNet | ICML | Detection | EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks | [Paper](https://arxiv.org/abs/1905.11946) |
| 2019 | ABD-Net | ICCV | Appearance | ABD-Net: Attentive but Diverse Person Re-Identification | [Paper](https://arxiv.org/abs/1908.01114) |
| 2019 | Bag of Tricks | CVPRW | Appearance | Bag of Tricks and a Strong Baseline for Deep Person Re-Identification | [Paper](https://arxiv.org/abs/1903.07071) |
| 2019 | Social-BiGAT | NeurIPS | Motion | Social-BiGAT: Multimodal Trajectory Forecasting using Bicycle-GAN and Graph Attention Networks | [Paper](https://arxiv.org/abs/1907.03395) |
| 2020 | DETR | arXiv | Detection | End-to-End Object Detection with Transformers | [Paper](https://arxiv.org/abs/2005.12872) |
| 2020 | YOLOv4 | arXiv | Detection | YOLOv4: Optimal Speed and Accuracy of Object Detection | [Paper](https://arxiv.org/abs/2004.10934) |
| 2020 | Lifted DP | ICML | Association | Lifted Disjoint Paths with Application in Multiple Object Tracking | [Paper](https://arxiv.org/abs/2008.09577) |
| 2021 | Deformable DETR | arXiv | Detection | Deformable DETR: Deformable Transformers for End-to-End Object Detection | [Paper](https://arxiv.org/abs/2010.04159) |
| 2021 | YOLOX | arXiv | Detection | YOLOX: Exceeding YOLO Series in 2021 | [Paper](https://arxiv.org/abs/2107.08430) |
| 2021 | QDTrack | arXiv | Appearance | Quasi-Dense Similarity Learning for Multiple Object Tracking | [Paper](https://arxiv.org/abs/2006.06664) |
| 2021 | FairMOT | IJCV | Appearance | FairMOT: On the Fairness of Detection and Re-Identification in Multiple Object Tracking | [Paper](https://arxiv.org/abs/2004.01888) |
| 2021 | Multi-track Pooling | CVPR | Appearance | Discriminative Appearance Modeling with Multi-Track Pooling for Real-Time Multi-Object Tracking | [Paper](https://arxiv.org/abs/2101.12875) |
| 2021 | TransReID | ICCV | Appearance | TransReID: Transformer-Based Object Re-Identification | [Paper](https://arxiv.org/abs/2102.04378) |
| 2021 | ArTIST | CVPR | Association | Probabilistic Tracklet Scoring and Inpainting for Multiple Object Tracking | [Paper](https://arxiv.org/abs/2012.10077) |
| 2022 | DINO | arXiv | Detection | DINO: DETR with Improved DeNoising Anchor Boxes for End-to-End Object Detection | [Paper](https://arxiv.org/abs/2203.03605) |
| 2022 | ByteTrack | ECCV | Association | ByteTrack: Multi-Object Tracking by Associating Every Detection Box | [Paper](https://arxiv.org/abs/2110.06864) |
| 2022 | BoT-SORT | arXiv | Association | BoT-SORT: Robust Associations Multi-Pedestrian Tracking | [Paper](https://arxiv.org/abs/2206.14651) |
| 2022 | MAA | WACV | Association | Modelling Ambiguous Assignments for Multi-Person Tracking in Crowds | [Paper](https://arxiv.org/abs/2201.01049) |
| 2023 | OC-SORT | CVPR | Association | Observation-Centric SORT: Rethinking SORT for Robust Multi-Object Tracking | [Paper](https://arxiv.org/abs/2203.14360) |
| 2023 | StrongSORT | TMM | Association | StrongSORT: Make DeepSORT Great Again | [Paper](https://arxiv.org/abs/2202.13514) |
| 2023 | SGT | WACV | Association | Detection Recovery in Online Multi-Object Tracking with Sparse Graph Tracker | [Paper](https://arxiv.org/abs/2205.00968) |
| 2023 | ColTrack | ICCV | Association | Collaborative Tracking Learning for Frame-Rate-Insensitive Multi-Object Tracking | [Paper](https://arxiv.org/abs/2308.05911) |
| 2023 | Deep OC-SORT | ICIP | Appearance | Deep OC-SORT: Multi-Pedestrian Tracking by Adaptive Re-Identification | [Paper](https://arxiv.org/abs/2302.11813) |
| 2023 | GHOST | CVPR | Appearance | Simple Cues Lead to a Strong Multi-Object Tracker | [Paper](https://arxiv.org/abs/2206.04656) |
| 2024 | UCMCTrack | AAAI | Association | UCMCTrack: Multi-Object Tracking with Uniform Camera Motion Compensation | [Paper](https://arxiv.org/abs/2312.08952) |
| 2024 | Hybrid-SORT | AAAI | Association | Hybrid-SORT: Weak Cues Matter for Online Multi-Object Tracking | [Paper](https://arxiv.org/abs/2308.00783) |



#### Joint Detection and Embedding

> Unify detection and ReID feature extraction in a single network.

| Year | Method | Publication | Title | Link |
|------|--------|-------|-------|------|
| 2020 | UnsupTrack | arXiv | Simple Unsupervised Multi-Object Tracking | [Paper](https://arxiv.org/abs/2006.02609) |
| 2020 | PointTrack | ECCV | Segment as Points for Efficient Online Multi-Object Tracking and Segmentation | [Paper](https://arxiv.org/abs/2007.01550) |
| 2020 | PointTrack++ | arXiv | PointTrack++ for Effective Online Multi-Object Tracking and Segmentation | [Paper](https://arxiv.org/abs/2007.01549) |
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

| Year | Method | Publication | Title | Link |
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

| Year | Method | Publication | Title | Link |
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
