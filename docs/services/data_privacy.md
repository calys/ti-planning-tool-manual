## Local Anonymization (Data Privacy Workflow)

> **Coming soon in TIP V5.0** — This feature is not yet available and is currently under development. Details on this page are subject to change.

**_Summary_**:

TIP V5.0 will introduce an optional local anonymization workflow for users with data privacy concerns. A personalizer pipeline, available as part of [Sim4Life](https://sim4life.swiss/), can be run locally to generate an anonymized, segmented head model from a T1 MRI scan. The tool deforms facial features beyond recognition while preserving the accuracy of internal tissues relevant for TI stimulation planning, and automatically segments the different tissues. Only the anonymized, segmented output is then uploaded to the cloud for electromagnetic simulation.

----

### Motivation

In the standard TIP workflow, magnetic resonance (MR) images are uploaded directly to the cloud for processing, including automatic segmentation from MR images and personalization of the head model. Some users and institutions have concerns about uploading identifiable medical images to remote servers. To address this, TIP V5.0 will offer a **local anonymization workflow** that ensures no personally identifiable anatomical features leave the user's local environment.

### How It Works

The anonymization workflow consists of two stages:

#### 1. Local Preprocessing (on your machine)

The local personalizer pipeline (`run_personalizer.bat`) generates an anonymized, personalized head model with electrode placement from a T1 MRI scan using Sim4Life.

**Prerequisites**
- [Sim4Life](https://sim4life.swiss/) **version 9.4 or later**, installed on Windows.
- A T1 MRI scan in NIfTI format (`.nii.gz`). The filename must contain `t1`.
- The `personalizer` Python package is automatically installed into Sim4Life's bundled Python environment on first run.
- Atlas data (~37 MB) is downloaded automatically to `%USERPROFILE%\.personalizer` on first run.

**Input files**

Place your input files in the project's input directory:

```
project_root\
└── inputs\
    ├── input_1\
    │   └── subject_t1.nii.gz       (required — T1 MRI scan)
    ├── input_2\
    │   └── fiducials.sab            (optional — electrode positions)
    └── input_3\
        └── sim_settings.json        (optional — simulation settings)
```

**Running the tool**

Open a Command Prompt and run the batch file. Paths containing spaces must be enclosed in double quotes:

```bat
run_personalizer.bat --sim4life "C:\Program Files\Sim4Life_9.4" --project-root C:\data\subj01 --electrode-radius 7.0
```

Key arguments:

| Argument                | Description                                                |
| ----------------------- | ---------------------------------------------------------- |
| `--project-root PATH`  | Project root directory (contains `inputs/` and `outputs/`) |
| `--electrode-radius MM` | Electrode radius in mm (e.g. `7.0`)                       |
| `--electrode-type TYPE` | Preset type: `ROUND_1_6CM2` or `ROUND_3CM2`               |
| `--sim4life PATH`       | Sim4Life installation directory (if non-default)           |
| `--atlas NAME`          | Brain atlas to register (e.g. `ICBM_152`)                 |
| `--dti`                 | Process DTI/DWI data for anisotropic conductivity          |

You must provide either `--electrode-radius` or `--electrode-type`.

**What it does**

- The tool **deforms facial features** (face, ears, etc.) beyond recognition, removing identifying characteristics from the image.
- Crucially, internal tissue structures relevant for TI planning are **not degraded** by this process.
- It **automatically segments** the different tissues in the image and generates a personalized head model with electrode placement.

**Output**

The pipeline produces the following files in the project's `outputs/` directory:

| Folder              | Contents                            |
| ------------------- | ----------------------------------- |
| `outputs/output_1/` | SMASH file (`.smash`) — head model  |
| `outputs/output_2/` | SAB file (`.sab`) — head model      |
| `outputs/output_3/` | T1 image (`.nii.gz`) — processed T1 |
| `outputs/output_5/` | JSON config — target coordinates    |
| `outputs/output_6/` | SAT file (`.sat`) — head model      |

All output files are bundled into a zip archive (`results.zip`) along with a `personalizer_args.json` file that records the exact parameters used.

> **Tip**: To inspect the anonymized head model locally, open Sim4Life, go to **File > Import...**, and select the `.smash` or `.sab` file from the outputs.

#### 2. Cloud Simulation (AWS)

- Upload the output zip directly to the TIP platform.
- The platform runs **66 ohmic quasi-static electromagnetic simulations** on the AWS cloud using the anonymized personalized head model.
- These 66 basis simulations can be **recombined at the postprocessing stage** to reproduce the TI fields for any electrode montage — there is no need to rerun simulations when exploring different configurations.

### Cost

Running the cloud simulations for a personalized head model costs approximately **$60 per model**. This cost is at the charge of the user and is managed through the [Billing Center](/docs/platform_introduction/billing_center.md).

### Key Benefits

- **Privacy**: Identifiable facial features never leave your local machine. Only the anonymized, segmented head model is uploaded.
- **Accuracy**: Internal tissue geometry is fully preserved — simulation quality is not compromised.
- **Flexibility**: The 66 precomputed basis simulations allow postprocessing exploration of any electrode montage without additional simulation cost.
- **Integration**: The personalizer pipeline is bundled with [Sim4Life](https://sim4life.swiss/) (version 9.4+) and installs its dependencies automatically on first run.

### Requirements

- A local installation of [Sim4Life](https://sim4life.swiss/) **version 9.4 or later** on Windows.
- A T1-weighted MRI scan in `.nii.gz` format meeting the [data quality requirements](/docs/services/file_picker.md) outlined in Step 0.
- A TIP account with sufficient credits for cloud simulation (see [Billing Center](/docs/platform_introduction/billing_center.md)).
