# Survey-on-MOT
# 🎯 Awesome Multi-Object Tracking (MOT) Survey

> A comprehensive survey of Multi-Object Tracking (MOT) methods, datasets, and benchmarks.  


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

| Year | Method | Venue | Title | Link |
|------|--------|-------|------------|------|
| 1960 | Kalman&nbsp;Filter | Journal of Basic Engineering  | A New Approach to Linear Filtering and Prediction Problems | [Paper](https://ieeexplore.ieee.org/abstract/document/5311910) |
| 2002 | Particle&nbsp;Filter| IEEE Trans. Signal Processing | A tutorial on particle filters for online nonlinear/non-Gaussian Bayesian tracking | [Paper](https://ieeexplore.ieee.org/document/978374) |
| 2003 | Mean&nbsp;Shift     | IEEE TPAMI                    | Kernel-based object tracking | [Paper](https://ieeexplore.ieee.org/document/1195991) |
| 2004 | SVM&nbsp;Tracker | IEEE TPAMI | Support vector tracking | [Paper](https://ieeexplore.ieee.org/document/1307012) |
| 2009 | MILTrack    | CVPR       | Visual tracking with online Multiple Instance Learning | [Paper](https://ieeexplore.ieee.org/document/5206737) |
| 2015 | Struck      | IEEE TPAMI | Struck: Structured Output Tracking with Kernels | [Paper](https://ieeexplore.ieee.org/document/7360205) |
| 2010 | MOSSE | CVPR | Visual object tracking using adaptive correlation filters | [Paper](https://ieeexplore.ieee.org/document/5539960) |
| 2014 | KCF   | IEEE TPAMI | High-Speed Tracking with Kernelized Correlation Filters | [Paper](https://ieeexplore.ieee.org/document/6870486) \| [Code](https://github.com/joaofaro/KCFcpp) |
| 2017 | ECO   | CVPR | ECO:Efficient Convolution Operators for Tracking | [Paper](https://openaccess.thecvf.com/content_cvpr_2017/papers/Danelljan_ECO_Efficient_Convolution_CVPR_2017_paper.pdf) \| [Code](https://github.com/martin-danelljan/ECO) |
| 2017 | CSR‑DCF | CVPR | Discriminative Correlation Filter with Channel and Spatial Reliability | [Paper](https://openaccess.thecvf.com/content_cvpr_2017/papers/Lukezic_Discriminative_Correlation_Filter_CVPR_2017_paper.pdf) \| [Code](https://github.com/alanlukezic/csr-dcf) |


---
#### Handcrafted Features
> Rely on manually engineered features such as HOG, LBP, and color histograms.

| Year | Feature | Venue | Type | Title | Link |
|------|---------|-------|------|------------|------|
| 2002 | LBP         | IEEE TPAMI | Texture            | Multiresolution gray-scale and rotation invariant texture classification with local binary patterns | [Paper](https://ieeexplore.ieee.org/document/1017623) |
| 2005 | HOG         | CVPR       | Shape / Gradient   | Histograms of oriented gradients for human detection | [Paper](https://ieeexplore.ieee.org/document/1467360) |
| 2009 | Color&nbsp;Names | IEEE TIP   | Color / Appearance | Learning Color Names for Real-World Applications | [Paper](https://ieeexplore.ieee.org/document/4982667) |

---


### Joint Detection and Embedding (JDE) Methods

> Unify detection and re-identification within a single forward pass, trading sequential-pipeline redundancy for inter-task optimization tension.

| Year | Method | Venue | Titlw | Link |
|------|--------|-------|------------|------|
| 2020 | JDE         | ECCV    | Towards Real-Time Multi-Object Tracking | [Paper](https://arxiv.org/abs/1909.12605) |
| 2020 | CTracker    | ECCV    | Chained-Tracker: Chaining Paired Attentive Regression Results for End-to-End Joint Multiple-Object Detection and Tracking | [Paper](https://arxiv.org/abs/2007.14557) |
| 2020 | TubeTK      | CVPR    | TubeTK: Adopting Tubes to Track Multi-Object in a One-Step Training Model | [Paper](https://openaccess.thecvf.com/content_CVPR_2020/papers/Pang_TubeTK_Adopting_Tubes_to_Track_Multi-Object_in_a_One-Step_Training_CVPR_2020_paper.pdf) |
| 2021 | FairMOT     | IJCV    | FairMOT: On the Fairness of Detection and Re-Identification in Multiple Object Tracking | [Paper](https://arxiv.org/abs/2004.01888) |
| 2021 | SiamMOT     | CVPR    | SiamMOT: Siamese Multi-Object Tracking | [Paper](https://arxiv.org/abs/2105.11595) |
| 2021 | TraDeS      | CVPR    | Track to Detect and Segment: An Online Multi-Object Tracker | [Paper](https://arxiv.org/abs/2103.08808) |
| 2021 | TADAM       | CVPR    | Online Multiple Object Tracking with Cross-Task Synergy | [Paper](https://openaccess.thecvf.com/content/CVPR2021/papers/Guo_Online_Multiple_Object_Tracking_With_Cross-Task_Synergy_CVPR_2021_paper.pdf) |
| 2021 | SOTMOT      | CVPR    | Improving Multiple Object Tracking with Single Object Tracking | [Paper](https://openaccess.thecvf.com/content/CVPR2021/papers/Zheng_Improving_Multiple_Object_Tracking_With_Single_Object_Tracking_CVPR_2021_paper.pdf) |
| 2022 | CSTrack     | TIP     | Rethinking the competition between detection and ReID in Multi-Object Tracking | [Paper](https://arxiv.org/abs/2010.12138) |
| 2022 | RelationTrack | TMM   | RelationTrack: Relation-aware Multiple Object Tracking with Decoupled Representation | [Paper](https://arxiv.org/abs/2105.04322) |
| 2024 | PASTA       | NeurIPS | Is Multiple Object Tracking a Matter of Specialization? | [Paper](https://arxiv.org/abs/2411.00553) |
| 2025 | CrowdTrack  | arXiv   | CrowdTrack: A Benchmark for Difficult Multiple Pedestrian Tracking in Real Scenarios | [Paper](https://arxiv.org/abs/2507.02479) |
| 2020 | UnsupTrack  | arXiv   | Simple Unsupervised Multi-Object Tracking | [Paper](https://arxiv.org/abs/2006.02609) |


---
### Graph-based Association Methods
> Cast data association as relational reasoning over a graph of detections and tracklets, where message passing or structured matching replaces hand-crafted pairwise cost matrices with learned, globally aware assignment.

| Year | Method | Venue | Highlights | Link |
|------|--------|-------|------------|------|
| 2018 | GAT          | ICLR  | Foundational graph attention mechanism that lets nodes attend over neighbours with learned importance weights, later adopted as the backbone of many MOT association modules | [Paper](https://arxiv.org/abs/1710.10903) |
| 2019 | EDA_GNN      | arXiv | Reformulates frame-by-frame association as maximum weighted bipartite matching solved by a GNN optimisation module, with a multi-level matrix loss enabling affinity learning and matching to co-adapt during training | [Paper](https://arxiv.org/abs/1907.05315) |
| 2020 | MPNTracker   | CVPR  | Casts association as edge classification over a temporal graph; node features are refined through iterative time-aware message passing, and learned edge correspondence replaces hand-crafted cost matrices | [Paper](https://arxiv.org/abs/1912.07515) |
| 2020 | GNMOT        | WACV  | Designs separate appearance and motion graph networks to capture appearance and motion similarity respectively, with a carefully designed updating mechanism for nodes, edges, and the global graph variable | [Paper](https://openaccess.thecvf.com/content_WACV_2020/papers/Li_Graph_Networks_for_Multiple_Object_Tracking_WACV_2020_paper.pdf) |
| 2020 | TPAGT        | arXiv | Predicts tracklet positions via sparse optical flow and re-extracts features at predicted locations to preserve temporal alignment, before an adaptive GNN fuses spatial, appearance, and historical cues into association scores | [Paper](https://arxiv.org/abs/2010.09015) |
| 2021 | GMTracker    | CVPR  | Integrates graph partitioning with deep feature learning in a fully differentiable framework, jointly optimising representation and matching objective to overcome the suboptimality of greedy local matching | [Paper](https://arxiv.org/abs/2103.16178) |
| 2021 | TrackMPNN    | arXiv | Extends message-passing association to the online setting via dynamic undirected graphs over multiple timesteps, allowing incremental revision of previous assignments as new detections arrive | [Paper](https://arxiv.org/abs/2101.04206) |
| 2021 | GSDT         | ICRA  | Models spatial correlations among candidate objects as a graph in which convolutions propagate relational context between tracklet features and current-frame detections, jointly learning detection and tracking end-to-end | [Paper](https://arxiv.org/abs/2006.13164) |
| 2021 | CorrTracker  | CVPR  | Embeds motion evidence directly into appearance representations through explicit cross-frame correlation maps that encode each object's spatial displacement distribution, removing the need for a separate motion estimator | [Paper](https://arxiv.org/abs/2104.03541) |
| 2022 | LPT          | CVPR  | Replaces manually designed affinity matrices with a learned global objective that maps trajectory structures to assignment costs, accommodating scene-specific association patterns inaccessible to fixed formulations | [Paper](https://openaccess.thecvf.com/content/CVPR2022/papers/Li_Learning_of_Global_Objective_for_Network_Flow_in_Multi-Object_Tracking_CVPR_2022_paper.pdf) |
| 2023 | TransMOT     | WACV  | Combines a spatial graph over co-occurring intra-frame objects with a temporal transformer that aggregates structured representations across frames, enabling joint reasoning about co-presence and configuration evolution | [Paper](https://arxiv.org/abs/2104.00194) |
| 2023 | MotionTrack  | CVPR  | Jointly learns short-term displacement features that capture frame-to-frame velocity and long-term trajectory patterns that sustain identity across occlusion gaps, the two scales being complementary by design | [Paper](https://arxiv.org/abs/2303.10404) |
| 2023 | TrackFlow    | ICCV  | Models the conditional joint distribution of heterogeneous cues — motion, appearance, and depth — via normalising flows, yielding a unified likelihood score that obviates manual hyperparameter balancing across cost terms | [Paper](https://arxiv.org/abs/2308.11513) |

---
### End-to-End Transformer-based Tracking Methods

> Cast localisation, identity, and temporal correspondence as a single set-prediction problem trained under a permutation-invariant objective, dissolving the modular boundaries between detection, appearance modelling, and association.

| Year | Method | Venue | Highlights | Link |
|------|--------|-------|------------|------|
| 2020 | PointTrack    | ECCV    | Represents instances as compact point sets that replace per-pixel similarity computation with point-level characteristic matching, reducing computational overhead while preserving association accuracy under complex occlusion | [Paper](https://arxiv.org/abs/2007.01550) |
| 2020 | PointTrack++  | arXiv   | Extends PointTrack with refinements for online multi-object tracking and segmentation, retaining the point-set representation while improving robustness in dense scenes | [Paper](https://arxiv.org/abs/2007.01549) |
| 2021 | TransTrack    | arXiv   | Early instantiation of query-based tracking in which cross-attention propagates object features from the preceding frame to current encoder outputs, while final association is still resolved through IoU matching | [Paper](https://arxiv.org/abs/2012.15460) |
| 2021 | PermaTrack    | ICCV    | Embeds an object-permanence prior through a spatio-temporal ConvGRU that predicts plausible locations for fully occluded targets, sustaining trajectory continuity without re-identification at re-emergence | [Paper](https://arxiv.org/abs/2103.14258) |
| 2022 | TrackFormer   | CVPR    | Adopts an autoregressive query propagation strategy in which track queries are carried forward across frames and jointly decoded with new detection queries | [Paper](https://arxiv.org/abs/2101.02702) |
| 2022 | MOTR          | ECCV    | Introduces persistent track queries that each model a single trajectory through frame-by-frame decoder updates, accumulating temporal context via self-attention over historical states and cross-attention with current detections | [Paper](https://arxiv.org/abs/2105.03247) |
| 2022 | GTR           | CVPR    | Broadens the temporal scope of query propagation by operating over frame sequences rather than pairs, aggregating evidence across all frames simultaneously through trajectory-level queries | [Paper](https://arxiv.org/abs/2203.13250) |
| 2022 | MeMOT         | CVPR    | Per-object memory module that stores appearance and motion observations over an extended history, queried at each step via transformer attention to counteract representation drift in long sequences | [Paper](https://arxiv.org/abs/2203.16761) |
| 2022 | TransCenter   | TPAMI   | Dense heatmap queries on high-resolution feature maps recover the recall that sparse DETR-style query sets sacrifice in crowded scenes while retaining global context through attention | [Paper](https://arxiv.org/abs/2103.15145) |
| 2022 | P3AFormer     | ECCV    | Models each object as a spatial pixel distribution propagated via optical flow, recovering discriminability in densely crowded scenes where overlapping bounding boxes render box-level features ambiguous | [Paper](https://arxiv.org/abs/2207.05518) |
| 2022 | UTT           | CVPR    | Demonstrates that single-object and multi-object tracking benefit from joint training through a shared transformer backbone, with complementary supervisory signals improving performance on both tasks | [Paper](https://arxiv.org/abs/2203.15175) |
| 2022 | Unicorn       | ECCV    | Extends task unification to four tracking-related problems within a single model, with successful cross-task transfer suggesting that their representational requirements are more closely aligned than traditional separate treatments assume | [Paper](https://arxiv.org/abs/2207.07078) |
| 2023 | MeMOTR        | ICCV    | Integrates long-term memory within an end-to-end architecture by appending a memory bank to track queries, ensuring that features from arbitrarily distant frames remain accessible during cross-attention with current detections | [Paper](https://arxiv.org/abs/2307.15700) |
| 2024 | MASA          | CVPR    | Leverages zero-shot segmentation to decouple correspondence from category-specific training, enabling tracking of arbitrary object classes without per-category supervision | [Paper](https://arxiv.org/abs/2406.04221) |
| 2024 | GeneralTrack  | CVPR    | Identifies the architectural and training conditions under which cross-domain transfer becomes achievable, advancing tracking generalisation beyond fixed scene and category distributions | [Paper](https://arxiv.org/abs/2406.00429) |
| 2024 | SambaMOTR     | arXiv   | Replaces the transformer decoder with a Mamba state-space model that processes each tracklet sequence at linear time complexity, while cross-sequence attention synchronises hidden states across co-occurring objects | [Paper](https://arxiv.org/abs/2410.01806) |
| 2025 | CO-MOT        | ICLR    | Coopetition label assignment that includes tracked objects in the matching targets for detection queries during intermediate decoder layers, complemented by shadow query copies that enforce discriminative representations via one-to-set optimisation | [Paper](https://arxiv.org/abs/2305.12724) |
| 2025 | MOTIP         | CVPR    | Departs from matching-based formulations by predicting each detection's identity index directly from its query representation, collapsing detection and association into a single classification head that admits true end-to-end optimisation | [Paper](https://arxiv.org/abs/2403.16848) |

---


## Citation






## Contributing

Feel free to open a PR or Issue to add papers or fix errors!

---

