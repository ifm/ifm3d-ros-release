ifm3d-ros on Ubuntu 14.04 and ROS Indigo
----------------------------------------

This article provides a quick-start guide for getting a fresh install of Ubuntu
14.04 ready for usage with `ifm3d-ros` and an O3X camera. As a pre-requisite
for this article, we assume you already have Ubuntu 14.04 installed (but have
done no other configuration) and that you will be using `ifm3d` version `0.2.0`
and `ifm3d-ros` version `0.2.0`. Later versions of the `ifm3d` and `ifm3d-ros`
software will work as well until we end-of-life Ubuntu 14.04 and ROS
Indigo. Finally, since we assume you have done no updates to your Ubuntu
install, we also assume you are using `g++` version `4.8.4` (which is old).

### Update the Baseline Packages of your Ubuntu 14.04 Install

```
$ sudo apt-get update
$ sudo apt-get -u upgrade
```

### Install ROS Indigo

You should now follow
[these steps](http://wiki.ros.org/indigo/Installation/Ubuntu) exactly (we
assume you did) and that you chose to install `ros-indigo-desktop-full`. Go do
that now, then continue on.

### Additional Dependencies

There are a few things that we need to install to successfully build from
source that we did not get implicitly by installing ROS. The following commands
will handle these pre-requisites:

```
$ sudo apt-get install libxmlrpc-c++8-dev
$ sudo apt-get install libgoogle-glog-dev
```

### Install ifm3d

[ifm3d](https://github.com/lovepark/ifm3d) is the core underlying C++ driver
that `ifm3d-ros` wraps. We need to install that now. We assume you keep all of
your source code in `~/dev`.

```
$ mkdir ~/dev
$ cd ~/dev
$ git clone https://github.com/lovepark/ifm3d.git
$ cd ifm3d
$ mkdir build
$ cd build
$ cmake -DCMAKE_INSTALL_PREFIX=/usr -DFORCE_OPENCV2=ON ..
$ make
$ make check
$ make package
$ make repackage
$ sudo dpkg -i ifm3d_0.2.0_amd64-camera.deb
$ sudo dpkg -i ifm3d_0.2.0_amd64-framegrabber.deb
$ sudo dpkg -i ifm3d_0.2.0_amd64-image.deb
$ sudo dpkg -i ifm3d_0.2.0_amd64-tools.deb
```

You are now in position to install `ifm3d-ros`. Those instructions are
available on the main
[Readme](https://github.com/lovepark/ifm3d-ros#building-and-installing-the-software)
page.
