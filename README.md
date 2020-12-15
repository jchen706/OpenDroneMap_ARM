# OpenDroneMap_ARM

How to compile and run OpenDroneMap on ARM Processor:

- sudo apt-get install sqlite3 
- sudo apt-get install libsqlite3-dev
- sudo apt-get install libssl-dev - (for openssl)
- sudo apt-get install libpcl-dev libpdal-dev
- sudo apt-get install libxml2 libxslt 
- sudo apt-get install cython


- Install Proj 6.1.1 from sudo wget https://download.osgeo.org/proj/proj-6.1.1.tar.gz (follow the install guidelines)

- Ln -s /usr/local/lib/libproj.so.15 /usr/lib/ (fix error for pyproj)

## Install the Require Python Libraries (make sure check the python and numpy version are compatiable and check for new requirements from OpenDroneMap )

- PyYAML==3.13
- ExifRead==2.3.0
- cloudpickle==1.2.2
- pytz==2020.1
- gpxpy==1.3.5
- xmltodict==0.12.0
- appsettings==0.8
- loky==2.5.1
- repoze.lru==0.7
- rasterio==1.0.28
- attrs==19.1.0
- pyodm==1.5.4
- Pillow==6.1.0
- networkx==2.2
- scipy==1.2.1
- Pysolar==0.6
- psutil==5.6.3
- joblib==0.13.2
- Fiona==1.8.9.post2
- cryptography==2.8
- pyOpenSSL==19.1.0
- scikit-learn==0.20
- laspy==1.6.0
- lxml==4.5.1
- pyproj==2.2.2
- beautifulsoup4
- numpy
- scipy

## Next Steps:


### Run into bin not file directory error in Superbuild/install/bin

Fix: Go to Superbuild/install and remove the bin and add bin as (mkdir bin)

### Disable Math Optimization for x86, you can use ARM_NEON.h for ARM Math Optimizations

- For nearest neighbor , disable SSE2 and SSE3 instruction set for x86 . comment out the lines 
- Nearest_neighbor.h  set define search sse2 to 0 and sse3 to 0

File paths:

- ODM/SuperBuild/src/mvstexturing/elibs/mve/libs/sfm/nearest_neighbor.h
- ODM/SuperBuild/src/elibs/mve/libs/sfm/nearest_neighbor.h
- In mvstexturing folder in Superbuild (ODM/SuperBuild/src/mvstexturing), in the CMakeList.txt Line 32 comment out -mfpmath=sse. 

#### Comment out line openmvs_exporter.h  in csfm.cc line 7 and the py::class OpenMVSExporter in the csfm.cc file 

- This was a import error by compiler. Double import.

#### Copy the the newest Interface.h from OpenMvs Github Library to Interface.h.

- File path = ODM/SuperBuild/src/opensfm/opensfm/src/third_party/openmvs/Interface.h

### Image_io.cc Error for tiff and jpeg exception handing 

Files paths: 

- ODM/SuperBuild/src/mvstexturing/elibs/mve/libs/mve/image_io.cc
- ODM/SuperBuild/src/elibs/mve/libs/mve/image_io.cc

#### Fix: https://stackoverflow.com/questions/19857766/error-handling-in-libjpeg

- Edit image_io.cc for tiff and jpeg error exit handlers 
- I put the file in this repository

- cd /Superbuild 
- mkdir build 
- sudo cmake ..

# Last

- cd /ODM/build
- cmake ..
- sudo make






