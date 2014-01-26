#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=dosfstools
PKG_VERSION:=3.0.25
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://daniel-baumann.ch/files/software/dosfstools \
		http://fossies.org/linux/misc
PKG_MD5SUM:=bd73002ace02d8e6cfc7c4696b8098e9

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
ICONV_FULL:=1

define Package/dosfstools/Default
  SECTION:=utils
  CATEGORY:=Utilities
  URL:=http://www.daniel-baumann.ch/software/dosfstools/
  SUBMENU:=Filesystem
  DEPENDS:=$(ICONV_DEPENDS)
endef

define Package/dosfsck
  $(call Package/dosfstools/Default)
  TITLE:=dosfstools-fsck.fat
endef

define Package/dosfslabel
  $(call Package/dosfstools/Default)
  TITLE:=dosfstools-fatlabel
endef

define Package/mkdosfs
  $(call Package/dosfstools/Default)
  TITLE:=dosfstools-mkfs.fat
endef

define Package/dosfsck/description
	Utilities to create and check MS-DOS FAT filesystems.
	(fsck.vfat and fsck.fat for checking integrity of FAT volumes)
endef

define Package/dosfslabel/description
	Utilities to create and check MS-DOS FAT filesystems.
	(fatlabel for reading and writing labels of FAT volumes)
endef

define Package/mkdosfs/description
	Utilities to create and check MS-DOS FAT filesystems.
	(mkfs.vfat and mkfs.fat for creating FAT volumes)
endef

LDFLAGS+=$(ICONV_LDFLAGS) $(TARGET_LDFLAGS) -L$(STAGING_DIR)/usr/lib/libiconv-full/lib -liconv

define Build/Configure
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		$(TARGET_CONFIGURE_OPTS) \
		OPTFLAGS="$(TARGET_CFLAGS) -D_FILE_OFFSET_BITS=64" \
		PREFIX="/usr" \
		SBINDIR="/usr/sbin" \
		LDFLAGS="$(LDFLAGS)" \
		all
	$(MAKE) -C $(PKG_BUILD_DIR) \
		$(TARGET_CONFIGURE_OPTS) \
		OPTFLAGS="$(TARGET_CFLAGS) -D_FILE_OFFSET_BITS=64" \
		PREFIX="$(PKG_INSTALL_DIR)/usr" \
		SBINDIR="$(PKG_INSTALL_DIR)/usr/sbin" \
		install-bin
endef

define Package/dosfsck/install
	$(INSTALL_DIR) $(1)/lib/functions/fsck
	$(INSTALL_DATA) ./files/dosfsck.sh $(1)/lib/functions/fsck/
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/fsck.fat $(1)/usr/sbin/
	(cd $(1)/usr/sbin; ln -sf fsck.fat fsck.msdos; ln -sf fsckfat fsck.vfat)
endef

define Package/dosfslabel/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/fatlabel $(1)/usr/sbin/
endef

define Package/mkdosfs/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/mkfs.fat $(1)/usr/sbin/
	(cd $(1)/usr/sbin; ln -sf mkfs.fat mkfs.msdos; ln -sf mkfs.fat mkfs.vfat)
endef

$(eval $(call BuildPackage,dosfsck))
$(eval $(call BuildPackage,dosfslabel))
$(eval $(call BuildPackage,mkdosfs))
