<h1 align="center">tck2trk</h1>

<p align="center">
  This application converts tractography files from the .tck format to the .trk format. It uses a reference anatomy image in NIfTI format to ensure proper alignment.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/brainlife.app.843"><img src="https://img.shields.io/badge/Brainlife-brainlife.app.843-blue.svg" alt="Run on brainlife.io"></a>
</p>

## At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **This application converts tractography files from the .tck format to the .trk format. It uses a reference anatomy image in NIfTI format to ensure proper alignment.**

Converts a .tck tractogram to TrackVis .trk with nibabel, taking the voxel-to-RAS affine, voxel sizes, dimensions and voxel order for the .trk header from a reference image. The reference is the first available of T1w, parcellation or mask (the T2w branch is unreachable because of a typo in main). Use it when a downstream tool needs .trk streamlines; the reference image must be in the same space as the tractogram.

| | |
|---|---|
| **Inputs** | `neuro/track/tck` · `neuro/anat/t1w` (optional) · `neuro/anat/t2w` (optional) · `neuro/mask` (optional) · `neuro/parcellation/volume` (optional) |
| **Outputs** | `neuro/track/trk` |
| **Container** | `brainlife/dipy:1.4.1` |
| **Resources** | 1 CPUs · 8 GB memory · 0.08 h walltime |
| **Run it** | [doi.org/10.25663/brainlife.app.843](https://doi.org/10.25663/brainlife.app.843) |

#### Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `tck` | `neuro/track/tck` | yes | Tractogram in MRtrix .tck format. |
| `t1w` | `neuro/anat/t1w` | no | Optional T1-weighted image used as the reference for the .trk header (first choice). Same space as the tractogram. |
| `t2w` | `neuro/anat/t2w` | no | Optional T2-weighted reference image; not selected by the current code because of a typo in main. |
| `mask` | `neuro/mask` | no | Optional mask used as the reference image if no T1w or parcellation is given. |
| `parc` | `neuro/parcellation/volume` | no | Optional parcellation used as the reference image if no T1w is given. |

#### Outputs

| Output | Datatype | Description |
|---|---|---|
| `trk` | `neuro/track/trk` | The tractogram converted to TrackVis .trk format. |

<!-- brainlife-app:end -->

## Running the App

### On brainlife.io

Open the App at [doi.org/10.25663/brainlife.app.843](https://doi.org/10.25663/brainlife.app.843), choose `neuro/track/tck`, `neuro/anat/t1w`, `neuro/anat/t2w`, `neuro/mask`, `neuro/parcellation/volume` from your project and press **Execute**. The results are saved to your project as `neuro/track/trk`.

### Locally

You need [Singularity/Apptainer](https://apptainer.org/) (the App runs in `brainlife/dipy:1.4.1`), [`jq`](https://jqlang.github.io/jq/).

1. Clone this repository.
2. Create `config.json` with the paths to your inputs and the parameters:

   ```json
   {
       "tck": "/path/to/tck/tck",
       "t1": "/path/to/t1w/t1",
       "t2": "/path/to/t2w/t2",
       "mask": "/path/to/mask/mask",
       "parc": "/path/to/parc/parc",
       "key": "/path/to/parc/key",
       "label": "/path/to/parc/label"
   }
   ```

3. Run `./main`.

## Troubleshooting

- **Error: No valid anatomical reference found in config.json**: Provide a T1w, parcellation or mask input as the reference image.

## Features

- Input: `.tck` tractography file(s) and a reference anatomy image (`.nii` or `.nii.gz`).
- Output: Corresponding `.trk` tractography file(s).
- Skips non-TCK files and optionally overwrites existing TRK files.
- Supports multiple tractography files in a single execution.

## For Python Usage

- Python 3.6+
- Libraries:
  - `nibabel`
  - `argparse`

Install dependencies with:
```bash
pip install -r requirements.txt
```

## For Singularity Usage

- Singularity installed and accessible.

## Notes

- Non-TCK files are skipped automatically.
- Use the `-f` flag to overwrite output files if they already exist.

## Citing

If you use this App, please cite it, the software it builds on and brainlife.io:

- tck2trk. brainlife.io App. [doi:10.25663/brainlife.app.843](https://doi.org/10.25663/brainlife.app.843)
- Garyfallidis et al. Dipy, a library for the analysis of diffusion MRI data. *Frontiers in Neuroinformatics* 8 (2014). [doi:10.3389/fninf.2014.00008](https://doi.org/10.3389/fninf.2014.00008)
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Authors

Gabriele Amorosino

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
