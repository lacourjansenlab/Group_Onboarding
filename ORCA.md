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

This will tell ORCA to do a geometry optimization of the water molecule using the structure given in the file `Water.xyz` as
starting point. We will need to create that. ORCA will here use the RPBE exchange correlation functional, the def2-TZVPP
basis set and have strict optimization criteria for the geometry and the self consistent field (SCF) calculation. The
calculation will be running in parallel on 8 CPUs (overkill for this small molecule, but you will like to use this later).

We can make a file with the initial structure of water. Name it `Water.xyz`. The coordinates below are probably a bad guess.
You can make better starting structures with freely available programs as 'Avogadro' and store them as 'xyz' files as this one.
```bash!
3
Coordinates of water
  O -0.1 0.0 0.0
  H 0.5 0.0 -0.7
  H 0.5 0.0  0.7
```
