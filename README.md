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
- [Benchmarks](#benchmarks)
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
|--------|------|------|----------|------|
| MOT15 | 2015 | Pedestrian | Indoor / Outdoor | Varying camera motion, low resolution | Indoor / Outdoor | [官网](https://motchallenge.net/data/MOT15/) |
| MOT16 | 2016 | Pedestrian | Street scenes | Indoor / Outdoor | Indoor / Outdoor |[官网](https://motchallenge.net/data/MOT16/) |
| MOT17 | 2017 | Pedestrian | Multi-view street | Indoor / Outdoor | Indoor / Outdoor |[官网](https://motchallenge.net/data/MOT17/) |
| MOT20 | 2020 | Pedestrian | Crowded scenes | Indoor / Outdoor | Indoor / Outdoor |[官网](https://motchallenge.net/data/MOT20/) |
| DanceTrack | 2022 | Dance / Performance | Similar-looking persons | Indoor / Outdoor | Indoor / Outdoor |[官网](https://github.com/DanceTrack/DanceTrack) |
SportsMOT | 2023 | Sports | Athletes (Basketball / Football / Volleyball) | Indoor / Outdoor | Indoor / Outdoor |[官网](https://deeperaction.github.io/datasets/sportsmot.html)|
| BDD100K | 2020 | Autonomous Driving | Multi-class (car, pedestrian, truck, etc.) | Indoor / Outdoor | Indoor / Outdoor |[官网](https://www.bdd100k.com/) |

---

## Metrics

| 指标 | 全称 | 说明 |
|------|------|------|
| MOTA | Multiple Object Tracking Accuracy | 综合漏检、误检和 ID 切换 |
| IDF1 | ID F1 Score | 衡量 ID 一致性 |
| HOTA | Higher Order Tracking Accuracy | 兼顾检测与关联的综合指标 |
| MT | Mostly Tracked | 追踪帧数 > 80% 的轨迹比例 |
| ML | Mostly Lost | 追踪帧数 < 20% 的轨迹比例 |
| IDs | ID Switches | ID 切换次数 |
| FPS | Frames Per Second | 推理速度 |

---

## Benchmarks

### MOT17 (Private Detector)

| 排名 | 方法 | HOTA | MOTA | IDF1 | FPS |
|------|------|------|------|------|-----|
| 1 | ... | ... | ... | ... | ... |
| 2 | ... | ... | ... | ... | ... |

> 数据来源：[MOTChallenge](https://motchallenge.net/)

---

## Methods

### Traditional Object Tracking Methods

#### Generative Methods

> 通过对目标外观建模来定位目标，如均值漂移、粒子滤波等。  
> Model target appearance to locate objects (e.g., Mean Shift, Particle Filter).

| 年份 | 方法 | 会议/期刊 | 亮点 | 链接 |
|------|------|-----------|------|------|
| ... | ... | ... | ... | ... |

---

#### Discriminative Methods

> 将追踪转化为前景/背景二分类问题，在线更新分类器。  
> Treat tracking as foreground/background classification with online classifier updates.

| 年份 | 方法 | 会议/期刊 | 亮点 | 链接 |
|------|------|-----------|------|------|
| ... | ... | ... | ... | ... |

---

#### Correlation Filter Tracking

> 利用循环矩阵和傅里叶变换高效计算目标响应图。  
> Efficient target response map computation via circulant matrices and Fourier transform.

| 年份 | 方法 | 会议/期刊 | 亮点 | 链接 |
|------|------|-----------|------|------|
| 2010 | MOSSE | CVPR | 首个相关滤波追踪器 | [Paper](链接) |
| 2014 | KCF | TPAMI | 核技巧 + 多通道特征 | [Paper](链接) \| [Code](链接) |
| ... | ... | ... | ... | ... |

---

#### Handcrafted Features

> 依赖 HOG、LBP、颜色直方图等人工设计特征。  
> Rely on manually engineered features such as HOG, LBP, and color histograms.

| 年份 | 方法 | 会议/期刊 | 特征类型 | 链接 |
|------|------|-----------|---------|------|
| ... | ... | ... | ... | ... |

---

#### Limitations of Traditional Methods

> 传统方法在遮挡、光照变化、密集场景下性能有限，推动了深度学习方法的发展。  
> Traditional methods struggle with occlusion, illumination change, and crowded scenes, motivating deep learning approaches.

---

### Deep Learning-based MOT

---

#### Tracking-by-Detection Pipeline

> 先检测，后关联的经典两阶段框架。  
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

> 共享 Backbone，在单一网络中同时完成检测与 Re-ID。  
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

> 将检测框和轨迹建模为图节点，用 GNN 学习关联权重。  
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

> 基于注意力机制，无需手工设计后处理模块。  
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

欢迎提交 PR 或 Issue 来补充论文、修正错误！  
Feel free to open a PR or Issue to add papers or fix errors!

---

