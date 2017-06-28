---
layout: post
title: "Updating to GCC 4.8 in Ubuntu 12"
date: 2015-06-08
categories:
  - C++
description: 
image: 
image-sm: 
---

If you run Ubuntu 12 or any other old distro, you are probably missing most of the latest C++11 features! This is how you can update gcc to a more recent, more C++11-ish version.

First of all, check your current gcc version by doing 

```
gcc -v
```

Ubuntu 12 ships with GCC v4.6 by default. Fortunately, the aptitude repos include a newer version too: 

```
sudo apt-get install gcc-4.8
sudo apt-get install g++-4.8
```

Once installed, you must configure 4.8 as the default version:

```
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 20
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.8 20
sudo update-alternatives --config gcc
sudo update-alternatives --config g++
```

While this is the simplest way of getting a newer, cooler version of GCC in Ubuntu 12, you can follow the same procedure to update gcc in other Ubuntu versions (e.g. to gcc 4.9 in Ubuntu 14). 
