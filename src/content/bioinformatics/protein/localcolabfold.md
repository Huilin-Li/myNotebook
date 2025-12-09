# localcolabfold usage (straightforward)
[localcolabfold](https://github.com/YoshitakaMo/localcolabfold) is [ColabFold](https://colab.research.google.com/github/sokrypton/ColabFold/blob/main/AlphaFold2.ipynb) for protein structure prediction on local PC.

## One protein prediction in command line
1. msa only 
```
conda activate /(...)/lihuilin/mycolabfold/localcolabfold/colabfold-conda

module load cuda/12.0

colabfold_batch fafile outdir --msa-only
```


2. GPU prediction
```
conda activate /(...)/lihuilin/mycolabfold/localcolabfold/colabfold-conda

module load cuda/12.0
module load gcc/9.4.0

colabfold_batch fafile outdir --num-relax 1
```

## Multiple proteins prediction in slurm scrpits
1. msa only: msaonly.sh
```
#!/bin/bash

source ~/miniconda3/etc/profile.d/conda.sh
conda activate /(...)/lihuilin/mycolabfold/localcolabfold/colabfold-conda

module load cuda/12.0

cd /(...)/fasta_files

INPUT_FILES=($(ls *.fasta))
INPUT=${INPUT_FILES[$SLURM_ARRAY_TASK_ID-1]}
OUTPUT="${INPUT%.*}_out"


colabfold_batch $INPUT $OUTPUT --msa-only

```
bash msaonly.sh

2. GPU prediction
```
#!/bin/bash
#SBATCH -q gpu-huge
#SBATCH --nodes=1
#SBATCH -p a100-40g
#SBATCH --gres=gpu:1
#SBATCH --mem=80G
#SBATCH -J JobName					
#SBATCH -a 1-4


module load cuda/12.0
module load gcc/9.4.0

source ~/miniconda3/etc/profile.d/conda.sh
conda activate /storage/(...)/lihuilin/mycolabfold/localcolabfold/colabfold-conda

cd /(...)/fasta_files

INPUT_FILES=($(ls *.fasta))
INPUT=${INPUT_FILES[$SLURM_ARRAY_TASK_ID-1]}
OUTPUT="${INPUT%.*}_out"


colabfold_batch $INPUT $OUTPUT --num-relax 1
```


