# FireAURA-Net

This repository accompanies the following research paper:

**FireAURA-Net: Progressive Candidate-Aware Representation and Localization for Tiny Forest-Fire Detection in Remote Sensing Imagery**

*IEEE Journal of Selected Topics in Applied Earth Observations and Remote Sensing (JSTARS)*, 2026.

**DOI:** https://doi.org/10.1109/JSTARS.2026.3744354

## FIRESET: Dataset Description and Annotation Protocol

### Scope and Sources

FIRESET is a single-class dataset for detecting tiny forest fire points in remote sensing imagery. It contains fire-containing images and non-fire background images collected from public forest-fire datasets, repositories, online resources, UAV video frames, and manually selected non-fire scenes.

Fire-containing images are predominantly remote-sensing observations. Non-fire images include diverse viewpoints and challenging backgrounds such as sunsets, yellow vegetation, and dry grass. The target class, `fire`, covers identifiable visible flames or fire-point instances. The dataset supports bounding-box detection, not smoke detection or pixel-level flame segmentation.

### Screening and Annotation Unification

Before the experimental split, candidate images were manually screened to remove clearly identifiable duplicates or highly similar samples across sources, including highly similar consecutive UAV frames.

Source annotations were not directly adopted as final ground truth. Identifiable fire instances were re-examined and re-annotated under a unified protocol and assigned to the single `fire` class, rather than merely relabeling source categories.

Smoke without identifiable visible flames and fire-like non-fire regions were treated as background. Smoke alone was not used to infer invisible fire points. Non-fire images received no fire bounding boxes.

### Bounding-Box Principles

- **Visible extent:** Tight axis-aligned boxes enclosed identifiable visible flames while minimizing unrelated smoke, vegetation, and background.
- **Separate instances:** Spatially distinguishable fire points were annotated separately.
- **Irregular flames:** Boxes followed the identifiable visible extent; their rectangular shape may include some background.
- **Tiny instances:** Clearly identifiable fire points were retained regardless of their small size.

Boxes indicate visible fire locations and rectangular extents, not exact flame contours, smoke boundaries, or hidden fire extent. Pixels inside a box are not necessarily all flame pixels.

### Dataset Contents and Statistics

The merged COCO annotation file prepared for this release contains:

| Item | Count |
|---|---:|
| Total images | 836 |
| Images with annotated fire instances | 531 |
| Images without fire annotations | 305 |
| Fire bounding boxes | 1,603 |
| Detection classes | 1 (`fire`) |

The figures above describe the current merged annotation file. They should not be interpreted as train/validation/test subset statistics.


### Dataset Organization

FIRESET images and annotations are publicly available through this repository.

The COCO-format annotations are stored in the repository, while the dataset images are distributed as a ZIP archive through GitHub Releases.

Repository structure:

```text
FireAURA-Net/
├── README.md
└── datasets/
    └── FIRESET/
        └── annotations/
            └── instances_all.json
```

Release asset:
- `FIRESET-images.zip` (836 images)

### Download and Usage

**Dataset images:**

Download `FIRESET-images.zip` from the [FIRESET Dataset Release](https://github.com/Lavender0311/FireAURA-Net/releases/tag/dataset).

**COCO annotations:**

Download [instances_all.json](https://github.com/Lavender0311/FireAURA-Net/blob/main/datasets/FIRESET/annotations/instances_all.json).

After downloading, extract the image archive and organize the files as follows:

```text
FIRESET/
├── images/
│   └── [836 image files]
└── annotations/
    └── instances_all.json
```

The `file_name` values in the JSON correspond to the original image filenames. All images should be kept under the `images/` directory without renaming.

The released annotations do not include predefined training, validation, or test splits. Users may construct their own splits following the guidance below.


### Annotation Format

The annotations use the COCO JSON format, with the `images`, `annotations`, and `categories` fields. The only detection category is `fire` (`category_id = 1`). Each bounding box is specified in original-image pixel coordinates as `[x, y, width, height]`, where `(x, y)` denotes the upper-left corner. The `image_id` field links each annotation to the corresponding image record.

Images without fire annotations remain in `images` but have no associated fire entries in `annotations`. Bounding boxes do not provide pixel-level flame segmentation masks.

### Public Release

This release includes the retained FIRESET images and COCO-format bounding-box annotations for all annotated fire instances. Non-fire images remain in the image records without associated fire annotations.

The dataset is provided as an unpartitioned collection. The training, validation, and test split lists and per-image subset assignments used for the experiments reported in the paper are not provided in this release.

### Guidance for User-Defined Splits

Users may construct training, validation, and test splits according to their experimental needs. When reporting results on user-defined splits, the splitting procedure, subset sizes, random seed where applicable, and image assignments should be documented to facilitate comparison and reuse. Because quantitative results may depend on dataset partitioning, results obtained using alternative splits should be interpreted together with the corresponding split settings.

### Citation

If FIRESET is useful for your research, please cite the associated paper:

**FireAURA-Net: Progressive Candidate-Aware Representation and Localization for Tiny Forest-Fire Detection in Remote Sensing Imagery.**

*IEEE Journal of Selected Topics in Applied Earth Observations and Remote Sensing*, 2026.

https://doi.org/10.1109/JSTARS.2026.3744354
