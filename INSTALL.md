## 1. Instalare server FaReS

### 1.1 Obtinere server

Serverul FaReS poate fi descarcat din sectiunea Releases a proiectului de pe GitHub. Documentatia se afla in arhiva, in directorul docs.


### 1.2 Instalare diverse pachete necesare pentru dezvoltare.
```bash
root@dev-04-ubuntu:~# apt-get update
root@dev-04-ubuntu:~# apt-get install python3-pip python3-dev python3-setuptools python3-flask
root@dev-04-ubuntu:~# apt-get install build-essential git cmake libssl-dev libffi-dev python3-dev

root@dev-04-ubuntu:~# gcc --version
gcc (Ubuntu 7.5.0-3ubuntu1~18.04) 7.5.0
Copyright (C) 2017 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

root@dev-04-ubuntu:~# make --version
GNU Make 4.1
Built for x86_64-pc-linux-gnu
Copyright (C) 1988-2014 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

root@dev-04-ubuntu:~# mkdir fares && cd fares
```


### 1.3 Compilare si instalare DLIB. Exista doua modalitati de a instala DLIB - cu si fara
accelerare GPU (NVIDIA CUDA).

Instalare DLIB **fara** suport GPU:
```bash
root@dev-04-ubuntu:~/fares# git clone https://github.com/davisking/dlib.git
root@dev-04-ubuntu:~/fares# cd dlib
root@dev-04-ubuntu:~/fares/dlib# mkdir build; cd build; cmake ..; cmake --build .
[...]
 *****************************************************************************
 *** No BLAS library found so using dlib's built in BLAS.  However, if you ***
 *** install an optimized BLAS such as OpenBLAS or the Intel MKL your code ***
 *** will run faster.  On Ubuntu you can install OpenBLAS by executing:    ***
 ***    sudo apt-get install libopenblas-dev liblapack-dev                 ***
 *** Or you can easily install OpenBLAS from source by downloading the     ***
 *** source tar file from http://www.openblas.net, extracting it, and      ***
 *** running:                                                              ***
 ***    make; sudo make install                                            ***
 *****************************************************************************
CUDA_TOOLKIT_ROOT_DIR not found or specified
-- Could NOT find CUDA (missing: CUDA_TOOLKIT_ROOT_DIR CUDA_NVCC_EXECUTABLE CUDA_INCLUDE_DIRS CUDA_CUDART_LIBRARY) (Required is at least version "7.5")
-- DID NOT FIND CUDA
-- Disabling CUDA support for dlib.  DLIB WILL NOT USE CUDA
-- C++11 activated.
-- Configuring done
-- Generating done
-- Build files have been written to: /root/fares/dlib/build
Scanning dependencies of target dlib
[  0%] Building CXX object dlib/CMakeFiles/dlib.dir/base64/base64_kernel_1.cpp.o
[  1%] Building CXX object dlib/CMakeFiles/dlib.dir/bigint/bigint_kernel_1.cpp.o
[  2%] Building CXX object dlib/CMakeFiles/dlib.dir/bigint/bigint_kernel_2.cpp.o
[  3%] Building CXX object dlib/CMakeFiles/dlib.dir/bit_stream/bit_stream_kernel_1.cpp.o
[  3%] Building CXX object dlib/CMakeFiles/dlib.dir/entropy_decoder/entropy_decoder_kernel_1.cpp.o
[  4%] Building CXX object dlib/CMakeFiles/dlib.dir/entropy_decoder/entropy_decoder_kernel_2.cpp.o
[  5%] Building CXX object dlib/CMakeFiles/dlib.dir/entropy_encoder/entropy_encoder_kernel_1.cpp.o
[...]
[ 95%] Building C object dlib/CMakeFiles/dlib.dir/external/libjpeg/jmemnobs.c.o
[ 96%] Building C object dlib/CMakeFiles/dlib.dir/external/libjpeg/jquant1.c.o
[ 96%] Building C object dlib/CMakeFiles/dlib.dir/external/libjpeg/jquant2.c.o
[ 97%] Building C object dlib/CMakeFiles/dlib.dir/external/libjpeg/jutils.c.o
[ 98%] Building CXX object dlib/CMakeFiles/dlib.dir/image_loader/jpeg_loader.cpp.o
[ 99%] Building CXX object dlib/CMakeFiles/dlib.dir/image_saver/save_jpeg.cpp.o
[100%] Linking CXX static library libdlib.a
[100%] Built target dlib

root@dev-04-ubuntu:~/fares/dlib/build# cd ..
root@dev-04-ubuntu:~/fares/dlib# python3 setup.py install
[...]
 *****************************************************************************
 *** No BLAS library found so using dlib's built in BLAS.  However, if you ***
 *** install an optimized BLAS such as OpenBLAS or the Intel MKL your code ***
 *** will run faster.  On Ubuntu you can install OpenBLAS by executing:    ***
 ***    sudo apt-get install libopenblas-dev liblapack-dev                 ***
 *** Or you can easily install OpenBLAS from source by downloading the     ***
 *** source tar file from http://www.openblas.net, extracting it, and      ***
 *** running:                                                              ***
 ***    make; sudo make install                                            ***
 *****************************************************************************
CUDA_TOOLKIT_ROOT_DIR not found or specified
-- Could NOT find CUDA (missing: CUDA_TOOLKIT_ROOT_DIR CUDA_NVCC_EXECUTABLE CUDA_INCLUDE_DIRS CUDA_CUDART_LIBRARY) (Required is at least version "7.5")
-- DID NOT FIND CUDA
-- Disabling CUDA support for dlib.  DLIB WILL NOT USE CUDA
-- C++11 activated.
-- Configuring done
-- Generating done
-- Build files have been written to: /root/fares/dlib/build/temp.linux-x86_64-3.6
Invoking CMake build: 'cmake --build . --config Release -- -j2'
Scanning dependencies of target dlib
[  1%] Building CXX object dlib_build/CMakeFiles/dlib.dir/bigint/bigint_kernel_1.cpp.o
[  1%] Building CXX object dlib_build/CMakeFiles/dlib.dir/base64/base64_kernel_1.cpp.o
[  1%] Building CXX object dlib_build/CMakeFiles/dlib.dir/bigint/bigint_kernel_2.cpp.o
[  2%] Building CXX object dlib_build/CMakeFiles/dlib.dir/bit_stream/bit_stream_kernel_1.cpp.o
[  3%] Building CXX object dlib_build/CMakeFiles/dlib.dir/entropy_decoder/entropy_decoder_kernel_1.cpp.o
[  3%] Building CXX object dlib_build/CMakeFiles/dlib.dir/entropy_decoder/entropy_decoder_kernel_2.cpp.o
[  4%] Building CXX object dlib_build/CMakeFiles/dlib.dir/entropy_encoder/entropy_encoder_kernel_1.cpp.o
[  5%] Building CXX object dlib_build/CMakeFiles/dlib.dir/entropy_encoder/entropy_encoder_kernel_2.cpp.o
[  5%] Building CXX object dlib_build/CMakeFiles/dlib.dir/md5/md5_kernel_1.cpp.o
[...]
[ 81%] Building CXX object dlib_build/CMakeFiles/dlib.dir/image_loader/jpeg_loader.cpp.o
[ 82%] Building CXX object dlib_build/CMakeFiles/dlib.dir/image_saver/save_jpeg.cpp.o
[ 83%] Linking CXX static library libdlib.a
[ 83%] Built target dlib
Scanning dependencies of target dlib_python
[ 84%] Building CXX object CMakeFiles/dlib_python.dir/src/matrix.cpp.o
[ 84%] Building CXX object CMakeFiles/dlib_python.dir/src/dlib.cpp.o
[ 84%] Building CXX object CMakeFiles/dlib_python.dir/src/vector.cpp.o
[...]
[ 95%] Building CXX object CMakeFiles/dlib_python.dir/src/correlation_tracker.cpp.o
[ 96%] Building CXX object CMakeFiles/dlib_python.dir/src/face_recognition.cpp.o
[ 96%] Building CXX object CMakeFiles/dlib_python.dir/src/cnn_face_detector.cpp.o
[ 97%] Building CXX object CMakeFiles/dlib_python.dir/src/global_optimization.cpp.o
[ 98%] Building CXX object CMakeFiles/dlib_python.dir/src/image_dataset_metadata.cpp.o
[ 98%] Building CXX object CMakeFiles/dlib_python.dir/src/numpy_returns.cpp.o
[ 99%] Building CXX object CMakeFiles/dlib_python.dir/src/line.cpp.o
[100%] Linking CXX shared module /root/fares/dlib/build/lib.linux-x86_64-3.6/dlib.cpython-36m-x86_64-linux-gnu.so
[100%] Built target dlib_python
creating build/bdist.linux-x86_64
creating build/bdist.linux-x86_64/egg
copying build/lib.linux-x86_64-3.6/dlib.cpython-36m-x86_64-linux-gnu.so -> build/bdist.linux-x86_64/egg
creating stub loader for dlib.cpython-36m-x86_64-linux-gnu.so
byte-compiling build/bdist.linux-x86_64/egg/dlib.py to dlib.cpython-36.pyc
creating build/bdist.linux-x86_64/egg/EGG-INFO
copying dlib.egg-info/PKG-INFO -> build/bdist.linux-x86_64/egg/EGG-INFO
copying dlib.egg-info/SOURCES.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying dlib.egg-info/dependency_links.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying dlib.egg-info/not-zip-safe -> build/bdist.linux-x86_64/egg/EGG-INFO
copying dlib.egg-info/top_level.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
writing build/bdist.linux-x86_64/egg/EGG-INFO/native_libs.txt
creating dist
creating 'dist/dlib-19.19.99-py3.6-linux-x86_64.egg' and adding 'build/bdist.linux-x86_64/egg' to it
removing 'build/bdist.linux-x86_64/egg' (and everything under it)
Processing dlib-19.19.99-py3.6-linux-x86_64.egg
creating /usr/local/lib/python3.6/dist-packages/dlib-19.19.99-py3.6-linux-x86_64.egg
Extracting dlib-19.19.99-py3.6-linux-x86_64.egg to /usr/local/lib/python3.6/dist-packages
Adding dlib 19.19.99 to easy-install.pth file

Installed /usr/local/lib/python3.6/dist-packages/dlib-19.19.99-py3.6-linux-x86_64.egg
Processing dependencies for dlib==19.19.99
Finished processing dependencies for dlib==19.19.99
```

Instalare DLIB **cu** suport GPU. In primul rand este nevoie de instalarea bibliotecilor
CUDA si cuDNN. Descarcarea lor se face de pe site-ul nVidia (https://nvidia.com) si este
nevoie de autentificare pentru a le putea descarca. Versiunea cuDNN trebuie sa corespunda
cu cea a bibliotecilor CUDA.
```bash
root@dev-04-ubuntu:~/fares# dpkg -i libcudnn7_7.6.5.32-1+cuda10.1_amd64.deb libcudnn7-dev_7.6.5.32-1+cuda10.1_amd64.deb
Selecting previously unselected package libcudnn7.
(Reading database ... 193929 files and directories currently installed.)
Preparing to unpack .../libcudnn7_7.6.5.32-1+cuda10.1_amd64.deb ...
Unpacking libcudnn7 (7.6.5.32-1+cuda10.1) ...
Preparing to unpack .../libcudnn7-dev_7.6.5.32-1+cuda10.1_amd64.deb ...
Unpacking libcudnn7-dev (7.6.5.32-1+cuda10.1) over (7.6.5.32-1+cuda10.1) ...
Setting up libcudnn7 (7.6.5.32-1+cuda10.1) ...
Setting up libcudnn7-dev (7.6.5.32-1+cuda10.1) ...
update-alternatives: using /usr/include/x86_64-linux-gnu/cudnn_v7.h to provide /usr/include/cudnn.h (libcudnn) in auto mode
Processing triggers for libc-bin (2.27-3ubuntu1) ...
```

```bash
root@dev-04-ubuntu:~/fares# git clone https://github.com/davisking/dlib.git
root@dev-04-ubuntu:~/fares# cd dlib
root@dev-04-ubuntu:~/fares/dlib# mkdir build; cd build
root@dev-04-ubuntu:~/fares/dlib/build# cmake  -D DLIB_USE_CUDA=1 -D USE_AVX_INSTRUCTIONS=1 ..
-- Using CMake version: 3.10.2
-- Compiling dlib version: 19.19.99
-- Enabling AVX instructions
-- Found system copy of libpng: /usr/lib/x86_64-linux-gnu/libpng.so;/usr/lib/x86_64-linux-gnu/libz.so
-- Found system copy of libjpeg: /usr/lib/x86_64-linux-gnu/libjpeg.so
-- Looking for cuDNN install...
-- Found cuDNN: /usr/lib/x86_64-linux-gnu/libcudnn.so
-- Building a CUDA test project to see if your compiler is compatible with CUDA...
-- Checking if you have the right version of cuDNN installed.
-- Enabling CUDA support for dlib.  DLIB WILL USE CUDA
-- C++11 activated.
-- Configuring done
-- Generating done
-- Build files have been written to: /root/fares/dlib/build

root@dev-04-ubuntu:~/fares/dlib/build# cmake --build . --config Release
[  1%] Building NVCC (Device) object dlib/CMakeFiles/dlib.dir/cuda/dlib_generated_cusolver_dlibapi.cu.o
[  3%] Building NVCC (Device) object dlib/CMakeFiles/dlib.dir/cuda/dlib_generated_cuda_dlib.cu.o
Scanning dependencies of target dlib
[  4%] Building CXX object dlib/CMakeFiles/dlib.dir/base64/base64_kernel_1.cpp.o
[  6%] Building CXX object dlib/CMakeFiles/dlib.dir/bigint/bigint_kernel_1.cpp.o
[  7%] Building CXX object dlib/CMakeFiles/dlib.dir/bigint/bigint_kernel_2.cpp.o
[  9%] Building CXX object dlib/CMakeFiles/dlib.dir/bit_stream/bit_stream_kernel_1.cpp.o
[ 10%] Building CXX object dlib/CMakeFiles/dlib.dir/entropy_decoder/entropy_decoder_kernel_1.cpp.o
[...]
[ 86%] Building CXX object dlib/CMakeFiles/dlib.dir/image_loader/png_loader.cpp.o
[ 87%] Building CXX object dlib/CMakeFiles/dlib.dir/image_saver/save_png.cpp.o
[ 89%] Building CXX object dlib/CMakeFiles/dlib.dir/image_loader/jpeg_loader.cpp.o
[ 90%] Building CXX object dlib/CMakeFiles/dlib.dir/image_saver/save_jpeg.cpp.o
[ 92%] Building CXX object dlib/CMakeFiles/dlib.dir/cuda/cudnn_dlibapi.cpp.o
[ 93%] Building CXX object dlib/CMakeFiles/dlib.dir/cuda/cublas_dlibapi.cpp.o
[ 95%] Building CXX object dlib/CMakeFiles/dlib.dir/cuda/curand_dlibapi.cpp.o
[ 96%] Building CXX object dlib/CMakeFiles/dlib.dir/cuda/cuda_data_ptr.cpp.o
[ 98%] Building CXX object dlib/CMakeFiles/dlib.dir/cuda/gpu_data.cpp.o
[100%] Linking CXX static library libdlib.a
[100%] Built target dlib

root@dev-04-ubuntu:~/fares/dlib/build# cd ..
root@dev-04-ubuntu:~/fares/dlib# python3 setup.py install
running install
running bdist_egg
running egg_info
creating dlib.egg-info
writing dlib.egg-info/PKG-INFO
writing dependency_links to dlib.egg-info/dependency_links.txt
writing top-level names to dlib.egg-info/top_level.txt
writing manifest file 'dlib.egg-info/SOURCES.txt'
package init file 'dlib/__init__.py' not found (or not a regular file)
reading manifest file 'dlib.egg-info/SOURCES.txt'
reading manifest template 'MANIFEST.in'
no previously-included directories found matching 'tools/python/build*'
writing manifest file 'dlib.egg-info/SOURCES.txt'
installing library code to build/bdist.linux-x86_64/egg
running install_lib
running build_py
running build_ext
Building extension for Python 3.6.9 (default, Nov  7 2019, 10:44:02)
[...]
-- Found CUDA: /usr/local/cuda-10.1 (found suitable version "10.1", minimum required is "7.5")
-- Looking for cuDNN install...
-- Found cuDNN: /usr/lib/x86_64-linux-gnu/libcudnn.so
-- Building a CUDA test project to see if your compiler is compatible with CUDA...
-- Checking if you have the right version of cuDNN installed.
-- Enabling CUDA support for dlib.  DLIB WILL USE CUDA
-- C++11 activated.
-- Configuring done
-- Generating done
-- Build files have been written to: /root/fares/dlib/build/temp.linux-x86_64-3.6
Invoking CMake build: 'cmake --build . --config Release -- -j12'
[  2%] Building NVCC (Device) object dlib_build/CMakeFiles/dlib.dir/cuda/dlib_generated_cusolver_dlibapi.cu.o
[  2%] Building NVCC (Device) object dlib_build/CMakeFiles/dlib.dir/cuda/dlib_generated_cuda_dlib.cu.o
Scanning dependencies of target dlib
[  3%] Building CXX object dlib_build/CMakeFiles/dlib.dir/entropy_encoder/entropy_encoder_kernel_2.cpp.o
[  4%] Building CXX object dlib_build/CMakeFiles/dlib.dir/bigint/bigint_kernel_1.cpp.o
[  5%] Building CXX object dlib_build/CMakeFiles/dlib.dir/bit_stream/bit_stream_kernel_1.cpp.o
[...]
[ 95%] Building CXX object CMakeFiles/dlib_python.dir/src/image_dataset_metadata.cpp.o
[ 96%] Building CXX object CMakeFiles/dlib_python.dir/src/numpy_returns.cpp.o
[ 97%] Building CXX object CMakeFiles/dlib_python.dir/src/line.cpp.o
[ 98%] Building CXX object CMakeFiles/dlib_python.dir/src/gui.cpp.o
[100%] Linking CXX shared module /root/AI/dlib/build/lib.linux-x86_64-3.6/dlib.cpython-36m-x86_64-linux-gnu.so
[100%] Built target dlib_python
creating build/bdist.linux-x86_64
creating build/bdist.linux-x86_64/egg
copying build/lib.linux-x86_64-3.6/dlib.cpython-36m-x86_64-linux-gnu.so -> build/bdist.linux-x86_64/egg
creating stub loader for dlib.cpython-36m-x86_64-linux-gnu.so
byte-compiling build/bdist.linux-x86_64/egg/dlib.py to dlib.cpython-36.pyc
creating build/bdist.linux-x86_64/egg/EGG-INFO
copying dlib.egg-info/PKG-INFO -> build/bdist.linux-x86_64/egg/EGG-INFO
copying dlib.egg-info/SOURCES.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying dlib.egg-info/dependency_links.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying dlib.egg-info/not-zip-safe -> build/bdist.linux-x86_64/egg/EGG-INFO
copying dlib.egg-info/top_level.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
writing build/bdist.linux-x86_64/egg/EGG-INFO/native_libs.txt
creating dist
creating 'dist/dlib-19.19.99-py3.6-linux-x86_64.egg' and adding 'build/bdist.linux-x86_64/egg' to it
removing 'build/bdist.linux-x86_64/egg' (and everything under it)
Processing dlib-19.19.99-py3.6-linux-x86_64.egg
creating /usr/local/lib/python3.6/dist-packages/dlib-19.19.99-py3.6-linux-x86_64.egg
Extracting dlib-19.19.99-py3.6-linux-x86_64.egg to /usr/local/lib/python3.6/dist-packages
Adding dlib 19.19.99 to easy-install.pth file

Installed /usr/local/lib/python3.6/dist-packages/dlib-19.19.99-py3.6-linux-x86_64.egg
Processing dependencies for dlib==19.19.99
Finished processing dependencies for dlib==19.19.99

```


### 1.4 Instalare alte module python3
```bash
root@dev-04-ubuntu:~/fares/dlib# cd ..
root@dev-04-ubuntu:~/fares# pip3 install wheel
[...]
root@dev-04-ubuntu:~/fares# pip3 install face_recognition matplotlib flask
[...]
```


### 1.5 Instalare componente server web (**optional**, doar pentru mediu de productie)
```bash
root@dev-04-ubuntu:~/fares# mkdir -p /usr/local/fares && cd /usr/local/fares
root@dev-04-ubuntu:/usr/local/fares#
root@dev-04-ubuntu:/usr/local/fares# apt-get install python3-venv
root@dev-04-ubuntu:/usr/local/fares# python3 -m venv ./.venv

root@dev-04-ubuntu:/usr/local/fares# source ./.venv/bin/activate

(.venv) root@dev-04-ubuntu:/usr/local/fares# python --version
Python 3.6.9
(.venv) root@dev-04-ubuntu:/usr/local/fares# pip -V
pip 9.0.1 from /usr/local/fares/.venv/lib/python3.6/site-packages (python 3.6)

(.venv) root@dev-04-ubuntu:/usr/local/fares# pip install gunicorn flask
Collecting gunicorn
[...]
Installing collected packages: gunicorn, MarkupSafe, Jinja2, click, Werkzeug, itsdangerous, flask
Successfully installed Jinja2-2.11.1 MarkupSafe-1.1.1 Werkzeug-1.0.1 click-7.1.1 flask-1.1.1 gunicorn-20.0.4 itsdangerous-1.1.0

(.venv) root@dev-04-ubuntu:/usr/local/fares# pip install wheel
Collecting wheel
[...]
Installing collected packages: wheel
Successfully installed wheel-0.34.2

(.venv) root@dev-04-ubuntu:/usr/local/fares# pip3 install face_recognition matplotlib
[...]
Installing collected packages: Pillow, dlib, numpy, face-recognition-models, face-recognition, six, python-dateutil, cycler, pyparsing, kiwisolver, matplotlib
Successfully installed Pillow-7.1.0 cycler-0.10.0 dlib-19.19.0 face-recognition-1.3.0 face-recognition-models-0.3.0 kiwisolver-1.2.0 matplotlib-3.2.1 numpy-1.18.2 pyparsing-2.4.6 python-dateutil-2.8.1 six-1.14.0

(.venv) root@dev-04-ubuntu:/usr/local/fares# deactivate
root@dev-04-ubuntu:/usr/local/fares#
```



## 2. Rulare server FaReS

Serverul de recunoastere poate fi rulat in mai multe moduri.

### 2.1 Folosind serverul intern al Flask - **doar pentru dezvoltare**
Se ruleaza serverul direct, din directorul unde a fost instalat. Acest server este **doar
pentru dezvoltare**; permite o singura conexiune.
```bash
root@dev-04-ubuntu:~# cd /usr/local/fares
root@dev-04-ubuntu:/usr/local/fares# ./fares.py
--------------------------------------------------------------------------------
DEBUG in fares [./fares.py:494]:
App created in create_app()
--------------------------------------------------------------------------------
 * Running on http://0.0.0.0:1025/ (Press CTRL+C to quit)
 * Restarting with stat
--------------------------------------------------------------------------------
DEBUG in fares [./fares.py:494]:
App created in create_app()
--------------------------------------------------------------------------------
 * Debugger is active!
 * Debugger PIN: 821-394-215
```

Se poate incarca in browser pagina aflata la URL http://<host>:1025/. De asemenea, se poate
rula pentru teste clientul intr-o alta consola.
```bash
root@dev-04-ubuntu:~# cd /usr/local/fares
root@dev-04-ubuntu:/usr/local/fares# bin/client_compare.py 127.0.0.1 1025 demo/image1.jpg demo/image2.jpg
{"info": {"code": 502, "message": "Internal server error. Please check the logs."}, "data": {"request_id": "", "id": "", "elapsed": -1, "distance": -1, "match": false}}
```


### 2.2 Folosind gunicorn (eventual cu supervisord) - **doar pentru servere interne**
Se trece in virtual environment si se ruleaza folosind gunicorn.
```bash
root@dev-04-ubuntu:~# cd /usr/local/fares
root@dev-04-ubuntu:/usr/local/fares# source ./.venv/bin/activate
(.venv) root@dev-04-ubuntu:/usr/local/fares#  gunicorn \
--workers 4 --bind 0.0.0.0:8000 wsgifares:app --log-level DEBUG --log-level=debug \
--log-file /usr/local/fares/log/gunicorn.log \
--access-logfile /usr/local/fares/log/access.log \
--error-logfile /usr/local/fares/log/error.log
[2020-04-02 13:50:19,819] INFO in fares: Setting up gunicorn logger done
[2020-04-02 13:50:19,819] DEBUG in fares: App created in create_app()
[2020-04-02 13:50:19,821] INFO in fares: Setting up gunicorn logger done
[2020-04-02 13:50:19,822] DEBUG in fares: App created in create_app()
[2020-04-02 13:50:19,825] INFO in fares: Setting up gunicorn logger done
[2020-04-02 13:50:19,825] DEBUG in fares: App created in create_app()
[2020-04-02 13:50:19,842] INFO in fares: Setting up gunicorn logger done
[2020-04-02 13:50:19,842] DEBUG in fares: App created in create_app()
[...]
```

Se poate incarca in browser pagina aflata la URL http://<host>:8000/. Sau se poate rula
pentru teste clientul intr-o alta consola.
```bash
root@dev-04-ubuntu:~# cd /usr/local/fares
root@dev-04-ubuntu:/usr/local/fares# bin/client_compare.py 127.0.0.1 8000 demo/image1.jpg demo/image2.jpg
{"info": {"code": 101, "message": "Max image size exceeded - base"}, "data": {"request_id": "DEFSERVER-1585828520.0941336-343371", "id": "AAAAaaaaaAAAAA111112", "elapsed": -1, "distance": -1, "match": false}}
root@dev-04-ubuntu:/usr/local/fares# bin/client_compare.py 127.0.0.1 8000 demo/image3.jpg demo/image2.jpg
{"info": {"code": 0, "message": ""}, "data": {"request_id": "DEFSERVER-1585828553.7371156-741199", "id": "AAAAaaaaaAAAAA111112", "elapsed": 1.9375565680002182, "distance": 0.5545955447440855, "match": true, "validate_facerectangle": {"top": 98, "left": 221, "height": 186, "width": 186}}}
```

De asemenea, gunicorn poate fi configurat sa fie folosit ca serviciu. Distributia ofera
un fisier de configurate pentru gunicorn (`gunicorn.conf.py`), in directorul `etc` .
```bash
root@dev-04-ubuntu:~# cd /usr/local/fares
root@dev-04-ubuntu:/usr/local/fares# cat etc/gunicorn.conf.py
# file gunicorn.conf.py
# coding=utf-8
# Reference: https://github.com/benoitc/gunicorn/blob/master/examples/example_config.py
import os
import multiprocessing

_ROOT = os.path.abspath(os.path.join(
    os.path.dirname(__file__), '..'))
_VAR = os.path.join(_ROOT, 'var')
_ETC = os.path.join(_ROOT, 'etc')

loglevel = 'debug'
#errorlog = os.path.join(_VAR, 'log/error.log')
#accesslog = os.path.join(_VAR, 'log/access.log')
errorlog = 'log/error.log'
accesslog = 'log/access.log'
#errorlog = "-"
#accesslog = "-"

# bind = 'unix:%s' % os.path.join(_VAR, 'run/gunicorn.sock')
bind = '0.0.0.0:8000'
# workers = 4
workers = multiprocessing.cpu_count() * 2 + 1

timeout = 3 * 60  # 3 minutes
keepalive = 4 * 60 * 60  # 1 day

capture_output = True

```

Gunicorn poate fi pornit folosind fisierul de configurare:
```bash
root@dev-04-ubuntu:~# cd /usr/local/fares
root@dev-04-ubuntu:/usr/local/fares#
root@dev-03-ubuntu:/usr/local/fares# source ./.venv/bin/activate
(.venv) root@dev-03-ubuntu:/usr/local/fares# gunicorn -c etc/gunicorn.conf.py wsgifares:app
[...]
```

Evident, gunicorn este cel mai bine folosit cu supervisord, care il va porni la reboot sau daca se intampla sa se opreasca.
```bash
root@dev-04-ubuntu:~# cd /usr/local/fares
root@dev-04-ubuntu:/usr/local/fares# apt-get install supervisor
Reading package lists... Done
Building dependency tree
Reading state information... Done
[...]

root@dev-04-ubuntu:/usr/local/fares# service supervisor status
● supervisor.service - Supervisor process control system for UNIX
   Loaded: loaded (/lib/systemd/system/supervisor.service; enabled; vendor preset: enabled)
   Active: active (running) since Thu 2020-04-02 15:28:30 CEST; 32s ago
     Docs: http://supervisord.org
 Main PID: 28918 (supervisord)
    Tasks: 1 (limit: 4915)
   CGroup: /system.slice/supervisor.service
           └─28918 /usr/bin/python /usr/bin/supervisord -n -c /etc/supervisor/supervisord.conf

Apr 02 15:28:30 dev-04-ubuntu systemd[1]: Started Supervisor process control system for UNIX.
Apr 02 15:28:30 dev-04-ubuntu supervisord[28918]: 2020-04-02 15:28:30,307 CRIT Supervisor running as root (no user in config file)
Apr 02 15:28:30 dev-04-ubuntu supervisord[28918]: 2020-04-02 15:28:30,308 WARN No file matches via include "/etc/supervisor/conf.d/*.conf"
Apr 02 15:28:30 dev-04-ubuntu supervisord[28918]: 2020-04-02 15:28:30,315 INFO RPC interface 'supervisor' initialized
Apr 02 15:28:30 dev-04-ubuntu supervisord[28918]: 2020-04-02 15:28:30,315 CRIT Server 'unix_http_server' running without any HTTP authentication checking
Apr 02 15:28:30 dev-04-ubuntu supervisord[28918]: 2020-04-02 15:28:30,315 INFO supervisord started with pid 28918

root@dev-04-ubuntu:/usr/local/fares# adduser faresuser
[...]
root@dev-04-ubuntu:/usr/local/fares# adduser faresuser sudo
Adding user `faresuser' to group `sudo' ...
Adding user faresuser to group sudo
Done.
root@dev-04-ubuntu:/usr/local/fares# chown -R faresuser:faresuser /usr/local/fares

```

Este nevoie de un fisier de configurare pentru supervisor. Un asemenea fisier este furnizat
cu serverul (`supervisor-fares-app.conf`), odata cu un fisier care porneste gunicorn (`run.sh`).
```bash
root@dev-04-ubuntu:/usr/local/fares# cat etc/supervisor-fares-app.conf
;/etc/supervisor/conf.d/fares-app.conf
[program:fares_app]
user = faresuser
directory = /usr/local/fares
command = /usr/local/fares/run.sh gunicorn -c etc/gunicorn.conf.py wsgifares:app

priority = 900
autostart = true
autorestart = true
stopsignal = TERM

redirect_stderr = true
stdout_logfile = /usr/local/fares/log/%(program_name)s.log
stderr_logfile = /usr/local/fares/log/%(program_name)s.log

root@dev-04-ubuntu:/usr/local/fares# cat run.sh
#!/bin/bash -e

if [ -f .venv/bin/activate ]; then
    echo   "Load Python virtualenv from '.venv/bin/activate'"
    source .venv/bin/activate
fi
exec "$@"
```

Fisierul de configurare poate fi copiat si folosit; trebuie doar pornit serviciul supervisor.
```bash
root@dev-04-ubuntu:/usr/local/fares# cp etc/supervisor-fares-app.conf /etc/supervisor/conf.d/fares-app.conf

root@dev-04-ubuntu:/usr/local/fares# supervisorctl reread
fares_app: available
root@dev-04-ubuntu:/usr/local/fares# supervisorctl update
fares_app: added process group
root@dev-04-ubuntu:/usr/local/fares# supervisorctl avail
root@dev-04-ubuntu:/usr/local/fares# supervisorctl avail
fares_app                        in use    auto      900:900
root@dev-04-ubuntu:/usr/local/fares# supervisorctl restart fares_app
fares_app: ERROR (not running)
fares_app: started
root@dev-04-ubuntu:/usr/local/fares-server# netstat -natup | grep 8000
tcp        0      0 0.0.0.0:8000            0.0.0.0:*               LISTEN      29422/python3
root@dev-04-ubuntu:/usr/local/fares# supervisorctl stop fares_app
fares_app: stopped
```

Daca trebuie repornit serviciul supervisor, se poate realiza cu comanda `service supervisor restart`.


### 2.3 Folosind nginx si gunicorn (eventual cu supervisord) - **pentru servere publice**

```bash
root@dev-04-ubuntu:~/fares# apt-get install nginx php7.2 php7.2-fpm php7.2-bz2 php7.2-bcmath php7.2-soap \
  php7.2-zip php7.2-sqlite3 php7.2-xml php7.2-mysql php7.2-json php7.2-gmp php7.2-gd php7.2-curl php-redis \
  php-mongodb php-imagick php-memcached
[...]
```

