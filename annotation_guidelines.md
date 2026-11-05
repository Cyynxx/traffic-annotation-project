# Annotation Guidelines: Street Traffic Object Detection

**Version:** 1.2
**Tool:** CVAT
**Annotation type:** Bounding boxes (Rectangle only)
**Dataset size:** 40 street-scene images
**Scene types:** Day and night traffic, dense city roads, highways, motorcycle traffic, mixed vehicles and pedestrians

---

## 1. Purpose

This document defines how objects are labeled in this project, so that every image is annotated in the same way. The goal is to draw one tight bounding box around every clearly visible vehicle and person, with the correct label. Consistency across all images matters more than speed.

## 2. Label set

| Label | Use for | Do not use for |
|---|---|---|
| `car` | Cars, taxis, SUVs, police cars, vans (e.g. Ford Transit), pickups | Buses, large cargo trucks |
| `bus` | Buses, double-deckers, minibuses | Vans |
| `truck` | Lorries and cargo trucks of any size | Vans and pickups |
| `motorcycle` | Motorcycles and scooters | Bicycles |
| `auto_rickshaw` | Tuk-tuks and three-wheelers | Cars |
| `Human` | Pedestrians, motorcycle riders and passengers, cyclists | Mannequins, posters, reflections |

If a vehicle is hard to classify, choose the closest label. Never leave a clearly visible object unlabeled because it is difficult.

## 3. Drawing rules

1. **Tool:** Use Rectangle only, including for tilted or angled vehicles. Do not use polygons.
2. **Tight boxes:** Box edges touch the outermost visible parts of the object. Include mirrors, bumpers, and antennas. Exclude shadows and reflections.
3. **One object per box:** Never draw one box around a group.
4. **Overlap:** Overlapping boxes are allowed.
5. **Edge of image:** If an object is cut by the image border, draw the box up to the border.
6. **Partial visibility:** Box the visible part only. Never guess where hidden parts end.

## 4. What to label

Label an object only if all three conditions are true:

1. More than **50%** of the object is visible.
2. The box would be at least about **30 x 30 pixels**.
3. The object type can be identified without guessing.

## 5. What to skip

- Objects less than 50% visible (hidden by other objects or cut off).
- Objects smaller than about 30 x 30 pixels (too far away).
- Vehicles or people shown on billboards, posters, screens, or reflections.
- Toys and scale models.
- Bicycles (the cyclist is labeled `Human`, the bicycle is not labeled).

## 6. Decision rules for specific situations

| Situation | Decision |
|---|---|
| Van (Ford Transit, delivery van, minivan) | `car` |
| Taxi, police car, SUV | `car` |
| Cargo lorry, large truck | `truck` |
| Double-decker bus | `bus` |
| Motorcycle with a rider | One `motorcycle` box and one separate `Human` box for each person on it |
| Rider visible but motorcycle more than 50% hidden | Box the rider only |
| Motorcycle visible but rider more than 50% hidden | Box the motorcycle only |
| People inside a vehicle (seen through glass or inside the cabin) | Skip |
| People on the roof of a vehicle or hanging on its sides | `Human`, one box per person |
| Group of people standing close together | One `Human` box per person, never one box for the group |
| Vehicle covered by more than 50% by another vehicle | Skip |
| Partly hidden vehicle with more than 50% visible | Box the visible part only |
| Night scene where only headlights are visible and the shape is unclear | Skip |
| Night scene where the vehicle shape is clearly identifiable | Label normally |
| Tilted vehicle | Rectangle that fits the visible outline |
| Vehicle partly cut by the image border | Label if more than 50% visible, box up to the border |

## 7. Annotation workflow

1. Create the task in CVAT and define all labels as Rectangle.
2. For each image, label large and near objects first, then medium objects, then check the whole image once more before moving on.
3. Apply the same decisions from Section 6 in every image.
4. Reuse boxes (copy and paste) only when objects are in the same position, then adjust them to fit.
5. Save regularly.

## 8. Quality control

Quality is checked in a second full pass after the first annotation pass.

1. Wait at least one day after finishing the first pass, then review every image again from scratch.
2. For each image check: missing objects, wrong labels, loose or tight boxes, objects skipped against the rules, and inconsistencies between images.
3. Record each correction and classify it as one of: missing object, wrong label, loose box, rule violation.
4. Calculate the **error rate** as total corrections divided by total labeled objects.
5. Fix all errors and re-check labels that were changed.

Final quality results are reported in the project README, not in this document.

## 9. Known limitations

- The images come from mixed public sources with varied lighting, resolution, and camera angles.
- Some images are from video frames, so similar scenes may appear more than once.
- Small and distant objects are excluded by the size rule, so this dataset is not suitable for evaluating small-object detection.
- Labeling decisions for ambiguous cases are documented in Section 6 and were applied consistently, but remain a single annotator's judgment.

## 10. Version history

- **v1.0:** Initial label set, 50% visibility rule, and 30 x 30 pixel size rule.
- **v1.1:** Added decisions for vans, riders and passengers, people inside and on top of vehicles, bicycles, night scenes, occlusion by other vehicles, and Rectangle-only drawing.
- **v1.2:** Final dataset size set to 40 images.
