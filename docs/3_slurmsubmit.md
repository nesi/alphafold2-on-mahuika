# Slurm submission scripts

!!! circle-info "Information on versions"
    
    - Following instructions are for AlphaFold >= 2.3.2.
    - If you are after an older version, refer to [these page](https://support.nesi.org.nz/hc/en-gb/articles/4405170961039-AlphaFold#alphafold_singularity_container_(prior_to_v2.3.2)) which the instruction on how to deploy it via Singularity/Apptainer containers 


!!! folder-open "Directory structure (recommended)"
    
    - Use nobackup filesystem at all times
    - We recommend storing input .fasta files , corresponding outputs and slurm logs in three separate directories

    <center>![image](./nesi_images/directory_structure.png){width="260"}</center>

## `monomer`
### **Slurm script for a single query file**  


!!! terminal "terminal"
    ```bash
    #!/bin/bash -e
    
    #SBATCH --account       nesi12345
    #SBATCH --job-name      af-test
    #SBATCH --mem           24G
    #SBATCH --cpus-per-task 6
    #SBATCH --gpus-per-node A100:1
    #SBATCH --time          03:00:00
    #SBATCH --output        /nesi/nobackup/nesi12345/slurmlog/%j.out
    
    module purge
    module load AlphaFold2DB/2023-04
    module load AlphaFold/2.3.2
    
    INPUT_PATH=/nesi/nobackup/nesi12345/input
    OUTPUT=/nesi/nobackup/nesi12345/output
    
    run_alphafold.py --use_gpu_relax \
    --data_dir=$AF2DB \
    --uniref90_database_path=$AF2DB/uniref90/uniref90.fasta \
    --mgnify_database_path=$AF2DB/mgnify/mgy_clusters_2022_05.fa \
    --bfd_database_path=$AF2DB/bfd/bfd_metaclust_clu_complete_id30_c90_final_seq.sorted_opt \
    --uniref30_database_path=$AF2DB/uniref30/UniRef30_2021_03 \
    --pdb70_database_path=$AF2DB/pdb70/pdb70 \
    --template_mmcif_dir=$AF2DB/pdb_mmcif/mmcif_files \
    --obsolete_pdbs_path=$AF2DB/pdb_mmcif/obsolete.dat \
    --model_preset=monomer \
    --max_template_date=2022-6-1 \
    --db_preset=full_dbs \
    --output_dir=${OUTPUT} \
    --fasta_paths=${INPUT_PATH}/filename.fasta
    ```

### **Slurm array for multiple queries**

!!! terminal "code"
    ```bash
    #!/bin/bash -e
    
    #SBATCH --account       nesi12345
    #SBATCH --job-name      af--array_test
    #SBATCH --mem           24G
    #SBATCH --cpus-per-task 6
    #SBATCH --gpus-per-node A100:1
    #SBATCH --array         0-5
    #SBATCH --time          4:00:00
    #SBATCH --output        /nesi/nobackup/nesi12345/slurmlog/%A.%a.out
    
    module purge
    module load AlphaFold2DB/2023-04
    module load AlphaFold/2.3.2
    
    INPUT_PATH=/nesi/nobackup/nesi12345/input
    OUTPUT=/nesi/nobackup/nesi12345/output
    
    INPUT_FASTA=($INPUT_PATH/*.fasta)
    INPUT_NAMES=$(basename ${INPUT_FASTA[SLURM_ARRAY_TASK_ID]%.*})
    
    run_alphafold.py --use_gpu_relax \
    --data_dir=$AF2DB \
    --uniref90_database_path=$AF2DB/uniref90/uniref90.fasta \
    --mgnify_database_path=$AF2DB/mgnify/mgy_clusters_2022_05.fa \
    --bfd_database_path=$AF2DB/bfd/bfd_metaclust_clu_complete_id30_c90_final_seq.sorted_opt \
    --uniref30_database_path=$AF2DB/uniref30/UniRef30_2021_03 \
    --pdb70_database_path=$AF2DB/pdb70/pdb70 \
    --template_mmcif_dir=$AF2DB/pdb_mmcif/mmcif_files \
    --obsolete_pdbs_path=$AF2DB/pdb_mmcif/obsolete.dat \
    --model_preset=monomer \
    --max_template_date=2022-6-1 \
    --db_preset=full_dbs \
    --output_dir=${OUTPUT}/${INPUT_NAMES} \
    --fasta_paths=${INPUT_PATH}/${INPUT_NAMES}.fasta
    ```