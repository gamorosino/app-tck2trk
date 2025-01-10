# TCK to TRK Converter

This application converts tractography files from the `.tck` format to the `.trk` format. It uses a reference anatomy image in NIfTI format to ensure proper alignment.

## Features
- Input: `.tck` tractography file(s) and a reference anatomy image (`.nii` or `.nii.gz`).
- Output: Corresponding `.trk` tractography file(s).
- Skips non-TCK files and optionally overwrites existing TRK files.
- Supports multiple tractography files in a single execution.

## Author
Gabriele Amorosino (gabriele.amorosino@utexas.edu)

## Usage

### Running on Brainlife.io

You can run this app on the Brainlife.io platform, which provides cloud computing resources for neuroimaging workflows. Both inputs and outputs are managed directly on the Brainlife.io platform.

#### On Brainlife.io via UI
1. Navigate to the Brainlife.io platform.
2. Locate the TCK to TRK Converter app in the Apps section.
3. Click the "Execute" tab and specify the required dataset inputs (an anatomy NIfTI file and one or more TCK tractography files).
4. Submit the job and wait for the results.

#### On Brainlife.io using CLI
1. Install the Brainlife CLI by following the instructions at [Brainlife CLI Installation](https://brainlife.io/cli).
2. Log in to the CLI with your Brainlife.io credentials:
   ```bash
   bl login
   ```
3. Run the app with the following command:
   ```bash
   bl app run --id <app_id> --project <project_id> --input t1w:<t1w_object_id> --input tck:<tck_object_id>
   ```
   Replace `<app_id>`, `<project_id>`, `<t1w_object_id>`, and `<tck_object_id>` with the appropriate identifiers.

### Running Locally (on your machine)

#### Option 1: Using Python Directly

##### Prerequisites
- Python installed on your system.
- Required Python libraries: `nibabel`, `argparse`.
  Install them using pip:
  ```bash
  pip install nibabel argparse
  ```

##### Clone the Repository
Clone the repository to your local machine:
```bash
git clone https://github.com/gamorosino/app-trc2trk
cd app-trc2trk
```

##### Command-line Usage
Run the script using the following command:
```bash
python tck2trk.py <anatomy_image.nii> <tractogram1.tck> [<tractogram2.tck> ...]
```

###### Options
- `-f`, `--force`: Overwrite existing TRK files.

##### Example
```bash
python tck2trk.py anatomy.nii.gz tract1.tck tract2.tck -f
```

This will:
1. Load the anatomy reference (`anatomy.nii.gz`).
2. Convert `tract1.tck` and `tract2.tck` into `tract1.trk` and `tract2.trk`, overwriting existing TRK files if any.

#### Option 2: Using Singularity

##### Prerequisites
- Singularity installed and accessible.

##### Steps
1. Clone the repository:
   ```bash
   git clone https://github.com/gamorosino/app-trc2trk
   cd app-trc2trk
   ```

2. Create a `config.json` file in the repository directory, specifying the required input paths. Example:
   ```json
   {
       "tck": "/path/to/tract.tck",
       "t1w": "/path/to/t1w.nii.gz"
   }
   ```

3. Run the script:
   ```bash
   ./main
   ```

This will:
- Use the Singularity container to execute the script and convert the TCK file to a TRK file.

## Requirements

### For Python Usage
- Python 3.6+
- Libraries:
  - `nibabel`
  - `argparse`

Install dependencies with:
```bash
pip install -r requirements.txt
```

### For Singularity Usage
- Singularity installed and accessible.

## Outputs
The converted TRK files are saved in the same directory as the input TCK files, with the same filename but a `.trk` extension.

## Notes
- Non-TCK files are skipped automatically.
- Use the `-f` flag to overwrite output files if they already exist.

## Acknowledgments
This script was created to streamline the conversion of tractography files while ensuring alignment with reference anatomical images.
