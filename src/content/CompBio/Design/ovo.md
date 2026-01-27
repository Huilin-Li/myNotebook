# OVO

## install
- https://ovo.dichlab.org/docs/user_guide/installation.html

1. `conda create --name myovo python=3.13`
2. `conda activate myovo`
3. `python --version` (Python 3.13 recommended, at least 3.10)
4. `java -version` Java (OpenJDK 21-24 recommended, at least 17)
> module load jdk/18.0.1.1
5. `pip install ovo`
6. `ovo init home`
<center>
  <figure>
    <img src=".\bioIMG\ovo1.PNG" alt=" " width="700">
    <figcaption>ovo init home</figcaption>
  </figure>
</center>


7. `source /home/shenhuaizhongLab/lihuilin/.bashrc` # load env variables
8. `conda deactivate`
9. `conda activate myovo` # re-activate this environment
10. `conda install -c bioconda nextflow`
```
(myovo) [lihuilin@login02 ~]$ nextflow -version

      N E X T F L O W
      version 25.10.2 build 10555
      created 28-11-2025 19:24 UTC (29-11-2025 03:24 CDT)
      cite doi:10.1038/nbt.3820
      http://nextflow.io

```
11. `ovo init preview`
<center>
  <figure>
    <img src=".\bioIMG\ovo2.PNG" alt=" " width="700">
    <figcaption>ovo init preview</figcaption>
  </figure>
</center>


<div class="warning">

**Download RFdiffusion model checkpoint files:**

In practice, due to the network constraints on HPC, it will be much faster to download these files locally, and then transfer them to the correct folder on HPC. (e.g. /storage/shenhuaizhongLab/lihuilin/ovo/reference_files/rfdiffusion_models)

</div>

12. 
<div class="warning">

**Process requirement exceeds available CPUs -- req: 4; avail: 1**

`ovo init preview` needs internecr accession and CPUs\\(\ge\\)4

</div>



12. 

10. `srun -p intel-sc3 -c 4 --mem=10G --pty bash` 
> Process requirement exceeds available CPUs -- req: 4; avail: 1
11. `mkdir -p /storage/shenhuaizhongLab/lihuilin/ovo/workdir/work/conda/env-fa85553f425440ecd8f4fdc763417c2f/lib/python3.11/site-packages/RFdiffusion`
> folder name must be RFdiffusion
12. `cd /storage/shenhuaizhongLab/lihuilin/ovo/workdir/work/conda/env-fa85553f425440ecd8f4fdc763417c2f/lib/python3.11/site-packages/RFdiffusion`
13. `git clone --depth 1 https://github.com/prihoda/RFdiffusion-fork`
14. `/storage/shenhuaizhongLab/lihuilin/ovo/workdir/work/conda/env-fa85553f425440ecd8f4fdc763417c2f/bin/python -m pip install biopandas`
15. `/storage/shenhuaizhongLab/lihuilin/ovo/workdir/work/conda/env-fa85553f425440ecd8f4fdc763417c2f/bin/python -m pip install torch`
16. `/storage/shenhuaizhongLab/lihuilin/ovo/workdir/work/conda/env-fa85553f425440ecd8f4fdc763417c2f/bin/python -m pip install omegaconf`
17. `/storage/shenhuaizhongLab/lihuilin/ovo/workdir/work/conda/env-fa85553f425440ecd8f4fdc763417c2f/bin/python -m pip install hydra-core`
18. `/storage/shenhuaizhongLab/lihuilin/ovo/workdir/work/conda/env-fa85553f425440ecd8f4fdc763417c2f/bin/python -m pip install scipy`
19. `/storage/shenhuaizhongLab/lihuilin/ovo/workdir/work/conda/env-fa85553f425440ecd8f4fdc763417c2f/bin/python -m pip install opt_einsum`
20. `/storage/shenhuaizhongLab/lihuilin/ovo/workdir/work/conda/env-fa85553f425440ecd8f4fdc763417c2f/bin/python -m pip install dgl`




