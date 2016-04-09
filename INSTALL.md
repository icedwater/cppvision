# Installing OpenCV on Ubuntu 15.04

This is adapted from the [2.0 tutorial][v2tut] which also expects Ubuntu 10.04,
so most of the version numbers would no longer be relevant. I hope to find what
works and send this to the OpenCV site at some point.

## Required Packages
 * gcc 4.4.x or later
 * cmake 2.8.7 or higher
 * git
 * gtk+2.x or higher, including headers (libgtk2.0-dev)
 * pkg-config
 * Python 2.6 or later and Numpy 1.5 or later with developer packages
   (python-dev, python-numpy)
 * ffmpeg or libav development packages:
   * libavcodec-dev
   * libavformat-dev
   * libswscale-dev

This should normally be achieved by running the following commands:

    sudo apt-get install build-essential
    sudo apt-get install cmake git libgtk2.0-dev pkg-config
    sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev

## Installation Issues
I had some difficulty with libgtk2.0-dev though, some dependencies would not be
installed at first. It turns out that ubuntu-desktop was using a higher version
of libglib2.0-dev than libgtk2.0-dev was expecting, so I had to downgrade that.
The versions of dependencies you would need to specify can be seen in the error
message when the earlier apt-get install fails. It looks like this:

    The following packages have unmet dependencies: 
    libgtk2.0-dev : Depends libglib2.0-0 (= 2.44.0-ubuntu-3) but ... 

So just amend the install instruction for libglib2.0-0 as follows:

    sudo apt-get install libglib2.0-0=2.44.0-ubuntu-3 # for my case

This removes ubuntu-desktop, along with other important packages; however it is
possible to just reinstall this and all the dependencies will be pulled in:

    sudo apt-get install ubuntu-desktop

After this, there was still an issue with libpcre3, which I had to downgrade in
order to install the correct version of libpcre3-dev that libgtk2.0-dev needs:

    sudo apt-get install libpcre3=2:8.35-3.3ubuntu1 # for my case

However, there is still an issue with held packages (specific version numbers),
which I am yet to resolve. It seems the chain runs pretty far down, so it might
be a lot easier to wait till the next LTS version of Ubuntu (16.04) to try this
again.

## Optional Packages
 * libtbb2 libtbb-dev
 * libdc1394 2.x 
 * libjpeg-dev
 * libpng-dev 
 * libtiff-dev 
 * libjasper-dev 
 * libdc1394-22-dev 

Again, run these commands to set up the packages as needed:

    sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev
    sudo apt-get install libjpeg-dev libpng-dev libtiff-dev
    sudo apt-get install libjasper-dev libdc1394-22-dev

## Installation notes

There were fewer issues with the optional libraries, but some packages had been
renamed, such as libtiff5-dev and libpng12-dev rather than just libtiff-dev and
libpng-dev. But these should not present issues during compile time.

[v2tut]: http://docs.opencv.org/3.1.0/d7/d9f/tutorial_linux_install.html
