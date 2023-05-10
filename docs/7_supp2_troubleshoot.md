# Supplementary. 2: Troubleshooting

!!! screwdriver-wrench "1. `RuntimeError: Resource exhausted: Out of memory`"

    - If you are to encounter the message "RuntimeError: Resource exhausted: Out of memory" , add the following variables to the slurm script
    - For module based runs  ( version `2.3.2` and above)
      ```bash
      export TF_FORCE_UNIFIED_MEMORY=1
      export XLA_PYTHON_CLIENT_MEM_FRACTION=4.0
      ```
    - For Singularity container based runs 
     ```bash
     export SINGULARITYENV_TF_FORCE_UNIFIED_MEMORY=1 
     export SINGULARITYENV_XLA_PYTHON_CLIENT_MEM_FRACTION=4.0
     ```