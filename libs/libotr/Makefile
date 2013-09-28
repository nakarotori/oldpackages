include $(TOPDIR)/rules.mk

PKG_NAME:=libotr
PKG_VERSION:=3.2.1
PKG_RELEASE:=1
#PKG_VERSION:=4.0.0
#PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.cypherpunks.ca/otr/
PKG_MD5SUM:=974acf937d2ce0ee89b27a9815c17a3f
#PKG_MD5SUM:=00979dca82d70383fcd1b01f3974363c

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libotr/Default
  SECTION:=libs
  CATEGORY:=Libraries
  URL:=http://www.cypherpunks.ca/otr/
endef

define Package/libotr
  $(call Package/libotr/Default)
  DEPENDS:=+libgcrypt
  TITLE:=OTR Messaging Library
  MENU:=1
endef

define Package/libotr/description
Off-the-Record (OTR) Messaging allows you to have private conversations over
instant messaging.
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC='$(TARGET_CC) $(FPIC)' \
		CFLAGS='$(TARGET_CFLAGS) -Wall -D_GNU_SOURCE' \
		LDFLAGS='$(TARGET_LDFLAGS)' \
		all
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libotr $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libotr.{a,so*,la} $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/libotr.pc $(1)/usr/lib/pkgconfig/
endef

define Package/libotr/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libotr.so.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libotr))
