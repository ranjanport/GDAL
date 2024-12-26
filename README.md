# GDAL : Geospatial library wheels for Python on Linux/Mac (ARM & AMD)
This repository contains the build of GDAL : Wheel Files

## Build Instructions

### Build Requirements Installations
```bash
apt install libtiff5 libtiff-dev curl wget sqlite3 sqlite build-essential libsqlite3-dev libcurl4-openssl-dev python3.11-dev swig doxygen expat zlib1g-dev zlib1g libgeotiff-dev libpng-dev libjpeg-dev libpq-dev libfreexl-dev libspatialite-dev libwebp-dev libhdf5-dev libffi-dev  libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libbz2-dev python3.11-lib2to3  python3.11-distutils -y
```
```bash
apt-get install proj-bin -y
```

### Install CMAKE Build Tool
``` bash 
wget https://github.com/Kitware/CMake/releases/download/v3.29.0/cmake-3.29.0-linux-x86_64.sh && mv cmake-3.29.0-linux-x86_64.sh /usr && cd /usr && sh cmake-3.29.0-linux-x86_64.sh
```

### Install Python Specific Version Dependencies (Python 3.1*)
#### Adding PIP (Replace the * with version)
``` bash
curl -sS https://bootstrap.pypa.io/get-pip.py | python3.1*
```

```python
 pip install numpy
 ```

### Install PROJ Library with all the requirement & Dependencies
```bash
VERSION_PROJLIB=9.5.0
wget https://download.osgeo.org/proj/proj-${VERSION_PROJLIB}.tar.gz
tar -xf proj-${VERSION_PROJLIB}.tar.gz
cd  proj-${VERSION_PROJLIB}
mkdir build
cd build
cmake ..
cmake --build .
cmake --build . --target install
projsync --system-directory --all
```

### Install GDAL Library with all the requirement & Dependencies
```bash
VERSION=3.9.3
wget https://github.com/OSGeo/gdal/releases/download/v${VERSION}/gdal-${VERSION}.tar.gz
tar -xf gdal-${VERSION}.tar.gz
cd gdal-{VERSION}
mkdir build
cd build
cmake .. -DCMAKE_BUILD_TYPE=Release -Donnxruntime_ENABLE_PYTHON=ON -DPYTHON_EXECUTABLE=/usr/bin/python3.11 -Donnxruntime_BUILD_SHARED_LIB=ON -Donnxruntime_DEV_MODE=OFF -DPYTHON_INCLUDE_DIR=“/usr/include/python3.11” -DNUMPY_INCLUDE_DIR=“/usr/local/lib/python3.11/dist-packages/numpy/core/include/numpy”
cmake --build .
cmake --build . --target install
```

### Install GDAL Python Wheel
```python
pip install GDAL==${VERSION}
```

### Move the Wheel to the Artifactory as the Wheel files is build and stored in .cache of pip in the user directory
```bash
mv $USER/.cache/pip/path/to/whl/file ~/Downloads
```
