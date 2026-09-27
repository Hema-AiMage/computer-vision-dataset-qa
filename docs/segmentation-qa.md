# Segmentation Annotation QA Guide

Segmentation quality depends on more than assigning the correct class to an object.

A useful segmentation dataset requires masks or polygons that follow object boundaries consistently, represent the intended regions correctly, and apply the same annotation rules across images, annotators, and batches.

This guide outlines practical checks for reviewing semantic and instance segmentation annotations.

## 1. Boundary Accuracy

The annotation boundary should follow the visible object boundary according to the project's required level of precision.

Review for:

- Masks extending into the background
- Object pixels incorrectly excluded
- Rough boundaries around clearly visible edges
- Polygon points placed too far from the object
- Excessive simplification of curved or irregular shapes
- Unnecessary polygon points that add complexity without improving accuracy

The required precision should be defined by the project rather than assumed by individual annotators.

---

## 2. Over-Segmentation and Under-Segmentation

Two common mask errors are:

**Over-segmentation:** background or neighboring regions are incorrectly included.

**Under-segmentation:** valid portions of the target object are excluded.

Reviewers should inspect the complete object boundary, particularly around:

- Thin structures
- Irregular shapes
- Curved edges
- Object-background transitions
- Low-contrast boundaries

---

## 3. Instance Separation

For instance segmentation, separate object instances should remain separate even when they belong to the same class.

Check for:

- Two neighboring objects merged into one mask
- One object incorrectly split into multiple instances
- Instance identities lost during overlap
- Incorrect separation in crowded scenes

Correct class assignment alone does not guarantee correct instance annotation.

---

## 4. Occlusion

Occluded objects require consistent interpretation.

Review:

- Whether only visible regions should be segmented
- Whether hidden regions should ever be estimated
- Whether partially visible instances remain separate
- Whether similar occlusion cases are handled consistently

The correct approach depends on the approved project specification.

Annotators should not independently invent hidden object boundaries unless the project explicitly requires amodal annotation.

---

## 5. Holes and Internal Regions

Some objects contain legitimate holes or background regions inside their outer boundary.

Review for:

- Background areas incorrectly filled
- Valid holes accidentally removed
- Internal regions incorrectly excluded
- Polygon structures that cannot represent the intended geometry correctly

Whether holes should be represented depends on the annotation format and project requirements.

---

## 6. Small and Thin Regions

Thin structures and small regions are easy to lose during annotation.

Examples may include:

- Cables
- Poles
- Bicycle components
- Narrow object extensions
- Small defects
- Fine structural features

Reviewers should determine whether these regions meet the project's inclusion rules and verify that similar cases are treated consistently.

---

## 7. Overlapping Objects

Overlapping instances can create ambiguous boundaries.

Check that:

- Each visible instance is represented correctly
- Masks do not accidentally absorb neighboring objects
- Instance identities remain separate
- Occluded boundaries follow the approved annotation rules
- Overlap does not create duplicate or conflicting regions

Crowded scenes often require additional review.

---

## 8. Class Consistency

Each mask or polygon should use the correct class.

Review for:

- Incorrect class assignments
- Similar classes being confused
- Different labels used for equivalent objects
- Class changes between related images
- Unauthorized or obsolete class names

Class definitions should be applied consistently across the complete dataset.

---

## 9. Missing and Extra Masks

QA should search for both false negatives and false positives.

### Missing annotations

Look for required objects or regions that have no mask.

### Extra annotations

Look for masks covering:

- Background
- Reflections
- Shadows
- Artifacts
- Excluded object categories
- Regions that do not meet project requirements

Reviewing only existing masks will not reveal missing ground truth.

---

## 10. Polygon Quality

For polygon-based segmentation, review the geometry itself.

Check for:

- Self-intersecting polygons
- Incorrectly ordered points
- Large gaps between polygon edges and object boundaries
- Excessive unnecessary points
- Too few points to represent important shape changes
- Accidental points far outside the object

Polygon complexity should be sufficient to represent the target accurately without introducing unnecessary noise.

---

## 11. Edge Ambiguity

Some boundaries are genuinely difficult to determine because of:

- Motion blur
- Shadows
- Low contrast
- Transparency
- Reflections
- Thermal imagery
- Compression artifacts
- Partial visibility

These cases should be handled through documented annotation rules rather than inconsistent individual judgment.

When necessary:

1. Identify the ambiguous boundary
2. Apply the approved guideline
3. Escalate unresolved cases
4. Document the decision
5. Apply the same decision to similar examples

---

## 12. Cross-Batch Consistency

A dataset can contain individually acceptable masks while still being inconsistent overall.

Compare samples across:

- Annotators
- Reviewers
- Batches
- Classes
- Capture environments
- Lighting conditions
- Data sources

Look for systematic differences in boundary precision, inclusion rules, occlusion treatment, and class interpretation.

---

## 13. Final Segmentation Acceptance Checklist

Before accepting an annotated image, verify:

- [ ] Required objects or regions have been considered
- [ ] No obvious required masks are missing
- [ ] Boundaries follow project requirements
- [ ] Background is not unnecessarily included
- [ ] Valid object regions are not incorrectly excluded
- [ ] Separate instances remain separate where required
- [ ] Occlusions follow the approved rules
- [ ] Holes and internal regions are handled correctly
- [ ] Small and thin structures follow inclusion rules
- [ ] Classes are correct and consistent
- [ ] No unintended extra masks remain
- [ ] Polygon geometry is valid
- [ ] Ambiguous boundaries follow documented decisions

---

## 14. Dataset-Level Review

Segmentation QA should not stop at individual masks.

A useful review hierarchy is:

**Region → Object/Instance → Image → Batch → Dataset**

This helps identify systematic differences that may not be obvious when reviewing annotations one at a time.

---

## Core Principle

**Boundary consistency is part of ground-truth quality.**

A segmentation dataset can contain the correct objects and classes while still introducing noise through inconsistent boundaries, instance separation, occlusion handling, or annotation precision.

High-quality segmentation QA therefore evaluates both **local mask accuracy** and **dataset-wide consistency**.
