<h1 align="center">Warp reference Ventral Putamen ROI(s) to Subject Space</h1>

<p align="center">
  Warps left and right ventral putamen ROIs from MNI152 space into a subject's T1-weighted space using an ANTs rigid, affine and SyN registration and its inverse.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/brainlife.app.792"><img src="https://img.shields.io/badge/Brainlife-brainlife.app.792-blue.svg" alt="Run on brainlife.io"></a>
</p>

## At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Warps left and right ventral putamen ROIs from MNI152 space into a subject's T1-weighted space using an ANTs rigid, affine and SyN registration and its inverse.**

Registers the subject brain to the MNI152 1 mm template with antsRegistration (rigid, affine, SyN, using the subject brain mask), then applies the inverse warp and affine with antsApplyTransforms to the bundled ventral putamen masks so they land on the subject T1 grid. Use the resulting ROIs for subject-level segmentation or tracking. The README states this branch is not meant to be run directly on brainlife.io but as part of a specific workflow.

| | |
|---|---|
| **Inputs** | `neuro/anat/t1w` · `neuro/mask` |
| **Outputs** | `neuro/rois` |
| **Container** | `brainlife/ants:2.2.0` |
| **Resources** | 8 CPUs · 18 h walltime |
| **Run it** | [doi.org/10.25663/brainlife.app.792](https://doi.org/10.25663/brainlife.app.792) |

#### Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `t1` | `neuro/anat/t1w` | yes | Subject T1-weighted image; the ROIs are resampled onto its grid. Should be skull-stripped (registration uses the MNI152 brain template). |
| `brainMask` | `neuro/mask` (brain) | yes | This is used to align the subject's data to the MNI152 template. |

#### Outputs

| Output | Datatype | Description |
|---|---|---|
| `output` | `neuro/rois` | The post-warp (now in subject space) ROI(s) |

<!-- brainlife-app:end -->

## Running the App

### On brainlife.io

Open the App at [doi.org/10.25663/brainlife.app.792](https://doi.org/10.25663/brainlife.app.792), choose `neuro/anat/t1w`, `neuro/mask` from your project and press **Execute**. The results are saved to your project as `neuro/rois`.

### Locally

You need [Singularity/Apptainer](https://apptainer.org/) (the App runs in `brainlife/ants:2.2.0`), [`jq`](https://jqlang.github.io/jq/).

1. Clone this repository.
2. Create `config.json` with the paths to your inputs and the parameters:

   ```json
   {
       "t1": "/path/to/t1/t1",
       "mask": "/path/to/brainMask/mask"
   }
   ```

3. Run `./main`.

## How to adapt this template to YOUR desired use case.

The process for adapting this app to your use case is actually quite simple.  All one needs to do is create a branch / fork of [this repository](https://github.com/DanNBullock/app-warp_refROI_to_subjSpace/tree/master) and then upload the ROIs (_which are themselves in MNI space_) that you wish to warp _to_ subject space.  When that branch / fork is [set up as an app](https://brainlife.io/docs/apps/register/), the resultant brainlife.io app should output the desired ROI(s) in subject space when run with the appropriate inputs.

**TLDR**: Make a fork of this repository and upload your rois to the `rois/` directory.

## Citing

If you use this App, please cite it, the software it builds on and brainlife.io:

- Warp reference Ventral Putamen ROI(s) to Subject Space. brainlife.io App. [doi:10.25663/brainlife.app.792](https://doi.org/10.25663/brainlife.app.792)
- Avants et al. A reproducible evaluation of ANTs similarity metric performance in brain image registration. *NeuroImage* 54:2033-2044 (2011). [doi:10.1016/j.neuroimage.2010.09.025](https://doi.org/10.1016/j.neuroimage.2010.09.025)
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Authors

- [Daniel Bullock](https://github.com/DanNBullock)

## Funding

[![Wellcome-226486/Z/22/Z](https://img.shields.io/badge/Wellcome-226486%2FZ%2F22%2FZ-purple.svg)](https://wellcome.org/)
[![NIH-NINDS-U24NS140384](https://img.shields.io/badge/NIH_NINDS-U24NS140384-green.svg)](https://reporter.nih.gov/project-details/11261037)
[![NIH-NINDS-UM1NS132207](https://img.shields.io/badge/NIH_NINDS-UM1NS132207-green.svg)](https://reporter.nih.gov/project-details/11411328)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://reporter.nih.gov/project-details/10262925)
[![NIH-NIBIB-R01EB030896](https://img.shields.io/badge/NIH_NIBIB-R01EB030896-green.svg)](https://reporter.nih.gov/project-details/10428625)
[![NIH-NIMH-R01MH126699](https://img.shields.io/badge/NIH_NIMH-R01MH126699-green.svg)](https://reporter.nih.gov/project-details/10460628)
[![NIH-NIDCD-R01DC020088](https://img.shields.io/badge/NIH_NIDCD-R01DC020088-green.svg)](https://reporter.nih.gov/project-details/11140284)
[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-2203524](https://img.shields.io/badge/NSF_BCS-2203524-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2203524)
[![NSF-IIS-1636893](https://img.shields.io/badge/NSF_IIS-1636893-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-OAC-2148729](https://img.shields.io/badge/NSF_OAC-2148729-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148729)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NSF-IIS-2148700](https://img.shields.io/badge/NSF_IIS-2148700-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148700)
[![NSF-OAC-1916518](https://img.shields.io/badge/NSF_OAC-1916518-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1916518)

<sub>brainlife.io, which runs this App, is publicly funded by Wellcome, the U.S. National Institutes of Health and the U.S. National Science Foundation; acknowledging that support helps keep it running.</sub>
