# Image Annotation Review Checklist

A practical checklist for reviewing image annotation batches before acceptance.

Use this alongside the project's approved annotation guidelines.

## Before Review

- [ ] Confirm the correct dataset/batch is open
- [ ] Confirm the current annotation guideline version
- [ ] Confirm required classes
- [ ] Confirm inclusion/exclusion rules
- [ ] Confirm occlusion and truncation rules
- [ ] Confirm any minimum object-size requirements

## Object Coverage

- [ ] Scan the complete image, not only existing annotations
- [ ] Check for missing required objects
- [ ] Check small and distant objects
- [ ] Check partially visible objects
- [ ] Check image boundaries
- [ ] Check dark, low-contrast, or difficult regions
- [ ] Check crowded or overlapping areas

## Bounding Boxes

- [ ] Box placement follows project rules
- [ ] Required visible object regions are covered
- [ ] Excessive background is avoided
- [ ] No unintended duplicate boxes exist
- [ ] Truncated objects follow project rules
- [ ] Occluded objects follow project rules

## Classes

- [ ] Each annotation has the correct class
- [ ] Similar classes are not confused
- [ ] Class names/IDs follow the approved schema
- [ ] Ambiguous cases follow documented decisions

## Segmentation / Polygons

Where applicable:

- [ ] Boundaries follow required precision
- [ ] Background is not unnecessarily included
- [ ] Required object regions are not excluded
- [ ] Separate instances remain separate
- [ ] Polygon geometry is valid
- [ ] Small or thin regions follow project rules

## False-Positive Check

- [ ] No background structures are incorrectly annotated
- [ ] Reflections or shadows are not mislabeled
- [ ] Excluded categories are not annotated
- [ ] No obsolete or accidental annotations remain

## Consistency Check

Compare with other reviewed samples:

- [ ] Box placement style is consistent
- [ ] Boundary precision is consistent
- [ ] Class interpretation is consistent
- [ ] Occlusion handling is consistent
- [ ] Truncation handling is consistent
- [ ] Difficult cases follow the same decisions

## Before Accepting the Image

- [ ] All required objects have been considered
- [ ] No obvious missing annotations remain
- [ ] No obvious false-positive annotations remain
- [ ] Annotation geometry is acceptable
- [ ] Classes are correct
- [ ] Project-specific rules are satisfied

## Reviewer Note

When an error appears systematic rather than isolated, check other annotations from the same batch for the same issue before accepting the batch.

**Review the image, not just the labels already present.**
