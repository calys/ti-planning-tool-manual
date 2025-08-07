# Release Notes

## TIP V4.0

### Release Date: 05.06.2025

TIP V4.0 brings intelligent automation, advanced optimization, and a streamlined user experience—delivering improved stimulation outcomes with less effort and greater speed.

### Selected New Features

- **Automated Personalization**: Neural network-based automatic identification and placement of anatomical landmarks for the EEG 10-10 system, eliminating the need for manual fiducial point placement.
- **Smart Optimization with SuMo**: New surrogate-modeling-based optimizer (SuMo) that combines Gaussian process modeling with a multi-objective genetic algorithm to systematically explore the solution space and provide Pareto-optimal solutions.
- **Enhanced Speed and Accuracy**: Optimization runs complete in half the time compared to TIP V3.0 with improved results, leveraging parallel processing to reduce wait times.
- **Streamlined User Workflow**: Simplified protocol design flow with intelligent automation and visualization upgrades, eliminating the electrode selector and sweep steps.

TIP V4.0 also includes many smaller features and general improvements in the presented information content and usability, as well as bug fixes.

----

## TIP V3.0

### Release Date: 24.09.2024

TIP V3.0 now includes the possibility of personalized modeling.

### Selected New Features

- **Personalized Stimulation Modeling**: Users can now upload a subject’s own anatomical data (T1-weighted magnetic resonance imaging (MRI) scans and, optionally, diffusion tensor imaging (DTI) data) for personalized TI stimulation assessment, planning, and optimization. This feature allows for superior stimulation protocols thanks to improved modeling realism and prediction accuracy.
- **Enhanced Target Selection**: Users can register a detailed brain atlas at the International Consortium for Brain Mapping (ICBM) to benefit from an increased number of potential target regions for stimulation optimization.
- **Parallelized Electromagnetic (EM) Simulations**: Leveraging AWS resources, low-frequency EM simulations are set up for individual electrodes and executed in parallel, speeding up the overall process.

TIP V3.0 also includes many smaller features and general improvements in the presented information content and usability, as well as bug fixes.

----

## TIP V2.0

### Release Date: 17.08.2023

TIP V2.0 brings a range of new functionalities and improvements to the Temporal Interference Planning Tool (TIP).

### Selected New Features**

- Library of highly detailed anatomical head models, complete with precomputed field exposures, enabling inter-subject variability assessment
- Mouse model to facilitate TI research involving rodents
- Two new modes complementing the classic TI model: multichannel TI and phase-modulation TI
- Expanded list of brain stimulation targets
- Flexibile optimization goal functions
- Optimized utilization of cloud-computing and parallelization, delivering an interactive user experience for efficient exploration of large stimulation parameter spaces

TIP V2.0 also includes many smaller features and general improvements in the presented information content and usability, as well as bug fixes.

----

## TIP V1.0

### Release Date: 01.09.2022

TIP V1.0 is the first public release of the Temporal Interference Planning Tool (TIP). The tool empowers individual researchers that might not be modeling experts and supports neuroscientists and brain stimulation experts in the design of optimized electrode placement and exposure conditions for targeted Temporal Interference Stimulation (TIS).

### Features

- Accessible fully online
- Based on o<sup>2</sup>S<sup>2</sup>PARC technology
- Based on libraries of precomputed fields
- TI planning setup
  - one anatomical model - [MIDA](https://itis.swiss/virtual-population/regional-human-models/mida-model/)
  - circular shape electrode with a fixed area
  - interactive electrode pair placement
  - selection of the target structure
- Fully automatic, exhaustive search of the considered electrode placement configuration space
- Three key metrics: target exposure magnitude, stimulation selectivity, and collateral stimulation
- Possibility to sort the list of TI configurations
- Study of the resulting exposure can be studied and if desired, the configuration (electrode locations, current magnitudes) can be interactively refined.
- Visualization of TI and high-frequency exposure distributions on top of medical image data
- Visualization of the fields in 2D and 3D
- Report generation
- Exporting fields in .cache
- Interactive exposure analysis in Sim4Life:web
