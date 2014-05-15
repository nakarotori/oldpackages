#
# Copyright (C) 2007-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libatomicops
PKG_VERSION:=8c4daf9edfae755c09267d8a3fbd1fbd4f22a464
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/ivmai/libatomic_ops
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=8c4daf9edfae755c09267d8a3fbd1fbd4f22a464
PKG_RELEASE:=$(PKG_SOURCE_VERSION)

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk

define Package/libatomicops
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=implementations for atomic memory update operations
  DEPENDS:=@!TARGET_avr32
  URL:=http://www.hpl.hp.com/research/linux/atomic_ops/
endef

define Package/libatomicops/description
  Provides implementations for atomic memory update
  operations on a number of architectures. This allows
  direct use of these in reasonably portable code. Unlike
  earlier similar packages, this one explicitly considers
  memory barrier semantics, and allows the construction of
  code that involves minimum overhead across a variety of
  architectures.
endef

TARGET_CFLAGS += $(FPIC)

CONFIGURE_ARGS += \
	--enable-shared \
	--enable-static \

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
	$(CP) $(PKG_BUILD_DIR)/src/atomic_ops $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libatomic_ops*.a $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libatomicops))
