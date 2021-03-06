# Ortho4XP_FSX_P3D
A scenery generator for the X-Plane flight simulator

Work in progress at adding FSX/P3D (ESP support)

# Use at your own risk

# Prerequisites

Please install ImageMagick before attempting to run, otherwise the night/season creation won't work. An installer has been provided inside the dist/ directory.
The same installer can also be found here: https://www.imagemagick.org/download/binaries/ImageMagick-7.0.8-10-Q8-x64-dll.exe

NOTE: Need to provide the location of your resample.exe from the P3D or FSX SDK in Ortho4XP.cfg, like this:

`ESP_resample_loc=C:\\LOCATION\\TO\\resample.exe`

Notice the double backslashes `\\` instead of single `\`.

You can obtain the P3D resample.exe by installing the P3D SDK provided by Lockheed Martin on their site where you download P3D.
The FSX resample.exe can be found by installing the FSX SDK found in the FSX Deluxe Disc 2 or in FSX Acceleration Pack (or FSX Gold which includes the Acceleration pack)

# Running from exe
An executable (.exe) file has been provided in the dist/ directory, if you don't want to build the binary yourself. Simply double click on it, and it'll run.

# Running with Python
To install, follow the install guide for Ortho4XP, making sure to install all python libraries, and run Ortho4XP_v130.py from the command line.

# Example run from exe
https://www.youtube.com/watch?v=fkvmlbJXAq4

# Building binary (only tested on windows 10 64 bit):
Use pyinstaller like this:

`pyinstaller --clean -F -p src Ortho4XP_v130.py`

Then, copy spatialindex-64.dll and spatialindex_c.dll (from rtree python module) into the dist folder where the new executable is:

`cp /cygdrive/c/Users/fery2/AppData/Local/Programs/Python/Python36/lib/site-packages/rtree/spatialindex*.dll dist/`

To build the imagemagick based c++ dll, do something like:

`"F:\ExtraPrograms\Microsoft Visual Studio\2017\Community\VC\Tools\MSVC\14.14.26428\bin\Hostx64\x64\cl.exe" /LD /I "C:\Program Files\ImageMagick-7.0.8-Q8\include" /I C:/Users/fery2/AppData/Local/Programs/Python/Python36/include /I src\cpp\fast_image_mask.cpp src\cpp\FSET_ports.cpp  C:\Users\fery2\AppData\Local\Programs\Python\Python36\libs\python36.lib "C:\Program Files\ImageMagick-7.0.8-Q8\lib\CORE_RL_Magick++_.lib" "C:\Program Files\ImageMagick-7.0.8-Q8\lib\CORE_RL_MagickCore_.lib" "C:\Program Files\ImageMagick-7.0.8-Q8\lib\CORE_RL_MagickWand_.lib"`

Make sure the visual ++ environment is set to the correct bit of your python (32 vs 64 bit)

Note:
Imagemagick is required, specifically the q8 quantum depth version. To build it on UNIX from source code, configure like this:

`./configure --with-tiff=yes --with-quantum-depth=8`

# FINISHED:
base satellite imagery creation for FSX and P3D
water masks for FSX and P3D
build binary
night/seasonal texture creation options

# TODO:
remove extra steps not needed for ESP scenery creation
add integration with sceneproc to allow for adding of custom autogen from OpenStreetMap data
