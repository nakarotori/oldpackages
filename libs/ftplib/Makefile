#
# Copyright (C) 2008-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ftplib
PKG_VERSION:=4.0
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://nbpfaus.net/~pfau/ftplib
PKG_MD5SUM:=846c30323ee64850559cecb311118460

include $(INCLUDE_DIR)/package.mk

MAKE_PATH:=src

define Package/ftplib
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=ftplib
  URL:=http://nbpfaus.net/~pfau/ftplib/
endef

define Package/ftplib/description
ftplib is a set of routines that implement the FTP protocol. They allow
applications to create and access remote files through function calls instead
of needing to fork and exec an interactive ftp client program.
endef

MAKE_FLAGS += \
	DEFINES="$(TARGET_CFLAGS)"

define Build/Compile
	$(call Build/Compile/Default,all)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/src/ftplib.h $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/src/libftp.{so*,a} $(1)/usr/lib/
endef

define Package/ftplib/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/src/libftp.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,ftplib))
