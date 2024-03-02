# Copyright (C) 2024 Fusion CCTV, Inc.
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=opencv
PKG_VERSION:=4.9.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/opencv/opencv.git
PKG_SOURCE_VERSION:=dad8af6b17f8e60d7b95a1203a1b4d22f56574cf

PKG_MAINTAINER:= Marcus Folkesson <marcus.folkesson@gmail.com>
PKG_LICENSE:=BSD-3-Clause
PKG_LICENSE_FILES:=LICENSE

PKG_INSTALL:=1
CMAKE_INSTALL:=1
CMAKE_BINARY_SUBDIR:=build
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

# We need to include python3-package.mk for the python variables
# but we are not a python package, so set PYTHON3_PKG_BUILD.
PYTHON3_PKG_BUILD:=0

PKG_BUILD_DEPENDS:= \
  	+PACKAGE_opencv-python:python3/host \
  	+PACKAGE_opencv-python:python3-dev

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/opencv/Default/description
 OpenCV (Open Source Computer Vision Library) is an open source computer
 vision and machine learning software library. OpenCV was built to provide
 a common infrastructure for computer vision applications and to accelerate
 the use of machine perception in the commercial products. Being a
 BSD-licensed product, OpenCV makes it easy for businesses to utilize
 and modify the code.
endef

define Package/opencv/default
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=OpenCV
  URL:=https://opencv.org/
  DEPENDS:= \
  	+libpthread +librt +libatomic +libstdcpp +zlib +libjpeg +libwebp \
  	+PACKAGE_opencv-ffmpeg:ffmpeg \
  	+PACKAGE_opencv-ffmpeg:bzip2 \
  	+PACKAGE_opencv-ffmpeg:libffmpeg-full \
  	+PACKAGE_opencv-jpeg:libjpeg \
  	+PACKAGE_opencv-python:python3-numpy \
  	+PACKAGE_opencv-python:python3-numpy-src \
  	+PACKAGE_opencv-v4l:libv4l \
  	+PACKAGE_opencv-v4l:libv4l \
  	+PACKAGE_opencv-tiff:libtiff \
  	+PACKAGE_opencv-png:libpng \
  	+PACKAGE_opencv-gstreamer:gstreamer1
endef

define Package/opencv
	$(call Package/opencv/default)
endef

define Package/opencv-ffmpeg
	$(call Package/opencv/default)
	DEPENDS+=+opencv
	TITLE+= with ffmpeg
endef

define Package/opencv-jpeg
	$(call Package/opencv/default)
	DEPENDS+=opencv
	TITLE+= with jpeg
endef

define Package/opencv-python
	$(call Package/opencv/default)
	DEPENDS+=+opencv
	TITLE+= with python bindings
endef

define Package/opencv-v4l
	$(call Package/opencv/default)
	DEPENDS+=+opencv
	TITLE+= with v4l
endef

define Package/opencv-tiff
	$(call Package/opencv/default)
	DEPENDS+=+opencv
	TITLE+= with tiff 
endef

define Package/opencv-png
	$(call Package/opencv/default)
	DEPENDS+=+opencv
	TITLE+= with png
endef

define Package/opencv-gstreamer
	$(call Package/opencv/default)
	DEPENDS+=+opencv
	TITLE+= with gstreamer
endef

define Package/opencv-protobuf
	$(call Package/opencv/default)
	DEPENDS+=+opencv
	TITLE+= with protobuf
endef

ifeq ($(CONFIG_PACKAGE_opencv-ffmpeg),y)
	CMAKE_OPTIONS += -DWITH_FFMPEG=ON
else
	CMAKE_OPTIONS += -DWITH_FFMPEG=OFF
endif

ifeq ($(CONFIG_PACKAGE_opencv-jpeg),y)
	CMAKE_OPTIONS += \
		-DWITH_JPEG=ON \
		-DBUILD_OPENJPEG=ON \
		-DBUILD_JPEG=ON
else
	CMAKE_OPTIONS += \
		-DWITH_JPEG=OFF \
		-DBUILD_OPENJPEG=OFF \
		-DBUILD_JPEG=OFF
endif

ifeq ($(CONFIG_PACKAGE_opencv-python),y)
	CMAKE_OPTIONS += \
	-DBUILD_opencv_python2=OFF \
	-DBUILD_opencv_python3=ON \
	-DPYTHON3_INCLUDE_PATH=$(STAGING_DIR)/usr/include/python$(PYTHON3_VERSION) \
	-DPYTHON3_LIBRARIES=$(STAGING_DIR)/usr/lib/libpython$(PYTHON3_VERSION).so \
	-DPYTHON3_NUMPY_INCLUDE_DIRS=$(STAGING_DIR_ROOT)/usr/lib/python$(PYTHON3_VERSION)/site-packages/numpy/core/include \
	-DPYTHON3_PACKAGES_PATH=/usr/lib/python$(PYTHON3_VERSION)/site-packages
else
	CMAKE_OPTIONS += \
	-DBUILD_opencv_python2=OFF \
	-DBUILD_opencv_python3=OFF
endif

ifeq ($(CONFIG_PACKAGE_opencv-v4l),y)
	CMAKE_OPTIONS += \
		-DWITH_LIBV4L=ON \
		-DWITH_v4L=ON
else
	CMAKE_OPTIONS += \
		-DWITH_LIBV4L=OFF \
		-DWITH_v4L=OFF
endif

ifeq ($(CONFIG_PACKAGE_opencv-tiff),y)
	CMAKE_OPTIONS += \
		-DWITH_TIFF=ON
else
	CMAKE_OPTIONS += \
		-DWITH_TIFF=OFF
endif

ifeq ($(CONFIG_PACKAGE_opencv-png),y)
	CMAKE_OPTIONS += \
		-DWITH_PNG=ON
else
	CMAKE_OPTIONS += \
		-DWITH_PNG=OFF
endif

ifeq ($(CONFIG_PACKAGE_opencv-gstreamer),y)
	CMAKE_OPTIONS += \
		-DWITH_GSTREAMER=ON
else
	CMAKE_OPTIONS += \
		-DWITH_GSTREAMER=OFF
endif

ifeq ($(CONFIG_PACKAGE_opencv-protobuf),y)
	CMAKE_OPTIONS += \
		-DBUILD_PROTOBUF=ON \
		-DWITH_PROTOBUF=ON
else
	CMAKE_OPTIONS += \
		-DBUILD_PROTOBUF=OFF \
		-DWITH_PROTOBUF=OFF
endif

# OpenCV component options
CMAKE_OPTIONS += \
	-DBUILD_opencv_freetype=ON \
	-DBUILD_DOCS=OFF \
	-DBUILD_PERF_TESTS=OFF \
	-DBUILD_TESTS=OFF \
	-DBUILD_WITH_DEBUG_INFO=OFF \
	-DDOWNLOAD_EXTERNAL_TEST_DATA=OFF \
	-DOPENCV_GENERATE_PKGCONFIG=ON \
	-DCMAKE_VERBOSE=OFF \
	-DOPENCV_ENABLE_PKG_CONFIG=ON

# OpenCV build options
CMAKE_OPTIONS += \
	-DBUILD_WITH_STATIC_CRT=OFF \
	-DENABLE_CCACHE=OFF \
	-DENABLE_COVERAGE=OFF \
	-DENABLE_FAST_MATH=ON \
	-DENABLE_IMPL_COLLECTION=OFF \
	-DENABLE_NOISY_WARNINGS=OFF \
	-DENABLE_OMIT_FRAME_POINTER=ON \
	-DENABLE_PRECOMPILED_HEADERS=OFF \
	-DENABLE_PROFILING=OFF \
	-DOPENCV_WARNINGS_ARE_ERRORS=OFF \
	-DBUILD_opencv_gpu=OFF \
	-DWITH_1394=OFF -DBUILD_opencv_stitching=OFF \
	-DBUILD_opencv_superres=OFF -DBUILD_opencv_ts=OFF \
	-DBUILD_opencv_highgui=OFF \
	-DBUILD_opencv_videostab=OFF \
	-DWITH_GTK=OFF

# OpenCV link options
CMAKE_OPTIONS += \
	-DCMAKE_INSTALL_RPATH_USE_LINK_PATH=OFF \
	-DCMAKE_SKIP_RPATH=OFF \
	-DCMAKE_USE_RELATIVE_PATHS=OFF

# OpenCV packaging options:
CMAKE_OPTIONS += \
	-DBUILD_PACKAGE=OFF \
	-DENABLE_SOLUTION_FOLDERS=OFF \
	-DINSTALL_CREATE_DISTRIB=OFF

# Cuda stuff
CMAKE_OPTIONS += \
	-DBUILD_CUDA_STUBS=OFF \
	-DBUILD_opencv_cudaarithm=OFF \
	-DBUILD_opencv_cudabgsegm=OFF \
	-DBUILD_opencv_cudacodec=OFF \
	-DBUILD_opencv_cudafeatures2d=OFF \
	-DBUILD_opencv_cudafilters=OFF \
	-DBUILD_opencv_cudaimgproc=OFF \
	-DBUILD_opencv_cudalegacy=OFF \
	-DBUILD_opencv_cudaobjdetect=OFF \
	-DBUILD_opencv_cudaoptflow=OFF \
	-DBUILD_opencv_cudastereo=OFF \
	-DBUILD_opencv_cudawarping=OFF \
	-DBUILD_opencv_cudev=OFF \
	-DWITH_CUBLAS=OFF \
	-DWITH_CUDA=OFF \
	-DWITH_CUFFT=OFF

# NVidia stuff
CMAKE_OPTIONS += \
	-DWITH_NVCUVID=OFF \
	-DWITH_CAROTENE=OFF

# AMD stuff
CMAKE_OPTIONS += \
	-DWITH_OPENCLAMDBLAS=OFF \
	-DWITH_OPENCLAMDFFT=OFF

# Intel stuff
CMAKE_OPTIONS += \
	-DBUILD_WITH_DYNAMIC_IPP=OFF \
	-DWITH_INTELPERC=OFF \
	-DWITH_IPP=OFF \
	-DWITH_IPP_A=OFF

# Smartek stuff
CMAKE_OPTIONS += -DWITH_GIGEAPI=OFF

# Prosilica stuff
CMAKE_OPTIONS += -DWITH_PVAPI=OFF

# Ximea stuff
CMAKE_OPTIONS += -DWITH_XIMEA=OFF

# Non-Linux support (Android options) must remain OFF:
CMAKE_OPTIONS += \
	-DANDROID=OFF \
	-DBUILD_ANDROID_CAMERA_WRAPPER=OFF \
	-DBUILD_ANDROID_EXAMPLES=OFF \
	-DBUILD_ANDROID_SERVICE=OFF \
	-DBUILD_FAT_JAVA_LIB=OFF \
	-DINSTALL_ANDROID_EXAMPLES=OFF \
	-DWITH_ANDROID_CAMERA=OFF

# Non-Linux support (Mac OSX options) must remain OFF:
CMAKE_OPTIONS += \
	-DWITH_AVFOUNDATION=OFF \
	-DWITH_CARBON=OFF \
	-DWITH_QUICKTIME=OFF

# Non-Linux support (Windows options) must remain OFF:
CMAKE_OPTIONS += \
	-DWITH_CSTRIPES=OFF \
	-DWITH_DSHOW=OFF \
	-DWITH_MSMF=OFF \
	-DWITH_VFW=OFF \
	-DWITH_VIDEOINPUT=OFF \
	-DWITH_WIN32UI=OFF

# Software/3rd-party support options:
CMAKE_OPTIONS += \
	-DBUILD_EXAMPLES=OFF \
	-DBUILD_JASPER=OFF \
	-DBUILD_OPENEXR=OFF \
	-DBUILD_PNG=OFF \
	-DBUILD_TIFF=OFF \
	-DBUILD_ZLIB=OFF \
	-DINSTALL_C_EXAMPLES=OFF \
	-DINSTALL_PYTHON_EXAMPLES=OFF \
	-DINSTALL_TO_MANGLED_PATHS=OFF

# Disabled features (mostly because they are not available in OpenWRT)
CMAKE_OPTIONS += \
	-DWITH_1394=OFF \
	-DWITH_CLP=OFF \
	-DWITH_GDAL=OFF \
	-DWITH_GPHOTO2=OFF \
	-DWITH_GSTREAMER_0_10=OFF \
	-DWITH_LAPACK=OFF \
	-DWITH_MATLAB=OFF \
	-DWITH_OPENCL=OFF \
	-DWITH_OPENCL_SVM=OFF \
	-DWITH_OPENEXR=OFF \
	-DWITH_OPENNI2=OFF \
	-DWITH_OPENNI=OFF \
	-DWITH_UNICAP=OFF \
	-DWITH_VA=OFF \
	-DWITH_VA_INTEL=OFF \
	-DWITH_VTK=OFF \
	-DWITH_XINE=OFF

TARGET_LDFLAGS += -latomic

define Package/opencv/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libopencv* $(1)/usr/lib/
endef

define Package/opencv-python/install
	$(INSTALL_DIR) $(1)$(PYTHON3_PKG_DIR)
	cp -r  $(PKG_INSTALL_DIR)$(PYTHON3_PKG_DIR)/cv2 $(1)$(PYTHON3_PKG_DIR)/cv2
	mv $(1)$(PYTHON3_PKG_DIR)/cv2/python-$(PYTHON3_VERSION)/cv2.cpython-*.so \
		$(1)$(PYTHON3_PKG_DIR)/cv2/python-$(PYTHON3_VERSION)/cv2.cpython-$(PYTHON3_VERSION).so
endef

Package/opencv-ffmpeg/install = $(Package/opencv/install)
Package/opencv-jpeg/install = $(Package/opencv/install)
Package/opencv-v4l/install = $(Package/opencv/install)
Package/opencv-tiff/install = $(Package/opencv/install)
Package/opencv-png/install = $(Package/opencv/install)
Package/opencv-gstreamer/install = $(Package/opencv/install)
Package/opencv-protobuf/install = $(Package/opencv/install)

$(eval $(call BuildPackage,opencv))
$(eval $(call BuildPackage,opencv-ffmpeg))
$(eval $(call BuildPackage,opencv-jpeg))
$(eval $(call BuildPackage,opencv-python))
$(eval $(call BuildPackage,opencv-v4l))
$(eval $(call BuildPackage,opencv-tiff))
$(eval $(call BuildPackage,opencv-png))
$(eval $(call BuildPackage,opencv-gstreamer))
$(eval $(call BuildPackage,opencv-protobuf))
