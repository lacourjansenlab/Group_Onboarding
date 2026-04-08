# Tutorial to run ORCA on Habrok

You are assumed to have knowledge about quantum chemistry from courses in your programme.
This tutorial shows how you can run an ORCA calculation on Habrok. Before you can do this you need to obtain a free academic
license at the [ORCA website](https://www.faccts.de/orca/). More information of how to submit the license is given when you try
to load the module on habrok.

```bash!
module load ORCA
```

If you already have an active ORCA license  this will activate the ORCA module.

It is wise to collect all your ORCA calculations in one central place. Make a folder for this in your `/scratch/$USER` folder.

Now we want to do a simple calculation on the water molecule. First create a file telling ORCA what to do. You can best name
`water_geo.inp`.

```bash!
#Ground state geometry optimization

! RPBE RIJCOSX def2-TZVPP VeryTightSCF VeryTightOpt
%pal nprocs 8 end

* xyzfile 0 1 Water.xyz
```

This will tell ORCA to do a geometry optimization of the water molecule using the structure given in the file `water.xyz` as
starting point. We will need to create that. ORCA will here use the RPBE exchange correlation functional, the def2-TZVPP
basis set and have strict optimization criteria for the geometry and the self consistent field (SCF) calculation. The
calculation will be running in parallel on 8 CPUs (overkill for this small molecule, but you will like to use this later).

We can make a file with the initial structure of water. Name it `water.xyz`. The coordinates below are probably a bad guess.
You can make better starting structures with freely available programs as [Avogadro](https://avogadro.cc/index.html)
and store them as 'xyz' files as this one.
```bash!
3
Coordinates of water
  O -0.1 0.0 0.0
  H 0.5 0.0 -0.7
  H 0.5 0.0  0.7
```
We now need a script for Habrok to know how to do this calculation. You can name it `script_geo`.
```bash!
#!/bin/bash
#SBATCH --job-name "Orca_on_Water"
#SBATCH --ntasks=8
#SBATCH --nodes=1
#SBATCH --mem=50000
#SBATCH --time=0-01:00:00

module load ORCA/5.0.4-gompi-2022a
export ORCABIN=/apps/versions/2023.01/rocky8/x86_64/generic/software/ORCA/5.0.4-gompi-2022a/bin/

cd $TMPDIR
cp $SLURM_SUBMIT_DIR/water.xyz .
cp $SLURM_SUBMIT_DIR/water_geo.inp .

$ORCABIN/orca water_geo.inp > $SLURM_SUBMIT_DIR/water_geo.out

cp $TMPDIR/water_geo.xyz $SLURM_SUBMIT_DIR
```
Here we ask to use 8 CPUs (ntasks) through the queueing system and we reserve them for a max of 1 hour (time). We here
ask to use ORCA version 5.0.4. You may need to update this if you want to use a never version. With `module spider ORCA` you
can check which versions are available. If you change the version you also need to update the ORCABIN. This is the location
where ORCA is installed on the cluser. If you load the ORCA module of your choice you can find the location of this by
typing `which orca` on the commandline, which in the example above would display 
'/apps/versions/2023.01/rocky8/x86_64/generic/software/ORCA/5.0.4-gompi-2022a/bin/orca' on your screen. You would have to copy
everything but the final `orca` to the `export ORCABIN=` line in the script.

ORCA often generate numerous temporary files when running a calculation. We therefore like to do the calculation in a
temporary directory. We are assigned one by the SLURM queing system in the variable `$TMPDIR`. As the calculation will start
the script changes to this directory and copies the input files from the directory where we submitted out job. That
directory name is stored in the variable `$SLURM_SUBMIT_DIR` by SLURM.

The line calling orca will run the calculation and generate the output in a file in the directory from where we submitted the
SLURM job. At the end of the calculation orca will have generated various filed on the temporary directory. We want to copy
the final geometry back to our submission folder. You may add a `ls` command to check what other files are generated.
It is not recommended to copy all files back with a `cp *` command as if ORCA crashes you may end up copying a lot of large
temporary files that fills your available disk space.

To submit the script type: `sbatch script_geo`. The job is now likely waiting in the queue on habrok until the requested
CPUs are available to your job. You can check the status of all your jobs with the command `queue -u $USER`. This will
show your jobs that are running or waiting in the queue. If the job is not listed there anymore it either finished correctly
or crashed. You can check this with the `ls -lastr` command, which will list all files in the order that they were last 
changed.

If your job finished you should have the new optimized geometry in the `water_geo.xyz` file. The file `water_geo.out` will
tell you all about the details of how the calculation went. You can also find useful information as the final energy and
the dipole moment of the water molecule. The energy is propable close to -75.9 Hartree and the dipole moment close to 0.83
Debye.
