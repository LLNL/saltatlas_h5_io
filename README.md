# Getting Started (on LC)

## Install HDF5

```bash
module load gcc/8.3.1
spack compiler add
# Install HDF5 v1.10.7 with C++ support using GCC v8.3.1
spack install hdf5@1.10.7%gcc@8.3.1+cxx
```

## Build

There are two ways to build this program.
They vary in the way of telling CMake the location of HDF5.

### Common instruction
First, here are the common instructions:

```bash
module load gcc/8.3.1

# In a directory of this repository
mkdir build
cd build
```

### 1. Use spack load

Note that this one may not work.
I haven't investigated fully why `spack load` does not work properly sometimes;
however, here is my guess.

If you call `spack load hdf5`, the paths of the libraries which HDF5 depends on
are also put into `CMAKE_PREFIX_PATH`.
If you don't want to use the version installed by Spack, that will be an issue.
For example, an MPI is installed along with HDF5.
If you want to use an MPI installed in another location, it might be better to
avoid using `spack load`.

```bash
spack load hdf5@1.10.7%gcc@8.3.1+cxx
cmake ../
make
```

### 2. Use CMAKE_PREFIX_PATH

```bash
# Get the path to an installed HDF5
spack find --path hdf5

export CMAKE_PREFIX_PATH=/path/to/hdf5:${CMAKE_PREFIX_PATH}

cmake ../
make
```

# License
saltatlas_h5_io is distributed under the MIT license.

All new contributions must be made under the MIT license.

See [LICENSE-MIT](LICENSE-MIT), [NOTICE](NOTICE), and [COPYRIGHT](COPYRIGHT) for
details.

SPDX-License-Identifier: MIT

# Release
LLNL-CODE-833039
