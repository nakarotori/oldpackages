#
# Copyright (C) 2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libftdi
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://www.intra2net.com/en/developer/libftdi/download/
PKG_MD5SUM:=e02dd77ee10b82b5edfbb8c199185bbf

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libftdi
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libusb-compat
  TITLE:=library to talk to FTDI chips
  URL:=http://www.intra2net.com/en/developer/libftdi/
endef

define Package/libftdi/description
  libFTDI - FTDI USB driver with bitbang mode
  libFTDI is an open source library to talk to FTDI chips: FT232BM, FT245BM, FT2232C, FT2232H, FT4232H, FT2232D and FT245R, including the popular bitbang mode. 
  The library is linked with your program in userspace, no kernel driver required.
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/include/ftdi.h $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libftdi.{a,so} $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libftdi.so* $(1)/usr/lib/
endef

define Package/libftdi/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libftdi.so.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libftdi))
