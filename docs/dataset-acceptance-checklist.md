# Computer Vision Dataset Acceptance Checklist

A labeled dataset should not be accepted for model development simply because annotation work is marked complete.

Before delivery or ingestion into a training pipeline, the dataset should pass a final review covering annotation quality, completeness, consistency, structure, and export integrity.

This checklist provides a practical final acceptance gate for computer vision datasets.

## 1. Dataset Scope

Confirm that the delivered dataset matches the agreed project scope.

- [ ] Expected images, videos, or frames are present
- [ ] Required annotation tasks are complete
- [ ] Required classes are included
- [ ] Dataset batches are accounted for
- [ ] Known exclusions are documented
- [ ] No unintended source data is included

A dataset should not move to final acceptance when the delivered scope cannot be reconciled with the expected scope.

---

## 2. Annotation Guideline Compliance

Verify that annotations follow the approved project specification.

- [ ] Class definitions are applied correctly
- [ ] Inclusion and exclusion rules are followed
- [ ] Occlusion rules are applied consistently
- [ ] Truncation rules are followed
- [ ] Minimum object-size rules are respected where defined
- [ ] Difficult or ambiguous cases follow documented decisions
- [ ] Project-specific exceptions are handled consistently

The acceptance review should use the project's approved guidelines as the reference rather than reviewer preference.

---

## 3. Annotation Completeness

Check whether required ground truth is actually present.

Review for:

- Missing objects
- Missing masks or polygons
- Missing frames
- Unexplained gaps in tracks
- Incomplete annotation batches
- Unlabeled required classes

A technically accurate annotation is not sufficient if significant required ground truth is missing.

---

## 4. Annotation Accuracy

Review representative samples for annotation correctness.

### Bounding boxes

- [ ] Box placement follows project rules
- [ ] Required objects are not cut off incorrectly
- [ ] Excessive background is avoided
- [ ] Classes are correct
- [ ] Duplicate boxes are absent

### Segmentation

- [ ] Boundaries meet required precision
- [ ] Masks do not unnecessarily include background
- [ ] Required object regions are not missing
- [ ] Separate instances remain separate where required
- [ ] Polygon geometry is valid

### Video tracking

- [ ] Track IDs remain consistent
- [ ] Identity switches are not present
- [ ] Occlusion is handled correctly
- [ ] Exit/re-entry follows project rules
- [ ] Interpolated annotations have been reviewed
- [ ] Unexpected annotation gaps are resolved

---

## 5. False-Negative Review

Do not evaluate only existing annotations.

Reviewers should actively search for required objects or regions that were never annotated.

Pay particular attention to:

- Small objects
- Distant objects
- Low-contrast targets
- Thermal imagery
- Crowded scenes
- Partial visibility
- Image boundaries
- Motion blur
- Dark regions
- Overlapping objects

Missing ground truth can remain invisible if QA only inspects existing labels.

---

## 6. False-Positive Review

Check for annotations that should not exist.

Examples include:

- Background regions labeled as objects
- Reflections
- Shadows
- Duplicate annotations
- Excluded object categories
- Incorrectly interpreted structures
- Invalid masks or boxes

Both false negatives and false positives should be considered during acceptance.

---

## 7. Cross-Batch Consistency

Compare annotations across different batches and annotators.

Check for systematic differences in:

- Bounding-box placement
- Segmentation boundary precision
- Class interpretation
- Occlusion handling
- Truncation handling
- Minimum-size decisions
- Track-ID behavior
- Difficult-case interpretation

A dataset can contain individually reasonable annotations and still fail because different batches follow different conventions.

---

## 8. Class Coverage

Confirm that the expected class distribution has been reviewed.

Questions to ask:

- Are all expected classes represented?
- Are rare classes present where expected?
- Are any classes unexpectedly absent?
- Are similar classes frequently confused?
- Are class counts significantly different from expectations?

Class imbalance is not automatically an annotation error, but unexpected distributions should be investigated before acceptance.

---

## 9. Difficult-Sample Review

High-risk samples should receive additional attention.

Examples include:

- Heavy occlusion
- Dense scenes
- Small targets
- Fast motion
- Low light
- Thermal or low-contrast imagery
- Camera vibration
- Motion blur
- Unusual viewpoints
- Rare classes
- Ambiguous boundaries

Random sampling alone may underrepresent the cases most likely to contain annotation errors.

---

## 10. File and Export Integrity

Annotation quality is only useful if the exported data is structurally valid.

Verify:

- [ ] Required annotation files exist
- [ ] File names map correctly to source data
- [ ] Image/frame references are valid
- [ ] Class IDs and names match the expected schema
- [ ] Track IDs are represented correctly
- [ ] Coordinates use the expected format
- [ ] No required files are empty or corrupted
- [ ] Export format matches project requirements
- [ ] Dataset can be parsed by the intended downstream workflow

Examples may include COCO JSON, YOLO TXT, CVAT XML, or project-specific schemas.

---

## 11. Data Split Integrity

If train, validation, or test splits are part of the delivery, verify that they follow the project design.

Check for:

- Duplicate samples across splits
- Related frames leaking across intended independent splits
- Unexpected class absence from a split
- Incorrect file-to-annotation mappings

The appropriate split strategy depends on the project and should be defined before acceptance.

---

## 12. Sampling Strategy

A final QA sample should not rely exclusively on easy or random examples.

A stronger acceptance sample may include:

- Random samples
- Samples from every annotator
- Samples from every batch
- Every class where practical
- Difficult environments
- Rare classes
- Known edge cases
- Previously corrected samples

Risk-based sampling can reveal systematic problems that a purely random sample misses.

---

## 13. Corrections and Re-Review

When errors are found:

1. Record the issue
2. Determine whether it is isolated or systematic
3. Correct affected annotations
4. Check similar annotations for the same problem
5. Re-review corrected work
6. Confirm the issue is resolved before acceptance

Finding and fixing one example is not enough when the same annotation decision may have been repeated across a batch.

---

## 14. Final Delivery Gate

Before accepting the dataset, confirm:

- [ ] Scope is complete
- [ ] Annotation guidelines are satisfied
- [ ] Required ground truth is present
- [ ] Annotation accuracy has been reviewed
- [ ] False negatives have been actively checked
- [ ] False positives have been reviewed
- [ ] Cross-batch consistency is acceptable
- [ ] Class coverage has been examined
- [ ] Difficult samples have received additional review
- [ ] Export structure is valid
- [ ] Data splits are correct where applicable
- [ ] Identified errors have been corrected and re-reviewed
- [ ] Final delivery contents match the expected project specification

---

## Acceptance Principle

**Annotation completion and dataset acceptance are not the same thing.**

A dataset should move into model training or evaluation only after its annotations, structure, consistency, and delivery integrity have been checked against the project's requirements.

A useful acceptance hierarchy is:

**Annotation → Sample → Batch → Dataset → Export**

Each level can reveal problems that are invisible at the level below it.
