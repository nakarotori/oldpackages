#
# Copyright (C) 2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=openobex
PKG_VERSION:=1.7.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=git://gitorious.org/openobex/mainline.git
PKG_SOURCE_VERSION:=2e1c0fc5a8f5e41886141a6b402d00db735ccf49

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/openobex
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+libusb-1.0 +bluez-libs +udev +libxml2
  TITLE:=Free open source implementation of the Object Exchange (OBEX) protocol.
  URL:=https://gitorious.org/openobex
endef

CMAKE_OPTIONS += \
        -DCMAKE_BUILD_TYPE=MinSizeRel \
        -DBUILD_DOCUMENTATION=OFF

$(eval $(call BuildPackage,openobex))
