#
# Copyright (C) 2010-2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=chaosvpn
PKG_VERSION:=2.18

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://github.com/ryd/chaosvpn.git
PKG_REV:=2eb24810b5aa0b2d56f21562e52927020dc3090a
PKG_VERSION:=r20140124

PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)

include $(INCLUDE_DIR)/package.mk

define Package/chaosvpn
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Config generator for chaos vpn
  SUBMENU:=VPN
  DEPENDS:=+ip +tinc +kmod-tun +libopenssl
  URL:=https://wiki.hamburg.ccc.de/index.php/ChaosVPN::DebianHowto
  MAINTAINER:=Christopher J. Pilkington <cjp@0x1.net>
endef

define Package/chaosvpn/description
	Configure tincd for the chaosvpn network
endef

MAKE_FLAGS += \
	COPT="$(TARGET_CFLAGS) $(TARGET_CPPFLAGS) $(TARGET_LDFLAGS)"

define Package/chaosvpn/install
	$(INSTALL_DIR) $(1)/etc/tinc/chaos/ $(1)/usr/sbin/ $(1)/etc/init.d/ $(1)/etc/hotplug.d/iface/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/chaosvpn $(1)/usr/sbin/
	#$(INSTALL_DATA) $(PKG_BUILD_DIR)/chaosvpn.conf $(1)/etc/tinc/
	sed -e 's/"\/sbin\/ip /"\/usr\/sbin\/ip /' <$(PKG_BUILD_DIR)/chaosvpn.conf >$(1)/etc/tinc/chaosvpn.conf
	$(INSTALL_BIN) ./files/chaosvpn_config.sh $(1)/usr/sbin/
	$(INSTALL_BIN) ./files/chaosvpn.init $(1)/etc/init.d/chaosvpn
	$(INSTALL_BIN) ./files/chaosvpn.hotplug $(1)/etc/hotplug.d/iface/40-chaosvpn
endef

$(eval $(call BuildPackage,chaosvpn))

