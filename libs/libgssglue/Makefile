#
# Copyright (C) 2007-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libgssglue
PKG_VERSION:=0.4
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.citi.umich.edu/projects/nfsv4/linux/libgssglue
PKG_MD5SUM:=088797f3180702fa54e786496b32e750

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/libgssglue
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=required libraries for the nfs-utils
  URL:=http://www.citi.umich.edu/projects/nfsv4/linux
endef

define Package/libgssglue/description
 Support libraries - for newer nfs mount command (nfs4)
endef

TARGET_CFLAGS += -I$(PKG_BUILD_DIR)/lib $(FPIC)

MAKE_FLAGS += \
	OPT="$(TARGET_CFLAGS)" \
	INSTALLSUID="install -m 4755" \
	DESTDIR="$(PKG_INSTALL_DIR)"

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/gssglue/gssapi
	$(CP) $(PKG_INSTALL_DIR)/usr/include/gssglue/gssapi/gssapi.h $(1)/usr/include/gssglue/gssapi
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libgssglue.{a,so*} $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/libgssglue.pc $(1)/usr/lib/pkgconfig
endef

$(eval $(call BuildPackage,libgssglue))
