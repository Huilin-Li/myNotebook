# localcolabfold usage (history)


### slurm scripts

```
#!/bin/bash
#SBATCH -q gpu-huge
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=8
#SBATCH -p a40-tmp
#SBATCH --gres=gpu:1
#SBATCH --mem=50G
#SBATCH -J array-job					
#SBATCH -a 1-2
#SBATCH -o xxx.%A.%a.log



module load cuda/12.0
module load gcc/9.4.0

source ~/miniconda3/etc/profile.d/conda.sh
conda activate /(...)/lihuilin/mycolabfold/localcolabfold/colabfold-conda

cd /(...)/lihuilin/mycolabfold/mypredictions/xxx_remain

id_list="./names.txt"
id=`head -n $SLURM_ARRAY_TASK_ID $id_list | tail -n 1`


fafile=$id".fa"
outdir=$id"_out"
colabfold_batch $fafile $outdir --num-relax 1

```


```
#!/bin/bash
#SBATCH -q gpu-huge
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=8
#SBATCH -p a40-tmp
#SBATCH --gres=gpu:1 
#SBATCH --mem=50G


module load cuda/12.0
module load gcc/9.4.0

source ~/miniconda3/etc/profile.d/conda.sh
conda activate /(...)/lihuilin/mycolabfold/localcolabfold/colabfold-conda


for fa in myfa1 myfa2 myfa3 myfa4
do
    echo "start "$fa"predict"
    cd /(...)/lihuilin/mycolabfold/mypredictions/yyyfastas
    fafile=$fa".fa"
    outdir=$fa"_out"
    colabfold_batch $fafile $outdir --num-relax 3
    echo "end "$fa"predict"
done


```


```
#!/bin/bash
#SBATCH -q gpu-huge
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=8
#SBATCH -p a40-tmp
#SBATCH --gres=gpu:1 
#SBATCH --mem=50G


module load cuda/12.0
module load gcc/9.4.0

source ~/miniconda3/etc/profile.d/conda.sh
conda activate /(...)/lihuilin/mycolabfold/localcolabfold/colabfold-conda




cd /(...)/lihuilin/mycolabfold/mypredictions/aaa_remain


colabfold_batch myfa2.fa myfa2_out --num-relax 1


```

### msa only shell script

```
#!/bin/bash

source ~/miniconda3/etc/profile.d/conda.sh
conda activate /(...)/lihuilin/mycolabfold/localcolabfold/colabfold-conda

module load cuda/12.0


for fa in myfa0 myfa1 myfa2
do
    echo "start "$fa
    cd /(...)/lihuilin/mycolabfold/mypredictions/myfastas
    fafile=$fa".fa"
    outdir=$fa"_out"
    colabfold_batch $fafile $outdir --msa-only
    echo "end "$fa
done

```