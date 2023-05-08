# Visualisation


!!! jupyter "jupyter"

    - Please use Mahuika JupyterHub for Visualisation component. JupyterHub can be accessed via https://jupyter.nesi.org.nz/hub/login


## Visualisation Script

We provide a python script (`visualize_alphafold_results.py`) created by [VIB Belgium](https://elearning.bits.vib.be/courses/alphafold/lessons/alphafold-on-the-hpc/topic/alphafold-outputs/) to extract pLDDT, PAE and MSA visualizations (inspired by ColabFold code). 

!!! quote ""

    - This script is incorporated into `pymol-open-source/2.5.0` module The script uses the contents of the `.pkl` output files from the AlphaFold run. It takes three parameters in input:
    - `--input_dir` The location where the AlphaFold output files were stored.
    - `--output_dir` (optional) The location where the images that are generated should be stored. By default, they are stored in the input directory.
    - `--name` (optional) The prefix that will be used in for the filenames of the generated files. By default, no prefix is added.
    To run the script, you will also have the correct python modules loaded. You can do this by running the following lines before running the actual script.