# AlphaFold2 Databases

AlphaFold databases are stored in */opt/nesi/db/alphafold_db/*  parent directory. In order to make the database calling more convenient, we have prepared modules for each version of the database. Running `module spider AlphaFold2DB` will list the available versions named after the downladed Year and Month (Year-Month)

!!! terminal "terminal"
    ```bash
    $ module spider AlphaFold2DB

    ---------------------------------------------
      AlphaFold2DB:
    ---------------------------------------------
        Description:
          AlphaFold2 databases
    
         Versions:
            AlphaFold2DB/2022-06
            AlphaFold2DB/2023-04

    ```
Loading a module will set the `$AF2DB` environment variable which is pointing to the  selected version of the database. For an example. 

!!! terminal "terminal"
    ```bash
    $ module load AlphaFold2DB/2023-04
    
    $ echo $AF2DB 
    /opt/nesi/db/alphafold_db/2023-04
    ```