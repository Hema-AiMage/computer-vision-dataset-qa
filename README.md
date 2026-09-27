# Computer Vision Dataset QA

Practical quality-assurance guidelines for image, video, object tracking, and segmentation datasets used in computer vision.

This repository documents QA principles and review workflows developed from hands-on experience working with production computer vision datasets.

The focus is not simply whether an annotation exists, but whether the resulting ground truth is **accurate, consistent, complete, and usable for model development**.

## Why Dataset QA Matters

Annotation errors are not limited to incorrect class labels.

In real-world computer vision datasets, quality problems can include:

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

## QA Areas Covered

### Image Annotation
Bounding-box placement, class consistency, missed objects, duplicates, truncation, occlusion, and difficult edge cases.

### Video Object Tracking
Track-ID consistency, frame-by-frame box adjustment, occlusion handling, object re-entry, interpolation review, and identity switches.

### Segmentation
Mask accuracy, boundary consistency, overlapping objects, small regions, and class-level consistency.

### Dataset-Level QA
Cross-batch consistency, annotation guideline compliance, class coverage, sample validation, export checks, and final acceptance review.

## Repository Structure

- `docs/bounding-box-qa.md`
- `docs/video-tracking-qa.md`
- `docs/segmentation-qa.md`
- `docs/dataset-acceptance-checklist.md`
- `checklists/image-annotation-review.md`
- `checklists/video-tracking-review.md`

## Approach

A reliable QA workflow should evaluate annotations at three levels:

**Object level → Frame/Image level → Dataset level**

Passing one level does not guarantee that the dataset is production-ready.

For video datasets in particular, temporal consistency matters: an annotation may look correct in an individual frame while still being wrong when evaluated as part of an object track.

## About

Maintained by **Hema Sekhar**, Computer Vision Dataset Engineer and Founder of **Aimage Annotators**.

Aimage Annotators works with image, video, tracking, segmentation, and dataset QA workflows for computer vision and robotics applications.
