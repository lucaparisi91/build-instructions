## Boris installation instructions

You will first need to load all the dependencies, including openmpi, fftw and cuda.

```bash
module load gcc/10.2.0
module load fftw/3.3.10-gcc10.2-mpt2.25
module load python/3.11.5-gpu
module load oneapi
module load tbb/2022.0
```

Set a shell variable to identify the version and download the software

```bash
git clone https://github.com/SerbanL/BORIS.git
cd BORIS
```

You will need to modify the makefile, in order to build on Cirrus. You can copy the modified makefile in this folder into the root of the Boris2 source code.

```bash
cp makefile  BORIS
```

Finally you can compile the source using make. You will need to specify the root location of cuda and the root of the python environment.
Below an example corresponding do the modules loaded above on the 29th of May 2025.

```bash
cd BORIS
make configure arch=70 sprec=1 python=3.11 cuda=/work/y07/shared/cirrus-software/nvidia/hpcsdk-22.11/Linux_x86_64/22.11/cuda conda-env-path=/work/y07/shared/cirrus-software/miniconda3/23.11.0-2-py311-gpu
make compile -j 8
make install
```