#
# Copyright (C) 2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ussp-push
PKG_VERSION:=0.11
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://xmailserver.org
PKG_MD5SUM:=5c44983ee27809867041feff6bb4423a

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/ussp-push
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+openobex +bluez-libs
  TITLE:=ussp-push is a OBEX object pusher for Linux, using the BlueZ BlueTooth stack.
  URL:=http://xmailserver.org/ussp-push.html
endef

define Build/Configure
	$(call Build/Configure/Default,--with-linux-headers=$(LINUX_DIR))
endef

define Package/ussp-push/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/ussp-push $(1)/usr/bin/
endef


$(eval $(call BuildPackage,ussp-push))
