# Bounding Box Annotation QA Guide

Bounding-box quality is not determined only by whether an object has a box.

A production-ready object-detection dataset also requires consistent box placement, correct classes, complete object coverage, and uniform interpretation of the annotation guidelines across images, annotators, and batches.

This guide outlines practical checks for reviewing bounding-box annotations.

## 1. Object Coverage

The first QA question should be:

**Are all required objects annotated?**

Reviewers should scan the complete image rather than checking only existing boxes.

Look for:

- Missing objects
- Small or distant objects
- Partially visible objects
- Low-contrast objects
- Objects near image boundaries
- Objects in shadows or dark regions
- Objects partially hidden behind other objects

Checking only existing annotations can verify box quality while completely missing false negatives.

---

## 2. Bounding Box Tightness

Bounding boxes should follow the project's approved placement rules consistently.

Common problems include:

- Excessive background inside the box
- Parts of the object falling outside the box
- Boxes that are unnecessarily large
- Boxes that are too tight and cut off visible object pixels
- Inconsistent margins between annotators

The goal is not simply to create the smallest possible rectangle. The correct placement depends on the project's annotation specification.

---

## 3. Class Accuracy

Every bounding box should have the correct class.

Review for:

- Incorrect class assignments
- Similar classes being confused
- Class names used inconsistently
- Objects changing class between related images or frames
- Deprecated or unauthorized labels
- Annotators interpreting ambiguous classes differently

When class boundaries are unclear, the annotation guideline should define the decision rather than individual annotator preference.

---

## 4. Duplicate Annotations

A single object should not accidentally receive multiple overlapping annotations unless the project explicitly requires multiple labels.

Check for:

- Duplicate boxes
- Nearly identical overlapping boxes
- Old annotations left behind after correction
- Multiple annotators labeling the same object during merged workflows

Duplicates can distort object counts and ground-truth statistics.

---

## 5. Occluded Objects

Occlusion rules should be applied consistently.

Reviewers should verify:

- Whether partially occluded objects should be annotated
- How much visibility is required
- Whether the box represents the visible region or estimated full object
- Whether similar occlusions are treated consistently across the dataset

There is no universal rule for every dataset. The project's approved annotation specification should determine the correct behavior.

---

## 6. Truncated Objects

Objects cut by the image boundary require consistent treatment.

Check:

- Whether truncated objects should be labeled
- Whether the box stops at the image boundary
- Whether class assignment remains valid with partial visibility
- Whether similar boundary cases are handled consistently

Truncation and occlusion should not automatically be treated as the same condition.

---

## 7. Small and Difficult Objects

Small objects often produce a disproportionate number of annotation errors.

Pay additional attention to:

- Distant objects
- Thermal or low-contrast targets
- Motion blur
- Dark scenes
- Dense crowds
- Small objects near larger objects
- Partially visible targets

Where minimum-size rules exist, reviewers should apply them consistently rather than making image-by-image assumptions.

---

## 8. Box Consistency Across the Dataset

Even individually acceptable boxes can create poor ground truth if different annotators use different placement styles.

Review for systematic differences such as:

- One annotator using loose boxes while another uses tight boxes
- Different interpretations of occluded objects
- Different minimum-size thresholds
- Inconsistent class decisions
- Different treatment of image-boundary objects

QA should therefore examine both individual annotations and **cross-batch consistency**.

---

## 9. False Positives

Not every annotation corresponds to a valid target.

Check for boxes placed around:

- Background structures
- Reflections
- Shadows
- Object-like patterns
- Incorrect classes
- Objects excluded by the project guidelines

False-positive annotations can be as damaging to ground truth as missed objects.

---

## 10. Edge Cases

Ambiguous examples should not be resolved independently by every annotator.

A good workflow should:

1. Identify the ambiguous case
2. Compare it with the approved guidelines
3. Escalate unresolved cases
4. Document the decision
5. Apply the decision consistently to similar examples

This turns individual judgment calls into repeatable dataset rules.

---

## 11. Final Image Acceptance Checklist

Before accepting an annotated image, verify:

- [ ] All required objects have been considered
- [ ] No obvious required objects are missing
- [ ] Bounding boxes follow the approved placement rules
- [ ] Boxes do not unnecessarily include background
- [ ] Visible object regions are not incorrectly cut off
- [ ] Classes are correct and consistent
- [ ] No unintended duplicate annotations exist
- [ ] Occluded objects follow project rules
- [ ] Truncated objects follow project rules
- [ ] Small and difficult objects have been reviewed
- [ ] No obvious false-positive annotations remain
- [ ] Edge cases follow documented decisions

---

## 12. Dataset-Level Review

Image-level QA alone is not enough.

A reviewer should also examine samples across annotators, batches, locations, capture conditions, and classes to identify systematic inconsistencies.

A useful hierarchy is:

**Object → Image → Batch → Dataset**

An annotation can be technically acceptable in isolation while still being inconsistent with the rest of the dataset.

---

## Core Principle

**Consistency is part of accuracy.**

A dataset containing individually reasonable annotations can still produce unreliable ground truth when annotation rules are interpreted differently across thousands of images.

Bounding-box QA should therefore evaluate both **annotation correctness** and **dataset-wide consistency**.
