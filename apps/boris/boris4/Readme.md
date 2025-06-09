## Boris installation instructions (29-05-25)

You will first need to load all the dependencies, including openmpi, fftw and cuda.

```bash
module load gcc/10.2.0
module load fftw/3.3.10-gcc10.2-mpt2.25
module load python/3.11.5-gpu
module load oneapi
module load tbb/2022.0
module load nvidia/nvhpc-nompi/22.11
```

You will need to modify the makefile, in order to build on Cirrus. You can find an adapted makefile in this folder. You will need to copy it to the code source directory.

```bash
cp makefile BorisLin_v4.0g21
```

Finally you can compile the source using make. You will need to specify the root location of cuda and the root of the python environment.
Below an example corresponding do the modules loaded above.

```bash
cd BorisLin_v4.0g21
make configure arch=70 sprec=1 python=3.11 cuda=/work/y07/shared/cirrus-software/nvidia/hpcsdk-22.11/Linux_x86_64/22.11/cuda/11.8/targets/x86_64-linux conda-env-path=/work/y07/shared/cirrus-software/miniconda3/23.11.0-2-py311-gpu
make compile -j 8
make install
```


# Running

Before running make sure to load all the modules above and 

```bash
export LD_LIBRARY_PATH=/work/y07/shared/cirrus-software/nvidia/hpcsdk-22.11/Linux_x86_64/22.11/cuda/11.8/lib64/stubs:$LD_LIBRARY_PATH
```

You can check that all libraries are loaded using ldd.
Example output below

```bash
cirrus-login3:BorisLin_v4.0g21$ ldd BorisLin 
        linux-vdso.so.1 (0x00007fffbd395000)
        libpython3.11.so.1.0 => /work/y07/shared/cirrus-software/miniconda3/23.11.0-2-py311-gpu/lib/libpython3.11.so.1.0 (0x00007f9e876b6000)
        libtbb.so.12 => /mnt/lustre/e1000/home/y07/shared/cirrus-software/oneapi/2025.0/tbb/2022.0/lib/libtbb.so.12 (0x00007f9e87432000)
        libX11.so.6 => /lib64/libX11.so.6 (0x00007f9e870ef000)
        libfftw3.so.3 => /work/y07/shared/cirrus-software/fftw/3.3.10-gcc10.2-mpt2.25/lib/libfftw3.so.3 (0x00007f9e86dc8000)
        libnvidia-ml.so.1 => /work/y07/shared/cirrus-software/nvidia/hpcsdk-22.11/Linux_x86_64/22.11/cuda/11.8/lib64/stubs/libnvidia-ml.so.1 (0x00007f9e86bbc000)
        libcudart.so.11.0 => /work/y07/shared/cirrus-software/nvidia/hpcsdk-22.11/Linux_x86_64/22.11/cuda/lib64/libcudart.so.11.0 (0x00007f9e86915000)
        libcufft.so.10 => /work/y07/shared/cirrus-software/nvidia/hpcsdk-22.11/Linux_x86_64/22.11/math_libs/lib64/libcufft.so.10 (0x00007f9e75a3a000)
        libstdc++.so.6 => /work/y07/shared/cirrus-software/gcc/10.2.0/lib64/libstdc++.so.6 (0x00007f9e75667000)
        libm.so.6 => /lib64/libm.so.6 (0x00007f9e752e5000)
        libmvec.so.1 => /lib64/libmvec.so.1 (0x00007f9e750ba000)
        libgomp.so.1 => /work/y07/shared/cirrus-software/gcc/10.2.0/lib64/libgomp.so.1 (0x00007f9e74e7b000)
        libgcc_s.so.1 => /work/y07/shared/cirrus-software/gcc/10.2.0/lib64/libgcc_s.so.1 (0x00007f9e74c63000)
        libpthread.so.0 => /lib64/libpthread.so.0 (0x00007f9e74a43000)
        libc.so.6 => /lib64/libc.so.6 (0x00007f9e7467e000)
        libdl.so.2 => /lib64/libdl.so.2 (0x00007f9e7447a000)
        libutil.so.1 => /lib64/libutil.so.1 (0x00007f9e74276000)
        /lib64/ld-linux-x86-64.so.2 (0x00007f9e87c7e000)
        libxcb.so.1 => /lib64/libxcb.so.1 (0x00007f9e7404d000)
        librt.so.1 => /lib64/librt.so.1 (0x00007f9e73e45000)
        libXau.so.6 => /lib64/libXau.so.6 (0x00007f9e73c41000)
```