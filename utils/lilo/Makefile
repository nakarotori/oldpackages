#
# Copyright (C) 2006-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=lilo
PKG_VERSION:=24.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://alioth.debian.org/frs/download.php/file/3922
PKG_MD5SUM:=03d7090835a5675314082847f1ac7910

include $(INCLUDE_DIR)/package.mk

define Package/lilo
  SECTION:=base
  CATEGORY:=Boot Loaders
  DEPENDS:=@TARGET_x86
  TITLE:=lilo
  URL:=ftp://metalab.unc.edu/pub/Linux/system/boot/lilo/
endef

define Package/lilo/conffiles
/etc/lilo.conf
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC="$(HOSTCC) -m32" \
		alles
endef

define Package/lilo/install
	$(INSTALL_DIR) $(1)/sbin
	$(CP) $(PKG_BUILD_DIR)/lilo.static $(1)/sbin/lilo
	$(INSTALL_DIR) $(1)/etc
	$(CP) ./files/lilo.conf $(1)/etc/
	$(CP) ./files/boot.msg $(1)/etc/
endef

$(foreach command, as86 ld86, \
  $(eval $(call RequireCommand,$(command), \
   $(PKG_NAME) requires $(command). \
  )) \
)

$(eval $(call BuildPackage,lilo))

