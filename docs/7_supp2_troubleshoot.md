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

!!! screwdriver-wrench "2. `ValueError: Invalid character in the sequence: n`"
    
    This will get triggered in the event where an input file doesn't obey the following conditions

      - AlphaFold expects an input query sequence with capitalized one-letter amino-acid types from this set:
  
      ```
       'A', 'R', 'N', 'D', 'C', 'Q', 'E', 'G', 'H', 'I', 'L', 'K', 'M', 'F', 'P', 
       'S', 'T', 'W', 'Y', 'V' 
      ```
      
      - For `monomer` runs: Input file for the AlphaFold system should only contain one protein.