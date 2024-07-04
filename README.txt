[The mpi version of the c and fortran compiler are required.]

To compile, for example, do the following:

mkdir build && cd build
cmake .. && make

To run, copy the executable file and the input data files (ssc_*dat, inluding the cross sections for the selected ion species) into some directory, edit the input data files as necessary (note that the input is formatted, so one has to follow patterns provided in corresponding description lines), then do for example:

mpirun -np 8 ./edipic1d.out > out.log &
or 
hohup mpirun -np 8 ./edipic1d.out > out.log 2>&1 &
