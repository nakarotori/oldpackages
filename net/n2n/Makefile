#
# Copyright (C) 2007-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_BRANCH:=trunk
PKG_SOURCE_URL:=https://svn.ntop.org/svn/ntop/trunk/n2n
PKG_REV:=3875

PKG_NAME:=n2n
PKG_VERSION:=$(PKG_REV)
PKG_RELEASE:=4

PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.gz
PKG_SOURCE_PROTO:=svn
PKG_SOURCE_VERSION:=$(PKG_REV)

PKG_CHECK_FORMAT_SECURITY:=0

include $(INCLUDE_DIR)/package.mk

define Package/n2n
  SECTION:=net
  CATEGORY:=Network
  TITLE:=VPN tunneling daemon
  URL:=http://www.ntop.org/n2n/
  SUBMENU:=VPN
  DEPENDS:=+libpthread +kmod-tun
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		$(TARGET_CONFIGURE_OPTS) \
		CFLAGS="$(TARGET_CFLAGS)" \
		INSTALL_PROG=":"
endef

define Package/n2n/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/edge $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/supernode $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DATA) ./files/n2n.config $(1)/etc/config/n2n
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/n2n.init $(1)/etc/init.d/n2n
endef

define Package/n2n/conffiles
/etc/config/n2n
endef

$(eval $(call BuildPackage,n2n))
