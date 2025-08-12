## Platform R

Computing platform for UW-Madison SMPH.

- getting started documentation at
  <https://kb.wisc.edu/smph/informatics/internal/149361>

- other documentation at
  <https://kb.wisc.edu/smph/informatics/internal/search.php?q=&cat=14788>

- log in at <https://windows365.microsoft.com/ent#/devices>

- Use PuTTY to connect to cluster, with host:
  `slurm.platformr.wisc.edu`
  and port: 22

- spack shared environment

  ```
  spack env create r /mnt/scratch/shared/software/environments/r-4_4_0/spack.yaml
  spacktivate r
  spack install
  ```

- learn about spack environment

  ```
  spack config get
  spack find
  spack spec
  ```

- add packages to spack environment

  ```
  spacktivate r
  spack list
  spack list r-qtl
  spack add r-qtl
  spack install
  ```

- access data on restricted drive

  ```
  ls -ll /mnt/restricteddrive/broman
  rsync -av --progress /mnt/restricteddrive/broman/mydir /mnt/scratch/group/broman/
  ```

- copy data back to restricted drive

  ```
  rsync -av --progress /mnt/scratch/group/broman/mydir /mnt/restricteddrive/broman/processed
  ```

- using [slurm](https://slurm.schedmd.com/man_index.html) for job management

  ```
  sinfo
  srun --cpus-per-task=32 --mem=256G --pty my_script.sh
  sbatch --cpus-per-task=32 --mem=256G my_script.sh
  scancel job#
  nvidia-smi
  squeue -u broman
  ```


---

- packages found: r-qtl, r-here

- packages needed to be installed:
broman,
lineup,
lineup2,
mbmixture,
mmconvert,
qtl2,
qtl2convert,
qtl2fst,
regress,
simcross,
xoi

- seems like I just install them directly with `install.packages()`
