## Boris installation instructions (29-05-25)

You will first need to load all the dependencies, including openmpi, fftw and cuda.

```bash
module load gcc/10.2.0
module load fftw/3.3.10-gcc10.2-mpt2.25
module load python/3.11.5-gpu
module load oneapi
module load tbb/2022.0
```

Download the software from git and move in the code root directory.

```bash
git clone https://github.com/SerbanL/BORIS.git
```

You will need to modify the makefile, in order to build on Cirrus. You can find an adapted makefile in this folder. You will need to copy it to the code source directory.

```bash
cp makefile  BORIS
```

Finally you can compile the source using make. You will need to specify the root location of cuda and the root of the python environment.
Below an example corresponding do the modules loaded above.

```bash
cd BORIS
make configure arch=70 sprec=1 python=3.11 cuda=/work/y07/shared/cirrus-software/nvidia/hpcsdk-22.11/Linux_x86_64/22.11/cuda conda-env-path=/work/y07/shared/cirrus-software/miniconda3/23.11.0-2-py311-gpu
make compile -j 8
make install
```