# Survey-on-MOT
# 🎯 Awesome Multi-Object Tracking (MOT) Survey

> A comprehensive survey of Multi-Object Tracking (MOT) methods, datasets, and benchmarks.  
> 持续更新中 | Continuously updated.


[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
![Last Updated](https://img.shields.io/github/last-commit/你的用户名/仓库名)

---

## 📖 目录 / Table of Contents

- [简介 Introduction](#简介-introduction)
- [综述论文 Survey Papers](#综述论文-survey-papers)
- [方法分类 Methods](#方法分类-methods)
  - [检测器 Detectors](#检测器-detectors)
  - [Re-ID 模块](#re-id-模块)
  - [Tracking-by-Detection](#tracking-by-detection)
  - [Joint Detection and Tracking](#joint-detection-and-tracking)
  - [Transformer-based Methods](#transformer-based-methods)
  - [基于图神经网络 Graph-based Methods](#基于图神经网络-graph-based-methods)
- [数据集 Datasets](#数据集-datasets)
- [评估指标 Metrics](#评估指标-metrics)
- [排行榜 Benchmarks](#排行榜-benchmarks)
- [引用 Citation](#引用-citation)

---

## 简介 Introduction

本仓库整理了多目标追踪（MOT）领域的重要论文、数据集和评估方法，涵盖从传统方法到基于深度学习、Transformer 的最新进展。

Multi-Object Tracking (MOT) aims to detect and associate multiple objects across video frames. This repo provides a curated list of papers, datasets, and tools for researchers in this field.

---

## 综述论文 Survey Papers

| 年份 | 标题 | 来源 | 链接 |
|------|------|------|------|
| 2023 | Multiple Object Tracking: A Literature Review | TPAMI | [Paper](https://arxiv.org/abs/xxxx) |
| 2022 | ... | ... | ... |

---

## 方法分类 Methods

### 检测器 Detectors

> 用于初步目标检测的方法

| 年份 | 方法 | 会议/期刊 | 链接 |
|------|------|-----------|------|
| 2023 | YOLO-X | CVPR | [Paper](链接) \| [Code](链接) |
| 2022 | ... | ... | ... |

---

### Re-ID 模块

> 外观特征提取，用于跨帧目标匹配

| 年份 | 方法 | 会议/期刊 | 链接 |
|------|------|-----------|------|
| 2023 | ... | ... | ... |

---

### Tracking-by-Detection

> 先检测后关联的经典两阶段方法

| 年份 | 方法 | 会议/期刊 | 亮点 | 链接 |
|------|------|-----------|------|------|
| 2016 | SORT | ICIP | 卡尔曼 + 匈牙利算法 | [Paper](链接) \| [Code](链接) |
| 2017 | Deep SORT | ICIP | 加入外观特征 | [Paper](链接) \| [Code](链接) |
| 2022 | ByteTrack | ECCV | 低置信度检测框利用 | [Paper](链接) \| [Code](链接) |

---

### Joint Detection and Tracking

> 端到端检测与追踪联合训练

| 年份 | 方法 | 会议/期刊 | 亮点 | 链接 |
|------|------|-----------|------|------|
| 2020 | FairMOT | IJCV | 平衡检测与 ReID | [Paper](链接) \| [Code](链接) |
| 2021 | ... | ... | ... | ... |

---

### Transformer-based Methods

> 基于注意力机制的追踪方法

| 年份 | 方法 | 会议/期刊 | 亮点 | 链接 |
|------|------|-----------|------|------|
| 2021 | TrackFormer | CVPR | 查询追踪 | [Paper](链接) \| [Code](链接) |
| 2022 | MOTR | ECCV | 端到端 Transformer MOT | [Paper](链接) \| [Code](链接) |
| 2023 | ... | ... | ... | ... |

---

### 基于图神经网络 Graph-based Methods

| 年份 | 方法 | 会议/期刊 | 亮点 | 链接 |
|------|------|-----------|------|------|
| 2020 | MPNTrack | CVPR | 消息传递网络 | [Paper](链接) \| [Code](链接) |

---

## 数据集 Datasets

| 数据集 | 年份 | 场景 | 目标类型 | 链接 |
|--------|------|------|----------|------|
| MOT15 | 2015 | 行人 | 室内/室外 | [官网](链接) |
| MOT16 | 2016 | 行人 | 街道 | [官网](链接) |
| MOT17 | 2017 | 行人 | 多视角 | [官网](链接) |
| MOT20 | 2020 | 行人 | 拥挤场景 | [官网](链接) |
| DanceTrack | 2022 | 舞蹈人群 | 外观相似目标 | [官网](链接) |
| BDD100K | 2020 | 自动驾驶 | 多类目标 | [官网](链接) |

---

## 评估指标 Metrics

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

## 排行榜 Benchmarks

### MOT17 (Private Detector)

| 排名 | 方法 | HOTA | MOTA | IDF1 | FPS |
|------|------|------|------|------|-----|
| 1 | ... | ... | ... | ... | ... |
| 2 | ... | ... | ... | ... | ... |

> 数据来源：[MOTChallenge](https://motchallenge.net/)

---

## 引用 Citation






## 贡献 Contributing

欢迎提交 PR 或 Issue 来补充论文、修正错误！  
Feel free to open a PR or Issue to add papers or fix errors!

---

