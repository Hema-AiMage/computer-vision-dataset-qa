# Computer Vision Dataset QA

Practical quality-assurance guidelines, review workflows, and operational checklists for **image annotation, video object tracking, segmentation, and production computer vision datasets**.

This repository documents QA practices developed from hands-on work with real-world computer vision data.

The goal is not simply to determine whether an annotation exists, but whether the resulting ground truth is **accurate, consistent, complete, and usable for model development**.

## QA Guides

### [Bounding Box Annotation QA](docs/bounding-box-qa.md)
Review methodology for object coverage, box placement, class accuracy, duplicates, occlusion, truncation, difficult objects, and cross-batch consistency.

### [Video Object Tracking QA](docs/video-tracking-qa.md)
Frame-to-frame QA for Track ID consistency, object exit/re-entry, occlusion, interpolation, identity switches, missing frames, and difficult video conditions.

### [Segmentation Annotation QA](docs/segmentation-qa.md)
Review methodology for mask and polygon accuracy, boundary consistency, instance separation, occlusion, overlapping objects, and difficult edges.

### [Dataset Acceptance Checklist](docs/dataset-acceptance-checklist.md)
A final delivery gate covering dataset scope, annotation completeness, guideline compliance, class coverage, difficult samples, export integrity, data splits, and re-review.

## Operational Review Checklists

These shorter checklists are designed to be used directly during annotation QA.

### [Image Annotation Review Checklist](checklists/image-annotation-review.md)
A practical reviewer checklist for bounding boxes, segmentation, object coverage, class accuracy, false positives, and cross-sample consistency.

### [Video Tracking Review Checklist](checklists/video-tracking-review.md)
A sequence-level reviewer checklist for Track IDs, frame-to-frame accuracy, occlusion, interpolation, missing frames, identity switches, and temporal consistency.

## Why Dataset QA Matters

Annotation errors are not limited to incorrect class labels.

Real-world computer vision datasets can contain:

- Missing objects
- Inconsistent bounding boxes
- Incorrect or changing class labels
- Track-ID switches
- Lost identities after occlusion
- Incorrect handling of objects leaving and re-entering a scene
- Segmentation boundary errors
- Unreviewed interpolation
- Small or low-contrast objects being missed
- Inconsistent annotation rules across annotators or batches

These errors can propagate directly into training and evaluation data.

## QA Approach

A useful QA workflow evaluates annotations at multiple levels:

**Annotation → Object/Track → Image/Sequence → Batch → Dataset → Export**

Review should consider both individual annotation accuracy and systematic inconsistencies across the dataset.

Particular attention should be given to difficult cases such as:

- Occlusion
- Partial visibility
- Low contrast
- Thermal imagery
- Crowded scenes
- Fast motion
- Camera vibration
- Small or distant objects
- Ambiguous boundaries

## Tools & Data Formats

Experience includes workflows involving:

**Annotation platforms:** CVAT, Label Studio, LabelImg, Roboflow, Labelbox, SuperAnnotate

**Data formats:** COCO JSON, CVAT XML, YOLO TXT, and project-specific structured annotation exports

**Tasks:** Object Detection · Video Tracking · Semantic Segmentation · Instance Segmentation · Classification · Dataset QA

## About

Maintained by **Hema Sekhar**, Computer Vision Dataset Engineer and Founder of **Aimage Annotators**.

Aimage Annotators works with image, video, tracking, segmentation, and dataset QA workflows for computer vision and robotics applications.

**Website:** https://www.aimageannotators.com  
**LinkedIn:** https://www.linkedin.com/in/hemasekhar-ai-annotation-expert
