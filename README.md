# AABO: Adaptive Anchor Box Optimization for Object Detection via Bayesian Sub-sampling

# Introduction

Code for ECCV 2020 paper: AABO: Adaptive Anchor Box Optimization for Object Detection via Bayesian Sub-sampling ([paper](https://arxiv.org/abs/2007.09336)).

In AABO, we propose an adaptive anchor box optimization method for object detection via Bayesian sub-sampling, where optimal anchor configurations for a certain dataset and detector are determined automatically without manually adjustment.

Experiments demonstrate the effectiveness of AABO on different detectors and datasets, e.g. achieving around 2.4% mAP improvement on COCO, and the optimal anchors can bring 1.4% to 2.4% mAP improvement on SOTA detectors by only optimizing anchor configurations, e.g. boost Mask RCNN from 40.3% to 42.3%, and boost HTC detector from 46.8% to 48.2%.

# Implementation

The implementation is based on the open source detection toolbox [MMDetection](https://github.com/open-mmlab/mmdetection). 

- Please replace the original files in MMDetection with our new files: 

  - ` AABO/__init__.py` ---> `mmdetection/mmdet/models/anchor_heads/__init__.py`  
  - `AABO/anchor_generator.py` --->`mmdetection/mmdet/core/anchor/anchor_generator.py`
  - `AABO/anchor_head.py`--->`mmdetection/mmdet/models/anchor_heads/anchor_head.py` 

- Please add these files to the corresponding directories:

  - Add `AABO/aabo_rpn_head.py` to `mmdetection/mmdet/models/anchor_heads/`

  - Add `AABO/aabo_mask_rcnn_r101_fpn_2x.py ` to `mmdetection/configs/`

  - Add `AABO/aabo_htc_dcov_x101_64x4d_fpn_24e.py` to `mmdetection/configs/`

    

Note there are two example configuration files: `aabo_mask_rcnn_r101_fpn_2x.py` and `aabo_htc_dcov_x101_64x4d_fpn_24e.py`. Using these two configuration files, the optimized anchor settings searched by AABO could boost the performance of Mask RCNN and HTC. 

If you would like to test the performance of these optimized anchor settings on other detectors,  just replace the default anchors with the optimized anchors recorded in these two files. In our paper, we have conducted experiments on different advanced anchor-based detectors and observed consistent performance improvements.

We have tested the code with Pytorch 1.1 and [MMdetection v1.0rc1](https://github.com/open-mmlab/mmdetection/tree/v1.0rc1).

