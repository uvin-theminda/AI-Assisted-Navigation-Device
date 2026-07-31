# Training Data Requirements – WalkBuddy ML Stream

## Task

Find suitable training data from Kaggle, Roboflow, and verified sources for the WalkBuddy object detection model.

## Current Status

Lorenzo clarified that the team currently has enough candidate datasets for the first review, so additional dataset searching should be paused for now.

Datasets previously described as approved should be treated as candidate datasets pending final validation. Before any dataset is combined or used for training, the team still needs to confirm:

- target WalkBuddy classes
- exact dataset version
- licence
- annotation format
- dataset quality

## Current YOLO Model Classes

The current YOLO configuration in `ML_side/config/newdata.yaml` contains 8 classes:

- book
- books
- monitor
- office-chair
- whiteboard
- table
- tv
- couch

## App Detection Requirements Found

Initial code review found that the WalkBuddy app includes detection-related logic for the following categories:

- person
- car
- chair
- general obstacles

Examples found in the codebase:

- `software_side/walkbuddy_reactNative/frontend_reactNative/app/camera.tsx` includes priority and speech handling for `person`, `car`, and `chair`.
- `software_side/walkbuddy_reactNative/frontend_reactNative/app/(tabs)/camera.tsx` includes social awareness logic for `person` detections.
- `software_side/walkbuddy_reactNative/frontend_reactNative/app/(tabs)/predictive-path.tsx` uses YOLO detections to determine obstacle direction.

## Current Object-Detection Candidate Classes

Based on Lorenzo's clarification, the current object-detection candidate classes are:

- people
- stairs
- doors
- chairs
- tables
- poles
- bicycles
- vehicles
- related obstacles

These should be treated as candidate classes until final validation is completed.

## Items Not in Current Scope

The following are not part of the current object-detection dataset work and should be treated as future work.

### Future Segmentation Work

- sidewalks
- crosswalks
- floors
- walls
- traversability masks

### Future Sensor-Fusion / Navigation Research

- GPS datasets
- IMU datasets
- LiDAR datasets
- ROS bag datasets

## Current Restrictions

For now, the team should not:

- merge or relabel datasets
- change class IDs
- begin model training
- upload datasets to GitHub
- implement automatic downloading
- use general Roboflow search pages as final dataset references

## Initial Dataset Gap Analysis

| Class / Concept | In current YOLO config? | Found in app logic / project guidance? | Gap / Notes | Priority |
|---|---|---|---|---|
| book | Yes | Not clearly required in current guidance | Existing class | Low |
| books | Yes | Not clearly required in current guidance | Existing class | Low |
| monitor | Yes | Not clearly required in current guidance | Existing class | Low |
| office-chair | Yes | Related to chairs | May need mapping or validation against `chairs` | Medium |
| whiteboard | Yes | Not clearly required in current guidance | Existing class | Low |
| table | Yes | Yes | Existing class, but dataset quality/version still needs validation | High |
| tv | Yes | Not clearly required in current guidance | Existing class | Low |
| couch | Yes | Possible obstacle but not listed directly | Existing class, needs confirmation | Medium |
| people / person | No | Yes | Missing class required for social awareness and navigation safety | High |
| stairs | No | Yes | Missing navigation hazard class | High |
| doors | No | Yes | Missing navigation/wayfinding class | High |
| chairs | Partially | Yes | App expects `chair`, model has `office-chair`; needs clarification | High |
| poles | No | Yes | Missing obstacle/hazard class | High |
| bicycles | No | Yes | Missing outdoor obstacle class | Medium |
| vehicles / car | No | Yes | App mentions `car`; Lorenzo mentions vehicles | Medium |
| related obstacles | No | Yes | Needs clearer class definition before collection/training | High |

## Dataset Source Documentation Fields

For each candidate dataset source, the following information should be recorded before final validation:

| Dataset Name | Exact Source URL | Platform | Exact Dataset Version | Classes Included | Number of Images | Annotation Format | Licence / Usage Restrictions | Quality Notes | Suitable for WalkBuddy? |
|---|---|---|---|---|---|---|---|---|---|

## Proposed Next Step

Pause additional dataset searching and focus on validating the existing candidate datasets. For each candidate dataset, confirm the exact source, version, licence, annotation format, included classes, image count, and quality before any combining, relabelling, training, or uploading occurs.