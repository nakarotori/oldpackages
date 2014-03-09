#
# Copyright (C) 2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=jemalloc
PKG_VERSION:=3.5.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://www.canonware.com/download/jemalloc
PKG_MD5SUM:=43a6ce2f60d14d58c4b28b73b8b70cd2

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/jemalloc
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=malloc alternative
  URL:=http://www.canonware.com/jemalloc/index.html
endef

define Package/jemalloc/description
jemalloc is a general purpose malloc(3) implementation that emphasizes fragmentation avoidance and scalable concurrency support.
endef

define Package/jemalloc/InstallDev
	$(INSTALL_DIR) $(1)/usr/bin
endef

$(eval $(call BuildPackage,jemalloc))
