# Video Object Tracking QA Guide

Quality assurance for video object tracking requires more than checking whether a bounding box is correctly placed in an individual frame.

A track can contain visually accurate boxes and still be incorrect if the object's identity changes, annotations disappear unexpectedly, interpolation introduces errors, or the same object receives inconsistent Track IDs.

This guide outlines practical checks for reviewing tracked video datasets.

## 1. Track-ID Consistency

Each tracked object should maintain the same Track ID for as long as it remains continuously present in the scene.

Review for:

- Track-ID switches between nearby or overlapping objects
- A single object receiving multiple IDs without leaving the scene
- Two different objects incorrectly sharing one Track ID
- Track IDs changing after temporary occlusion
- Incorrect identity assignment in crowded scenes

### Example

If `Car-17` passes behind another vehicle for several frames but remains part of the same continuous trajectory, its identity should normally remain `Car-17` when it becomes visible again.

Temporary occlusion should not automatically create a new identity.

---

## 2. Object Exit and Re-entry

A clear distinction should be made between **occlusion** and **complete exit from the frame**.

If project guidelines specify that an object receives a new Track ID after completely leaving the frame, reviewers should verify that this rule is applied consistently.

### Review questions

- Did the object actually leave the image boundary completely?
- Was it merely hidden behind another object?
- Was a new ID created too early?
- Was an old ID incorrectly reused after a complete exit and later re-entry?

The exact rule should always follow the project's approved annotation guidelines.

---

## 3. Frame-by-Frame Bounding Box Accuracy

Interpolation can accelerate video annotation, but interpolated boxes should not be assumed to be correct.

Between keyframes, objects may:

- Change direction
- Change apparent size
- Become partially occluded
- Move rapidly
- Enter or leave the frame
- Change pose or orientation

For high-accuracy datasets, interpolated sequences should be reviewed and adjusted wherever the generated box no longer accurately represents the object.

### Check for

- Boxes drifting away from the object
- Excessive background inside the box
- Parts of the object being cut off
- Delayed box movement during fast motion
- Incorrect box size during perspective changes

---

## 4. Occlusion and Overlap

Crowded scenes are particularly vulnerable to tracking errors.

When objects overlap, reviewers should verify that:

- Identities are not swapped
- Boxes continue to correspond to the correct objects
- Temporary occlusion does not unnecessarily terminate a track
- Reappearing objects are matched according to the project's identity rules

Tracking should be evaluated across the sequence, not from isolated frames.

---

## 5. Small and Low-Contrast Objects

Small objects can be easy to miss, especially in:

- Thermal imagery
- Night scenes
- Low-contrast environments
- Distant road scenes
- Industrial or security footage
- Compressed video

Reviewers should examine the full frame rather than focusing only on existing annotations.

A QA process that checks only annotated objects can confirm box quality while completely missing **false negatives**.

---

## 6. Camera Motion and Vibration

Camera vibration, panning, or sudden movement can create apparent object motion that affects interpolated annotations.

Review for:

- Bounding-box drift
- Boxes lagging behind objects
- Incorrect interpolation during camera movement
- Tracks being terminated because of temporary blur
- Objects being mistaken for new instances after abrupt camera movement

---

## 7. Class Consistency Across a Track

The class assigned to an object should remain consistent unless the annotation specification explicitly requires otherwise.

Example problems include:

- `car` becoming `truck` midway through a track
- `bicycle` changing to `motorcycle`
- Different annotators assigning different classes to the same tracked object

Class changes should be investigated rather than accepted frame by frame.

---

## 8. Missing Frames and Annotation Gaps

Unexpected gaps inside an otherwise continuous track should be reviewed.

Possible causes include:

- Missed annotations
- Incorrect keyframe placement
- Interpolation failure
- Temporary low visibility
- Annotator oversight

A missing annotation should not automatically be treated as a valid track termination.

---

## 9. Review the Entire Track

Video QA should include both:

**Frame-level review** — Is the annotation correct in this frame?

and

**Track-level review** — Is the object's identity and annotation behavior correct across time?

A frame can pass QA while the overall track still fails.

---

## 10. Final Video Acceptance Checklist

Before accepting a tracked video, verify:

- [ ] Required objects are annotated
- [ ] Track IDs remain consistent
- [ ] No unexplained ID switches occur
- [ ] Occlusions are handled according to project rules
- [ ] Exit and re-entry rules are followed
- [ ] Bounding boxes remain accurate across frames
- [ ] Interpolated frames have been reviewed
- [ ] Small and low-contrast objects have been checked
- [ ] Classes remain consistent throughout tracks
- [ ] No unexplained annotation gaps remain
- [ ] Crowded and overlapping scenes have received additional review
- [ ] Final exports follow the required schema and project specification

---

## Core Principle

**Do not review video annotations as a collection of independent images.**

Video tracking ground truth contains a temporal dimension. Position, identity, continuity, visibility, and class consistency must all be evaluated across time.

A high-quality tracking dataset therefore requires QA at three levels:

**Object → Frame → Track**

and finally at the **video/dataset level**.
