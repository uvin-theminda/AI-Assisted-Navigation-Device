# Candidate Object-Detection Dataset Assessment – WalkBuddy ML Stream

## Task

Assess existing candidate object-detection datasets for their suitability for the WalkBuddy navigation model. This assessment focuses on dataset provenance, taxonomy compatibility, licensing, annotation format, coverage, and suitability for further validation.

No datasets are downloaded, merged, relabelled, modified, or used for training as part of this task.

## Current Status

The project already contains a set of candidate datasets in `ML_side/config/download_sheet.yaml`. Additional dataset searching is therefore not the current priority.

This document assesses the existing candidates and records information required before they can proceed through the project's dataset inspection and validation workflow.

A dataset being listed as `approved` in `download_sheet.yaml` is not treated by this assessment as evidence of final legal, quality, privacy, or training approval. The current dataset documentation states that these require independent review.

## Verified Current Model Classes

The current model baseline documentation confirms that the verified local `best.pt` artifact contains seven classes:

- book
- books
- monitor
- office-chair
- whiteboard
- table
- tv

`ML_side/config/newdata.yaml` additionally lists `couch`. However, the current baseline documentation states that `couch` is not present in the verified `best.pt` artifact.

The current baseline evaluation also identifies important navigation objects that are unsupported by the existing model, including person, bicycle, door, pole and vehicle.

## WalkBuddy MVP Target Taxonomy

The current development branch defines the following eight-class WalkBuddy MVP taxonomy:

| ID | Target Class |
|---:|---|
| 0 | person |
| 1 | stairs |
| 2 | door |
| 3 | chair |
| 4 | table |
| 5 | pole |
| 6 | bicycle |
| 7 | vehicle |

This taxonomy is defined in `ML_side/config/taxonomy_mapping.yaml` and documented in `ML_side/datasets/README.md`.

Earlier work on this task treated these classes as proposed and pending approval. The latest repository documentation now records them as the approved MVP taxonomy.

## Current Model to MVP Taxonomy Gap

| MVP Class | Present in Verified Current Model? | Related Current Class | Assessment |
|---|---|---|---|
| person | No | — | Missing |
| stairs | No | — | Missing |
| door | No | — | Missing |
| chair | No | office-chair | Related class exists, but taxonomy does not directly match |
| table | Yes | table | Directly represented |
| pole | No | — | Missing |
| bicycle | No | — | Missing |
| vehicle | No | — | Missing |

The current model therefore does not directly represent seven of the eight MVP taxonomy classes. `table` is the only direct class match.

## Existing Candidate Dataset Sources

The current repository identifies candidate datasets from Kaggle, Roboflow and other sources. The taxonomy mapping already contains proposed mappings from several of these datasets into the eight WalkBuddy target classes.

The main object-detection candidates relevant to this assessment include:

- obstacle_detection_roboflow
- obstacle_detection_kaggle
- indoor_object_detection
- light_poles
- pedestrian_detection
- doors_detection
- indoor_detection_vineeth
- indoor_objects_5iwhq
- revised_pedestrian_obstacle_detection
- pedestrian_walk
- outdoor_objects
- footpath_detection
- stairs_detection

Datasets intended specifically for segmentation or unrelated tasks are outside the scope of this object-detection assessment.

## Current Restrictions

During this assessment:

- raw datasets will not be uploaded to GitHub;
- datasets will not be merged or relabelled;
- class IDs will not be changed;
- model training will not be started;
- the current `best.pt` will not be replaced;
- dataset mappings will not be silently inferred;
- large or sensitive dataset material will remain outside Git.

The purpose of this task is assessment and documentation before further provenance, quality and compatibility validation.

## Candidate Dataset Assessment

For each relevant candidate, the following information will be assessed:

- exact dataset and source;
- dataset version;
- stated licence;
- complete source class list;
- image count;
- annotation format;
- indoor, outdoor or mixed coverage;
- proposed mapping to the WalkBuddy MVP taxonomy;
- quality or compatibility concerns;
- recommendation.

Recommendations use the following outcomes:

1. **Proceed to provenance validation and inspection**
2. **Investigate further**
3. **Reject**

### Candidate Assessments

#### 1. Obstacle Detection – Roboflow

- **Repository ID:** `obstacle_detection_roboflow`
- **Source:** Roboflow Universe – Visually Impaired Obstacle Detection
- **Source URL:** https://universe.roboflow.com/visually-impaired-obstacle-detection-uxdze/obstacle-detection-yeuzf
- **Version:** 11
- **Task:** Object Detection
- **Stated licence:** CC BY 4.0
- **Image count:** 9,183
- **Dataset split:** 7,855 train / 865 validation / 463 test
- **Annotation format:** Object-detection annotations; Roboflow provides YOLO TXT/YAML export formats including YOLOv8.
- **Coverage:** Primarily outdoor obstacle/navigation scenes.
- **Relevant source classes:** Bicycle, Bus, Car, Electric pole, Motorcycle, Person
- **Proposed WalkBuddy mappings:**
  - Bicycle → bicycle
  - Bus → vehicle
  - Car → vehicle
  - Electric pole → pole
  - Motorcycle → vehicle
  - Person → person
- **Unmapped/excluded classes recorded in the repository:** Dog, Traffic signs, Tree, Uncovered manhole
- **WalkBuddy classes covered:** person, pole, bicycle, vehicle
- **Quality / compatibility concerns:** The dataset does not cover the complete WalkBuddy taxonomy. Door, stairs, chair and table require other candidate sources. Licence provenance and the mapped annotations should still pass the project's independent validation and inspection workflow before training use.
- **Recommendation:** Proceed to provenance validation and inspection.

#### 2. Obstacle Detection – Kaggle

- **Repository ID:** `obstacle_detection_kaggle`
- **Source:** Kaggle – Obstacle Detection Dataset
- **Source URL:** https://www.kaggle.com/datasets/abtinzandi/obstacle-detection-dataset
- **Dataset version:** Not specified in the current repository configuration
- **Task:** Object Detection
- **Stated licence:** MIT
- **Image count:** Not yet independently verified from the exact source
- **Annotation format:** YOLO object-detection format
- **Coverage:** Primarily outdoor navigation and obstacle scenes
- **Relevant source classes:** Bike, Car, Person, Stairs, Electrical Pole, Motorcycle, Truck, Bus, Chair
- **Proposed WalkBuddy mappings:**
  - Bike → bicycle
  - Car → vehicle
  - Person → person
  - Stairs → stairs
  - Electrical Pole → pole
  - Motorcycle → vehicle
  - Truck → vehicle
  - Bus → vehicle
  - Chair → chair
- **Other source classes:** Building, Traffic sign, Road, Dustbin, Dog, Manhole, Tree, Guard rail, Pedestrian crosswalk, Bench, Traffic Cone, Fire hydrant, Traffic Barrel, Plant Pot, Electrical Box and Bicycle Rack
- **WalkBuddy classes covered:** person, stairs, chair, pole, bicycle, vehicle
- **Quality / compatibility concerns:** The exact dataset version is not recorded in `download_sheet.yaml`. Related published material for this dataset lineage contains data aggregated from multiple sources, so source-level licensing and provenance should be checked independently rather than relying only on the top-level MIT licence. Door and table are not covered by the current mapping.
- **Recommendation:** Investigate further before training use, particularly to verify the exact dataset version and source-level licensing/provenance.

#### 3. Indoor Object Detection – Kaggle

- **Repository ID:** `indoor_object_detection`
- **Source:** Kaggle – Indoor Objects Detection
- **Source URL:** https://www.kaggle.com/datasets/thepbordin/indoor-object-detection
- **Dataset version:** Not specified in the current repository configuration
- **Task:** Object Detection
- **Stated licence:** GNU Lesser General Public License 3.0
- **Image count:** Not yet independently verified from the exact source
- **Annotation format:** YOLOv5
- **Coverage:** Indoor environments
- **Complete source classes:** door, openedDoor, cabinetDoor, refrigeratorDoor, window, chair, table, cabinet, sofa/couch, pole
- **Proposed WalkBuddy mappings:**
  - door → door
  - openedDoor → door
  - cabinetDoor → door
  - refrigeratorDoor → door
  - chair → chair
  - table → table
  - pole → pole
- **Unmapped classes:** window, cabinet, sofa/couch
- **WalkBuddy classes covered:** door, chair, table, pole
- **Quality / compatibility concerns:** The exact dataset version is not recorded in `download_sheet.yaml`. Several different source classes are mapped into the single WalkBuddy `door` class, so annotation consistency should be inspected before use. The dataset is focused on indoor environments and therefore does not provide sufficient coverage for outdoor navigation classes such as person, bicycle and vehicle.
- **Recommendation:** Proceed to provenance validation and inspection, while verifying the exact dataset version and reviewing the proposed door-class mappings.

#### 4. Light Poles – Kaggle

- **Repository ID:** `light_poles`
- **Source:** Kaggle – Light Poles
- **Source URL:** https://www.kaggle.com/datasets/samuelayman/light-poles
- **Dataset version:** Not specified in the current repository configuration
- **Task:** Object Detection
- **Stated licence:** Apache 2.0
- **Image count:** Not yet verified from the exact source
- **Annotation format:** Not yet independently verified
- **Coverage:** Outdoor environments
- **Relevant source class:** light pole
- **Proposed WalkBuddy mapping:**
  - light pole → pole
- **WalkBuddy classes covered:** pole
- **Quality / compatibility concerns:** This is a specialised single-class dataset and therefore only contributes to the WalkBuddy `pole` class. The exact dataset version, image count, annotation format and licence details should be independently verified before training use. Pole annotations should also be inspected to determine whether the dataset contains sufficient variation in pole size, shape, distance and environment for navigation use.
- **Recommendation:** Investigate further before training use, with particular attention to dataset version, annotation format, image count and pole diversity.

#### 5. Pedestrian Detection – Kaggle

- **Repository ID:** `pedestrian_detection`
- **Source:** Kaggle – Pedestrian Dataset
- **Source URL:** https://www.kaggle.com/datasets/smeschke/pedestrian-dataset
- **Dataset version:** Not specified in the current repository configuration
- **Task:** Object Detection
- **Stated licence:** CC0 Public Domain
- **Image count:** Not yet verified from the exact source
- **Annotation format:** Not yet independently verified
- **Coverage:** Pedestrian-focused scenes
- **Relevant source class:** person
- **Proposed WalkBuddy mapping:**
  - person → person
- **WalkBuddy classes covered:** person
- **Quality / compatibility concerns:** This is a specialised dataset that only contributes to the WalkBuddy `person` class. The exact dataset version, image count and annotation format should be verified before training use. The images should also be inspected to determine whether pedestrian examples are representative of WalkBuddy use cases, including different distances, viewpoints, lighting conditions and levels of occlusion.
- **Recommendation:** Investigate further before training use, particularly to verify the dataset metadata and assess whether the pedestrian examples are sufficiently representative for WalkBuddy.

#### 6. Doors Detection – Kaggle

- **Repository ID:** `doors_detection`
- **Source:** Kaggle – Doors
- **Source URL:** https://www.kaggle.com/datasets/dataclusterlabs/doors-doors
- **Dataset version:** Not specified in the current repository configuration
- **Task:** Object Detection
- **Stated licence:** CC0 Public Domain
- **Image count:** Not yet verified from the exact source
- **Annotation format:** Not yet independently verified
- **Coverage:** Door-focused scenes
- **Current WalkBuddy mapping:** No explicit mapping for `doors_detection` is currently recorded in `taxonomy_mapping.yaml`.
- **Potential target class:** door
- **WalkBuddy classes potentially covered:** door
- **Quality / compatibility concerns:** This is a specialised door dataset, but the current repository does not contain an explicit taxonomy mapping for this source. The exact dataset version, complete source class list, image count and annotation format still need to be verified. A mapping to the WalkBuddy `door` class should only be added after the source labels and annotations have been reviewed.
- **Recommendation:** Investigate further before training use, particularly to verify the dataset metadata, source classes and annotation compatibility.

#### 7. Indoor Detection – Roboflow

- **Repository ID:** `indoor_detection_vineeth`
- **Source:** Roboflow Universe – Indoor Detection
- **Source URL:** https://universe.roboflow.com/vineeth-optimus/indoor-9xgfb
- **Version:** 1
- **Task:** Object Detection
- **Stated licence:** CC BY 4.0
- **Image count:** Not yet verified from the exact source
- **Annotation format:** Not yet independently verified
- **Coverage:** Indoor environments
- **Complete source classes recorded in the repository:** cabinet, cabinetDoor, chair, couch, door, openedDoor, pole, refrigeratorDoor, table, window
- **Proposed WalkBuddy mappings:**
  - cabinetDoor → door
  - chair → chair
  - door → door
  - openedDoor → door
  - pole → pole
  - refrigeratorDoor → door
  - table → table
- **Unmapped classes:** cabinet, couch, window
- **WalkBuddy classes covered:** door, chair, table, pole
- **Quality / compatibility concerns:** Several different door-related source classes are mapped into the single WalkBuddy `door` class. These mappings and annotation consistency should be inspected before training use. As an indoor-focused dataset, it also does not provide coverage for important outdoor classes such as bicycle and vehicle.
- **Recommendation:** Proceed to provenance validation and inspection, with particular attention to annotation quality and the consolidation of multiple door-related source classes.

#### 8. Indoor Objects – Roboflow

- **Repository ID:** `indoor_objects_5iwhq`
- **Source:** Roboflow Universe – Indoor Objects
- **Source URL:** https://universe.roboflow.com/indoor-objects/indoor-5iwhq
- **Version:** 2
- **Task:** Object Detection
- **Stated licence:** CC BY 4.0
- **Image count:** Requires verification for the exact version
- **Annotation format:** Not yet independently verified
- **Coverage:** Indoor environments
- **Source classes recorded in the repository mapping:** bed, chair, door, door-frame, shower, sink, sofa, stairs, table, toilet
- **Proposed WalkBuddy mappings:**
  - chair → chair
  - door → door
  - door-frame → door
  - stairs → stairs
  - table → table
- **Unmapped classes:** bed, shower, sink, sofa, toilet
- **WalkBuddy classes covered:** stairs, door, chair, table
- **Quality / compatibility concerns:** Available dataset information shows inconsistencies in the reported number of classes and images, so the metadata for the exact version 2 dataset should be verified before use. The `door` and `door-frame` classes are both mapped to the WalkBuddy `door` class and should be inspected for annotation consistency. The dataset is indoor-focused and does not cover person, pole, bicycle or vehicle.
- **Recommendation:** Investigate further before training use because the exact version metadata and class/image counts require verification.

#### 9. Pedestrian Walk – Roboflow

- **Repository ID:** `pedestrian_walk`
- **Source:** Roboflow Universe – Pedestrian Walk
- **Source URL:** https://universe.roboflow.com/objection-detection/pedestrian-walk
- **Version:** 1
- **Task:** Object Detection
- **Stated licence:** Public Domain
- **Image count:** Not yet verified from the exact source
- **Annotation format:** Not yet independently verified
- **Coverage:** Pedestrian-focused scenes
- **Source classes recorded in the repository:** B, F, M
- **Proposed WalkBuddy mappings:**
  - B → person
  - F → person
  - M → person
- **WalkBuddy classes covered:** person
- **Quality / compatibility concerns:** The source uses three separate pedestrian-related labels that are all mapped to the single WalkBuddy `person` class. The meaning and consistency of B, F and M should therefore be confirmed during inspection rather than inferred from the class names alone. As a specialised pedestrian dataset, it contributes only to the `person` class and must be combined with other validated sources to cover the full MVP taxonomy.
- **Recommendation:** Proceed to provenance validation and inspection, with particular attention to the meaning and annotation consistency of the three source classes.

#### 10. Outdoor Objects – Roboflow

- **Repository ID:** `outdoor_objects`
- **Source:** Roboflow Universe – Outdoor Objects
- **Source URL:** https://universe.roboflow.com/outdoor-od-fqdik/outdoor-109rx
- **Version:** 1
- **Task:** Object Detection
- **Stated licence:** CC BY 4.0
- **Image count:** Not yet verified from the exact source
- **Annotation format:** Not yet independently verified
- **Coverage:** Outdoor environments
- **Source classes recorded in the repository mapping:** building, foot path, person, plants, road, street light, trees
- **Proposed WalkBuddy mappings:**
  - person → person
  - street light → pole
  - car/vehicle → vehicle (additional visually confirmed source class recorded in the repository mapping)
- **Unmapped classes:** building, foot path, plants, road, trees
- **WalkBuddy classes covered:** person, pole, vehicle
- **Quality / compatibility concerns:** The repository mapping records an additional car/vehicle class that is not declared in the source YAML class list. This discrepancy should be verified during dataset inspection before the mapping is accepted. The dataset provides useful outdoor coverage but does not cover the complete WalkBuddy taxonomy.
- **Recommendation:** Investigate further, particularly the undeclared car/vehicle class and source annotation consistency, before training use.

### Remaining Repository Candidates

The following sources are also recorded in `ML_side/config/download_sheet.yaml`. They are not expanded into full candidate assessments above because they are either specialised supplementary datasets, outside the current object-detection scope, excluded/rejected by the current repository configuration, or require further metadata verification.

| Repository ID | Current Assessment | Reason / Next Action |
|---|---|---|
| `stairs_detection` | Investigate further | Roboflow v1 specialised source for the `stairs` class. Verify image count, annotation quality and provenance before use. |
| `footpath_detection` | Investigate further | Repository mapping includes person plus visually confirmed bicycle and vehicle classes that are not all declared in the source YAML. Mapping discrepancy requires inspection. |
| `revised_pedestrian_obstacle_detection` | Investigate further | Roboflow v4 candidate. Verify complete class list, image count, annotation format and mapping before use. |
| `antic_chairs` | Investigate further | Potential supplementary chair source, but no explicit mapping is currently recorded in `taxonomy_mapping.yaml`. |
| `road_sign_detection` | Reject for current MVP training set | Its recorded classes map outside the approved eight-class WalkBuddy taxonomy. |
| `indoor_objects_roboflow` | Excluded from current assessment | Explicitly listed under `excluded_datasets` in `taxonomy_mapping.yaml`. |
| `obstacle_detection_huggingface` | Rejected in current repository configuration | `download_sheet.yaml` currently records this source as rejected. |
| `fpv_crosswalk_segmentation` | Outside current scope | Segmentation dataset rather than the current eight-class object-detection task. |
| `mapillary_vistas` | Outside current assessment | Broader scene-level dataset requiring a separate assessment rather than direct inclusion in the current object-detection candidate workflow. |

## Overall Recommendation

The existing candidate sources provide potential coverage across all eight WalkBuddy MVP classes when considered together, but no single assessed dataset provides complete taxonomy coverage.

The strongest next step is not to search for additional datasets immediately, but to continue the project's controlled provenance and inspection workflow for the existing candidates. Candidates with clear repository mappings and useful taxonomy coverage should proceed to validation, while candidates with missing versions, uncertain metadata, undeclared source classes or unclear mappings should remain under investigation.

Particular attention should be given to:

- verifying exact dataset versions and source-level licences;
- confirming image counts and complete source class lists;
- inspecting annotation quality and class consistency;
- resolving undeclared or inconsistent source classes;
- checking indoor and outdoor representation;
- checking duplicate and split-leakage risks using the repository inspection tooling;
- maintaining the approved WalkBuddy class IDs defined in `taxonomy_mapping.yaml`.

No dataset should be merged, relabelled or used for training solely on the basis of this assessment. Final inclusion should occur only after the repository's provenance, licensing, quality and compatibility checks have been completed.
