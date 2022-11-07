# Tricks at CERN

## CVMFS

Precompiled software is available in the read-only service `cvmfs`. Service can be installed during the installation of the operative system in case of CERN CentOS, or manually afterwards, installing the `locmap` packages and then enabling that service. Visit the [webpage](https://linux.web.cern.ch/centos7/docs/locmap/) for further details.

There are two software builds of softare, `LGC` and `spack`. There is a daily built of each one, named `nightlies`, and a stable release. Each release may have a hash or version number which identify the status of the software at that time. 

Individual packages can be sourced from both `LGC` and `spack`. Alternatively, all the packages (around 1500) can be sourced with the following command

```shell
source /cvmfs/sft.cern.ch/lcg/views/dev4/latest/x86_64-centos7-gcc11-opt/setup.sh
```

For example, this command sources the latest version of Geant4, ROOT, Qt, DD4hep, etc, for a machine `x86_64` with `centos7` compiled using `gcc11`.

Keep in mind that `cvmfs` service can be enabled in the main machine, and then use a singularity container with `centos7` to use those packages.

Software in `cvmfs` is compiled for a variety of environments (OS + compiler),

```shell
ls /cvmfs/sft.cern.ch/lcg/views/dev4/latest/
aarch64-centos7-gcc11-opt   x86_64-centos7-gcc7-opt
arm64-mac12-clang131-opt    x86_64-centos7-gcc8-dbg
arm64-mac12-clang140-opt    x86_64-centos7-gcc8-opt
x86_64-centos7-clang10-dbg  x86_64-centos7-gcc9-dbg
x86_64-centos7-clang10-opt  x86_64-centos7-gcc9-opt
x86_64-centos7-clang11-dbg  x86_64-centos8-gcc10-dbg
x86_64-centos7-clang11-opt  x86_64-centos8-gcc10-opt
x86_64-centos7-clang12-dbg  x86_64-centos8-gcc11-dbg
x86_64-centos7-clang12-opt  x86_64-centos8-gcc11-opt
x86_64-centos7-clang80-dbg  x86_64-centos9-gcc11-dbg
x86_64-centos7-clang80-opt  x86_64-centos9-gcc11-opt
x86_64-centos7-clang8-dbg   x86_64-centos9-gcc12-dbg
x86_64-centos7-clang8-opt   x86_64-centos9-gcc12-opt
x86_64-centos7-clang9-opt   x86_64-mac1015-clang120-opt
x86_64-centos7-gcc10-dbg    x86_64-mac11-clang120-opt
x86_64-centos7-gcc10fp-dbg  x86_64-slc6-gcc62-opt
x86_64-centos7-gcc10fp-opt  x86_64-slc6-gcc7-dbg
x86_64-centos7-gcc10-opt    x86_64-slc6-gcc7-opt
x86_64-centos7-gcc11-dbg    x86_64-slc6-gcc8-dbg
x86_64-centos7-gcc11-opt    x86_64-slc6-gcc8-opt
x86_64-centos7-gcc12-dbg    x86_64-ubuntu1804-gcc7-opt
x86_64-centos7-gcc12-opt    x86_64-ubuntu1804-gcc8-opt
x86_64-centos7-gcc62-opt    x86_64-ubuntu2004-gcc9-opt
x86_64-centos7-gcc7-dbg     x86_64-ubuntu2204-gcc11-opt
```

## CernVM

A virtual box with all the CERN appliances can be installed following the instructions [here](https://cernvm.cern.ch/fs/).

## Cern docker images

Docker images of CERN CentOS are available [here](https://linux.web.cern.ch/dockerimages/)