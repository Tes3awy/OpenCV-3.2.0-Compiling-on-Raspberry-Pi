# Compile OpenCV 3.0.0 + OpenCV Contrib for Python on Raspberry Pi 2B

# Step 1:

	$ sudo apt-get update
	$ sudo apt-get upgrade
	$ sudo rpi-update (can be skipped, but recommended)
	$ sudo reboot now

# Step 2:

	$ sudo apt-get install build-essential cmake pkg-config

# tep 3:

	$ sudo apt-get install libjpeg8-dev libtiff5-dev libjasper-dev libpng12-dev

# Step 4:

	$ sudo apt-get install libgtk2.0-dev

# Step 5:

	$ sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev

# Step 6:

	$ sudo apt-get install libatlas-base-dev gfortran
	$ sudo apt-get install python-numpy python-scipy python-matplotlib
	$ sudo apt-get install default-jdk ant
	$ sudo apt-get install libgtkglext1-dev
	$ sudo apt-get install v4l-utils

# Step 7:
install pip

	$ wget https://bootstrap.pypa.io/get-pip.py
	$ sudo python get-pip.py

# Step 8:

	$ sudo apt-get install python2.7-dev

# Step 9:

	$ pip install numpy

# Step 10:
download OpenCV 3.0.0 and unpack it

	$ cd ~
	$ wget -O opencv.zip https://github.com/Itseez/opencv/archive/3.0.0.zip
	$ unzip opencv.zip

Contrib Libraries

	$ wget -O opencv_contrib.zip https://github.com/Itseez/opencv_contrib/archive/3.0.0.zip
	$ unzip opencv_contrib.zip

# Step 11:
preparing the build

	$ cd ~/opencv-3.0.0/
	$ mkdir build
	$ cd build
	$ cmake -D CMAKE_BUILD_TYPE=RELEASE \
		-D CMAKE_INSTALL_PREFIX=/usr/local \
		-D INSTALL_C_EXAMPLES=ON \
		-D INSTALL_PYTHON_EXAMPLES=ON \
		-D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-3.0.0/modules \
		-D BUILD_EXAMPLES=ON ..

# Step 12:
takes about 3.5 to 4 hours

	$ make -j4 (I prefer -j3, because it doesn't use all the cores so it keeps the RasPi cool enough)

# Step 13:
installing the build prepared in step 11

	$ sudo make install
	$ sudo ldconfig

# Step 14:

	$ sudo nano /etc/ld.so.conf.d/opencv.conf

opencv.conf will be blank, add the following line, then save and exit nano:

	/usr/local/lib          # enter this in opencv.conf, NOT at the command line
				(leave a blank line at the end of opencv.conf)


save opencv.conf by pressing ctrl+o
get back again to the command line by pressing ctrl+x

	$ sudo ldconfig

	$ sudo nano /etc/bash.bashrc

add the following lines at the bottom of bash.bashrc

	PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig       
	export PKG_CONFIG_PATH

(leave a blank line at the end of bash.bashrc)
save bash.bashrc changes (ctrl+o), then back at the command line (ctrl+x), 

#Step 15:
Reboot

	$ sudo shutdown -r now

#Step 16 Last Step:
verifying the installation

Open Python 2 IDLE on RasPi
Type the following lines in the python shell:

	>>> import cv2
	>>> print cv2.__version__

the following line should appear then:

	'3.0.0'
#Done

# Watch this repo to get updates. I will be posting how to connect Raspberry Pi to PC with ETHERNET CABLE (no internet needed)
