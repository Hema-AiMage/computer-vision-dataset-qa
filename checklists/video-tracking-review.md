# Video Object Tracking Review Checklist

A practical checklist for reviewing video object-tracking annotations before acceptance.

Use this alongside the project's approved tracking and annotation guidelines.

## Before Review

- [ ] Confirm the correct video and annotation range
- [ ] Confirm required object classes
- [ ] Confirm Track ID rules
- [ ] Confirm object exit/re-entry rules
- [ ] Confirm occlusion rules
- [ ] Confirm interpolation/keyframe policy
- [ ] Confirm any minimum object-size or visibility requirements

## Object Coverage

- [ ] Scan the complete frame, not only existing tracks
- [ ] Check for missing objects
- [ ] Check small and distant objects
- [ ] Check partially visible objects
- [ ] Check low-contrast or dark regions
- [ ] Check crowded and overlapping scenes
- [ ] Check objects entering or leaving the frame

## Track ID Consistency

For each tracked object:

- [ ] Track ID remains consistent while the object is continuously present
- [ ] No unintended Track ID changes occur
- [ ] Different objects do not accidentally share the same Track ID
- [ ] Reappearing objects follow the project's exit/re-entry rule
- [ ] Track IDs remain associated with the correct class
- [ ] Identity switches are absent

## Frame-to-Frame Box Accuracy

- [ ] Bounding boxes follow the object through every reviewed frame
- [ ] Box placement follows project rules
- [ ] Boxes do not drift away from the object
- [ ] Visible object regions are not incorrectly cut off
- [ ] Excessive background is avoided
- [ ] Sudden box-size changes are justified by the scene
- [ ] Fast motion and motion blur are reviewed carefully

## Occlusion and Overlap

- [ ] Track identity is preserved through allowed occlusions
- [ ] Overlapping objects retain separate identities
- [ ] Track IDs do not swap after objects cross
- [ ] Temporary disappearance follows project rules
- [ ] Reappearance is handled consistently

## Interpolation and Keyframes

Where interpolation is used:

- [ ] Interpolated frames have been visually reviewed
- [ ] Boxes remain aligned between keyframes
- [ ] Object motion does not cause interpolation drift
- [ ] Entry and exit frames are correctly positioned
- [ ] Occlusion transitions are checked manually
- [ ] Sudden motion or camera movement has not created incorrect boxes

Interpolation should assist annotation, not replace frame-level QA.

## Missing Frames and Annotation Gaps

- [ ] No unexplained gaps exist within active tracks
- [ ] Skipped frames are intentional and permitted
- [ ] Objects remain annotated throughout the required visibility period
- [ ] Track start frame is correct
- [ ] Track end frame is correct

## Class Consistency

- [ ] Object class remains correct throughout the track
- [ ] Similar classes are not confused
- [ ] Class changes occur only when explicitly allowed
- [ ] Class IDs/names follow the approved schema

## Difficult Conditions

Review carefully when the video contains:

- [ ] Low light
- [ ] Thermal or low-contrast imagery
- [ ] Fast-moving objects
- [ ] Camera vibration or camera motion
- [ ] Motion blur
- [ ] Crowded scenes
- [ ] Heavy occlusion
- [ ] Small or distant targets
- [ ] Weather or visibility limitations

## False-Positive Check

- [ ] No background structure is tracked as a valid object
- [ ] Reflections or shadows are not incorrectly tracked
- [ ] Duplicate tracks do not exist for the same object
- [ ] Excluded object categories are not tracked

## Sequence-Level Consistency

Do not review frames only as independent images.

- [ ] Object identity makes sense across the complete sequence
- [ ] Track behavior is temporally consistent
- [ ] Annotation style remains consistent throughout the video
- [ ] Difficult cases follow the same decisions across frames
- [ ] Corrections do not introduce new inconsistencies later in the track

## Before Accepting the Video

- [ ] Required objects have been considered throughout the sequence
- [ ] No obvious missing tracks remain
- [ ] No obvious false-positive tracks remain
- [ ] Track IDs are consistent
- [ ] No identity switches remain
- [ ] Frame-to-frame box placement is acceptable
- [ ] Occlusions and overlaps follow project rules
- [ ] Interpolated frames have been reviewed where applicable
- [ ] Track start and end frames are correct
- [ ] Classes are correct
- [ ] Project-specific requirements are satisfied

## Reviewer Note

When an error is found in a track, review the **entire affected track**, not only the frame where the error was first noticed.

When the same error appears across multiple tracks, check whether it is a systematic batch-level issue before accepting the video.

**For tracking datasets, temporal consistency is part of annotation accuracy.**
