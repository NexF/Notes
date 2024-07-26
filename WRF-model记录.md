# WRF-model记录

## WRF&WPS代码下载

https://github.com/wrf-model/WRF/releases
https://github.com/wrf-model/WPS/releases

用户指南
https://www2.mmm.ucar.edu/wrf/users/wrf_users_guide/build/html/overview.html

## 环境安装
```
sudo yum install netcdf-devel


sudo yum install mpich-devel
sudo yum install zlib-devel
sudo yum install libpng-devel
sudo yum install jasper-devel

export DIR=~/src/WRF/library/bin
export CC=gcc
export CXX=g++
export FC=gfortran
export FCFLAGS=-m64
export F77=gfortran
export FFLAGS=-m64
export NCDIR=/usr
export NFDIR=/usr
export LD_LIBRARY_PATH=${NCDIR}/lib64:${LD_LIBRARY_PATH}
CPPFLAGS=-I${NCDIR}/include LDFLAGS=-L${NCDIR}/lib ./configure --prefix=${NFDIR}


export NETCDF=/usr
export HDF5=/usr
export JASPERLIB=/usr/lib64
export JASPERINC=/usr/include

```

## 环境安装
参考https://www2.mmm.ucar.edu/wrf/OnLineTutorial/compilation_tutorial.php
```
sudo yum install gcc-gfortran   # gnu编译器在4.6以上

# 设置编译时的环境变量
export DIR=~/src/WRF/library/bin
export CC=gcc
export CXX=g++
export FC=gfortran
export FCFLAGS=-m64
export F77=gfortran
export FFLAGS=-m64
export JASPERLIB=$DIR/grib2/lib
export JASPERINC=$DIR/grib2/include
export LDFLAGS=-L$DIR/grib2/lib
export CPPFLAGS=-I$DIR/grib2/include

export PATH=/usr/bin:$PATH
export NETCDF=/usr
export LIBS="-lnetcdf -lz"
# 检测zlib是否安装
rpm -qa | grep zlib

# 安装hdf5
./configure --prefix=$DIR/hdf5
make
make install
export PATH=$DIR/hdf5/bin:$PATH
export HDF5=$DIR/hdf5
export LD_LIBRARY_PATH=$DIR/hdf5/lib:$LD_LIBRARY_PATH

# 安装netcdf-c
cd netcdf-c-4.7.2
export CPPFLAGS=-I${HDF5}/include
export LDFLAGS=-L${HDF5}/lib
./configure --prefix=$DIR/netcdf --disable-dap  --disable-netcdf-4 --disable-shared
make
make install

export PATH=$DIR/netcdf/bin:$PATH
export NETCDF=$DIR/netcdf
export LIBS="-lnetcdf -lz"

# 安装netcdf-fortran
cd netcdf-fortran-4.5.2
export CPPFLAGS="-I$DIR/netcdf/include -I${HDF5}/include"
export LDFLAGS="-L$DIR/netcdf/lib -L${HDF5}/lib"
./configure --prefix=$DIR/netcdf --disable-dap  --disable-netcdf-4 --disable-shared

# 安装mpich
cd mpich-3.0.4
./configure --prefix=$DIR/mpich
make
make install
export PATH=$DIR/mpich/bin:$PATH

# 安装zlib
cd zlib-1.2.7
./configure --prefix=$DIR/grib2
make
make install

cd libpng-1.2.50
./configure --prefix=$DIR/grib2
make
make install

cd jasper-1.900.1
./configure --prefix=$DIR/grib2
make
make install
```