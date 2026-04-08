Before running a F-2DES calculation on NISE, you'd need to have files containing
* your excitation energy transfer matrix (e.g. from MCFRET): _RateMatrix.dat_
* the transition dipole moments in binary: _Dipole.bin_
* the Hamiltonian trajectory in binary: _Energy.bin_
* a script for submitting your job: _submitFDCG_
* an input file containing specfications on your submission: _inputFDCG_
* two text files containing your 1 and 2 photon quantum yields: _Q1s.dat, Q2s.dat_

If you already have your window and doorway functions from a previous calculation, you can actually reduce the computation time by choosing `FD_CG_2DES_combine` as the Technique in your input file. Be sure to copy the following files into the folder where you will be running your calculation:
* windows_SE.dat
* windows_GB.dat
* windows_EA.dat
* doorway.dat

After running NISE, we would like to analize the resulting 2D spectral files, for this system specifically, we are interested in the parallel polarization data files _2D.par.dat_. This file consists of four columns. The first one being the excitation frequency $\omega_1$ and the second is the detection frequency $\omega_3$. In the third and fourth columns, we have the imaginary and the real parts of the signal, respectively. Here, we will be working with the real part only.