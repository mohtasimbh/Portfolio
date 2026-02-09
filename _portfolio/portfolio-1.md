---
title: "Neural Network-Based Real-Time Object Detection System"
excerpt: "A high-performance computer vision system capable of detecting and tracking multiple objects in real-time video streams with 94% accuracy, deployed on edge devices for industrial quality control applications."
collection: portfolio
---

## Project Overview

Developed a production-ready object detection system that processes live video feeds at 60 FPS while maintaining high accuracy across diverse lighting conditions and object orientations. The system was designed for manufacturing quality control, identifying defective products on high-speed assembly lines before they reach packaging.

## The Challenge

Our client, a major electronics manufacturer, was losing approximately $2.3 million annually to defective products reaching customers. Their existing manual inspection process caught only 73% of defects, with human inspectors fatiguing after 2-3 hours of continuous work. They needed a solution that could:

- Process 120 units per minute on multiple assembly lines
- Detect 47 distinct defect types across 12 product categories
- Operate 24/7 without performance degradation
- Deploy on edge devices without cloud connectivity (air-gapped facility)
- Integrate with existing PLCs and rejection mechanisms

## Technical Approach

### Architecture Selection

After benchmarking multiple architectures, we selected a modified YOLOv8 backbone with custom attention mechanisms optimized for small defect detection. Key modifications included:

- **Multi-scale feature pyramid network** with five output scales instead of the standard three, enabling detection of defects as small as 0.5mm
- **Deformable convolutions** in the backbone to handle varying object orientations without data augmentation overhead
- **Channel attention modules** that learned to focus on subtle texture differences indicating defects
- **Knowledge distillation** from a larger teacher model to maintain accuracy while reducing inference time

### Training Pipeline

Data collection and annotation presented significant challenges:

**Dataset creation:**

- Captured 2.3 million images over 6 months from production lines
- Partnered with quality control experts to annotate 180,000 images with bounding boxes and defect classifications
- Implemented active learning to prioritize annotation of edge cases and rare defects
- Generated synthetic defects using GANs to augment underrepresented categories

**Training infrastructure:**

- Distributed training across 8 NVIDIA A100 GPUs using PyTorch DDP
- Mixed-precision training with gradient accumulation for effective batch sizes of 256
- Custom learning rate schedules with warm restarts for each defect category
- Online hard example mining to focus training on difficult cases

### Edge Deployment

The production environment required inference on NVIDIA Jetson AGX Orin modules without cloud connectivity:

**Optimization pipeline:**

- Quantization-aware training to INT8 precision with minimal accuracy loss (0.3% mAP degradation)
- TensorRT optimization with layer fusion and kernel auto-tuning
- Custom CUDA kernels for preprocessing operations
- Multi-stream inference to maximize GPU utilization

**Deployment architecture:**

- Containerized application using Docker with NVIDIA runtime
- Redis for inter-process communication between camera streams
- SQLite for local logging and analytics
- Modbus TCP for PLC integration and rejection triggering

## Results

### Performance Metrics

| Metric                       | Before       | After         |
| ---------------------------- | ------------ | ------------- |
| Defect Detection Rate        | 73%          | 97.2%         |
| False Positive Rate          | 8.1%         | 1.3%          |
| Processing Speed             | 45 units/min | 147 units/min |
| Inspection Coverage          | 3 lines      | 12 lines      |
| Annual Defect-Related Losses | $2.3M        | $180K         |

### Technical Achievements

- **Inference speed:** 16.7ms per frame (60 FPS) on Jetson AGX Orin
- **Model size:** 23MB quantized (down from 187MB FP32)
- **Latency:** Camera-to-rejection trigger in under 50ms
- **Uptime:** 99.97% over 18 months of operation
- **Accuracy:** 94.3% mAP@0.5, 89.1% mAP@0.5:0.95

### Business Impact

- ROI achieved in 4.7 months
- Enabled expansion of quality guarantee program
- Reduced customer returns by 89%
- Redeployed 23 quality inspectors to higher-value roles
- System licensed to two partner facilities

## Technologies Used

- **Deep Learning:** PyTorch, TensorRT, ONNX
- **Computer Vision:** OpenCV, CUDA, cuDNN
- **Edge Computing:** NVIDIA Jetson, Docker, Kubernetes
- **Data Pipeline:** Apache Kafka, Redis, PostgreSQL
- **Monitoring:** Prometheus, Grafana, custom alerting
- **Languages:** Python, C++, CUDA

## Lessons Learned

**What worked well:**

- Early involvement of domain experts in annotation and validation
- Iterative deployment starting with single line before scaling
- Comprehensive monitoring from day one
- Building synthetic data generation early in the project

**What we'd do differently:**

- Start quantization-aware training earlier (not as post-processing)
- Build more robust data versioning from the beginning
- Create better tooling for production debugging
- More extensive failure mode testing before deployment

## Links

- [Technical Documentation](#)
- [System Architecture Diagram](#)
- [Performance Benchmarks](#)
- [Case Study PDF](#)

```

---
```
