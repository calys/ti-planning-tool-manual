## Local Anonymization (Data Privacy Workflow)

> **Coming soon in TIP V5.0** — This feature is not yet available and is currently under development. Details on this page are subject to change.

**_Summary_**:

TIP V5.0 will introduce an optional local anonymization workflow for users with data privacy concerns. An anonymization tool, available as part of [Sim4Life](https://sim4life.swiss/), can be installed locally to deidentify magnetic resonance images before they are uploaded to the cloud. The tool deforms facial features beyond recognition while preserving the accuracy of internal tissues relevant for TI stimulation planning, and automatically segments the different tissues. Only the anonymized, segmented data is then uploaded to the cloud for electromagnetic simulation.

----

### Motivation

In the standard TIP workflow, magnetic resonance (MR) images are uploaded directly to the cloud for processing, including automatic segmentation from MR images and personalization of the head model. Some users and institutions have concerns about uploading identifiable medical images to remote servers. To address this, TIP V5.0 will offer a **local anonymization workflow** that ensures no personally identifiable anatomical features leave the user's local environment.

### How It Works

The anonymization workflow consists of two stages:

1. **Local Preprocessing (on your machine)**

   - Install the anonymization tool, which is distributed as part of [Sim4Life](https://sim4life.swiss/).
   - Load your MR image file (e.g., T1-weighted MRI in NIfTI format) into the tool.
   - The tool **deforms facial features** (face, ears, etc.) beyond recognition, removing identifying characteristics from the image.
   - Crucially, internal tissue structures relevant for TI planning are **not degraded** by this process.
   - The tool also **automatically segments** the different tissues in the image.
   - The output is an anonymized, segmented image file ready for upload.

2. **Cloud Simulation (AWS)**

   - Upload the anonymized, segmented image file to the TIP platform.
   - The platform runs **66 ohmic quasi-static electromagnetic simulations** on the AWS cloud using the anonymized personalized head model.
   - These 66 basis simulations can be **recombined at the postprocessing stage** to reproduce the TI fields for any electrode montage — there is no need to rerun simulations when exploring different configurations.

### Cost

Running the cloud simulations for a personalized head model costs approximately **$60 per model**. This cost is at the charge of the user and is managed through the [Billing Center](/docs/platform_introduction/billing_center.md).

### Key Benefits

- **Privacy**: Identifiable facial features never leave your local machine.
- **Accuracy**: Internal tissue geometry is fully preserved — simulation quality is not compromised.
- **Flexibility**: The 66 precomputed basis simulations allow postprocessing exploration of any electrode montage without additional simulation cost.
- **Integration**: The anonymization tool is bundled with [Sim4Life](https://sim4life.swiss/), requiring no separate installation.

### Requirements

- A local installation of [Sim4Life](https://sim4life.swiss/) with the anonymization module.
- A T1-weighted MRI scan meeting the [data quality requirements](/docs/services/file_picker.md) outlined in Step 0.
- A TIP account with sufficient credits for cloud simulation (see [Billing Center](/docs/platform_introduction/billing_center.md)).
