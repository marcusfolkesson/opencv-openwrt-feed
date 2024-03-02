# OpenCV OpenWRT feed

## Description


 OpenCV (Open Source Computer Vision Library) is an open source computer vision and machine learning software library.
 OpenCV was built to provide a common infrastructure for computer vision applications and to accelerate the use of machine perception
 in the commercial products. Being a BSD-licensed product, OpenCV makes it easy for businesses to utilize and modify the code.

- [Website](https://opencv.org/)

## Usage

This repository is intended to be layered on-top of an OpenWrt buildroot. If you do not have an OpenWrt buildroot installed, see the documentation at: [OpenWrt Buildroot – Installation](https://openwrt.org/docs/guide-developer/build-system/install-buildsystem) on the OpenWrt support site.

To install this feed and all its package definitions, run the following in your OpenWRT root-folder:
```
echo "src-git opencv https://github.com/marcusfolkesson/opencv-openwrt-feed.git" >> ./feeds.conf
./scripts/feeds update opencv
./scripts/feeds install -a -p opencv
```

# Patches

Please submit any patches against the opencv-openwrt-feed repository via pull request.


