# Street Traffic Object Detection: Annotation Project

A small, fully documented bounding-box annotation project built with CVAT. It covers the whole workflow of a data annotator: writing guidelines, labeling, reviewing, and reporting quality.

## Overview

| | |
|---|---|
| **Task** | Object detection (bounding boxes) |
| **Tool** | CVAT |
| **Images annotated** | 40 |
| **Objects labeled** | 377 (about 9.4 per image) |
| **Classes** | 6 (`car`, `Human`, `motorcycle`, `bus`, `auto_rickshaw`, `truck`) |
| **Shape type** | Rectangle only |
| **Guidelines** | [annotation_guidelines.md](annotation_guidelines.md) (v1.2) |

## Dataset

The images come from a public Kaggle vehicle-detection dataset (Traffic Vehicles Object Detection). Many of the images are stock photos and video frames, so the images themselves are **not included** in this repository. Only the guidelines, statistics, and example screenshots are shared.

The scenes are intentionally varied: day and night, rain, dense city traffic, highways, mixed pedestrians and vehicles, and heavy motorcycle traffic.

## Label distribution

| Label | Objects | Share |
|---|---|---|
| car | 196 | 52% |
| Human | 93 | 25% |
| motorcycle | 36 | 10% |
| bus | 22 | 6% |
| auto_rickshaw | 19 | 5% |
| truck | 11 | 3% |
| **Total** | **377** | **100%** |

All 377 annotations are Rectangles. No polygons were used, in line with the guidelines.

## Workflow

1. **Wrote the guidelines first.** The label set, a 50% visibility rule, a minimum object size of about 30 x 30 pixels, and decision rules for ambiguous cases (vans, riders and passengers, people inside or on top of vehicles, night scenes, occlusion).
2. **Annotated all images** in CVAT with bounding boxes, applying the same rules in every image.
3. **Reviewed every image in a second pass**, after a break, and corrected the errors found.
4. **Updated the guidelines** (v1.0, v1.1, v1.2) whenever a new edge case required a consistent decision.

## Quality results

| Metric | Value |
|---|---|
| Images annotated | 40 |
| Objects labeled | 377 |
| Corrections made in the review pass | about 12 |
| Estimated error rate (corrections / objects) | about 3% |
| Average time per image | about 5 minutes |

The review was a self-review by a single annotator, so these numbers are an estimate of first-pass quality, not a measure of agreement between annotators. The time per image is high because many scenes contain dozens of overlapping vehicles and people.

## Main challenges and what they taught me

- **Consistency over speed.** The same type of vehicle must get the same label in every image, so each ambiguous case was turned into a written rule.
- **Dense and occluded scenes.** Rules for partly hidden objects (box the visible part, skip if less than 50% is visible) kept the labeling stable.
- **Rotated boxes.** Some early boxes were accidentally rotated in CVAT, which leaves empty corners. They were redrawn as straight rectangles to follow the guideline.
- **Class boundaries.** Deciding where a van ends and a truck or minibus begins needed an explicit rule.
- **Low-quality images.** Objects too small or too unclear to identify without guessing were skipped, following the size and visibility rules.

## Limitations

- Single annotator, no inter-annotator agreement measured.
- Small dataset (40 images), so it is not suitable for training a model.
- Small and distant objects are excluded by the size rule.
- Several images come from the same video, so scenes can repeat.

## Repository contents

- `README.md`: this file
- `annotation_guidelines.md`: the full annotation guidelines (v1.2)
- `screenshots/`: examples of annotated images and the CVAT interface
