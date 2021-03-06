#
# Copyright (C) 2009-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gst1-plugins-ugly
PKG_VERSION:=1.0.7
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/gst-plugins-ugly-$(PKG_VERSION)
PKG_SOURCE:=gst-plugins-ugly-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://gstreamer.freedesktop.org/src/gst-plugins-ugly/
PKG_MD5SUM:=8754edf6c3be235f232fb75ad11708bb

PKG_BUILD_DEPENDS:= gstreamer1 gst1-plugins-base liboil
PKG_CONFIG_DEPENDS:= \
	CONFIG_PACKAGE_gst1-mod-asf \
	CONFIG_PACKAGE_gst1-mod-lame \
	CONFIG_PACKAGE_gst1-mod-mad \
	CONFIG_PACKAGE_gst1-mod-mpeg2dec \

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/gstreamer1/Default
  CATEGORY:=Multimedia
  SECTION:=multimedia
  TITLE:=GStreamer
  URL:=http://gstreamer.freedesktop.org/
endef

define Package/gstreamer1/description/Default
 GStreamer open source multimedia framework
endef


define Package/gst1-plugins-ugly
$(call Package/gstreamer1/Default)
  TITLE+= plugins collection (ugly)
  DEPENDS+= $(GST_DEPENDS)
endef

define Package/gts-plugins-ugly/description
$(call Package/gstreamer1/description/Default)
 .
 This meta package contains only dependencies to the other plugins from
 the ugly plugins collection.
endef


GST_COND_SELECT = $(patsubst %,$(if $(CONFIG_PACKAGE_gst1-mod-$(1)),--enable,--disable)-%,$(1))

GST_VERSION:=1.0

CONFIGURE_ARGS += \
	--disable-debug \
	--disable-examples \
	\
	--disable-a52dec \
	--disable-amrnb \
	--disable-amrwb \
	$(call GST_COND_SELECT,asf) \
	--disable-cdio \
	--disable-dvdlpcmdec \
	--disable-dvdread \
	--disable-dvdsub \
	--disable-iec958 \
	$(call GST_COND_SELECT,lame) \
	$(call GST_COND_SELECT,mad) \
	$(call GST_COND_SELECT,mpeg2dec) \
	--disable-mpegaudioparse \
	--disable-mpegstream \
	--disable-realmedia \
	--disable-sidplay \
	--disable-synaesthesia \
	--disable-twolame \
	--disable-x264 \
	\
	--without-libiconv-prefix \
	--without-libintl-prefix \

EXTRA_LDFLAGS+= \
	-Wl,-rpath-link=$(STAGING_DIR)/usr/lib \


define Package/gst1-plugins-ugly/install
	/bin/true
endef


# 1: short name
# 2: description
# 3: dependencies on other gstreamer libraries (short name)
# 4: dependencies on other gstreamer plugins (short name)
# 5: dependencies on other packages
define GstBuildPlugin

  GST_DEPENDS += +gst1-mod-$(1)

  define Package/gst1-mod-$(1)
    $(call Package/gstreamer1/Default)
    TITLE+= $(2) plugin (ugly)
    DEPENDS+= +libgstreamer1 $$(foreach p,$(3),+libgst1$$(p)) $$(foreach p,$(4),+gst1-mod-$$(p)) $(5)
  endef

  define Package/gst1-mod-$(1)/description
   $(call Package/gstreamer1/description/Default)
   .
   This package contains the GStreamer $(2) plugin.
  endef

  define Package/gst1-mod-$(1)/install
	$(INSTALL_DIR) $$(1)/usr/lib/gstreamer-$(GST_VERSION)
	( cd $(PKG_INSTALL_DIR); $(CP) \
		./usr/lib/gstreamer-$(GST_VERSION)/libgst$(1).so* \
		$$(1)/usr/lib/gstreamer-$(GST_VERSION)/ \
	)
  endef

  $$(eval $$(call BuildPackage,gst1-mod-$(1)))
endef

$(eval $(call GstBuildPlugin,asf,ASF demuxer,audio riff rtp rtsp sdp tag,,))
$(eval $(call GstBuildPlugin,lame,MP3 encoder (using LAME),audio,,+lame-lib))
$(eval $(call GstBuildPlugin,mad,MP3 decoder (using MAD),audio tag,,+libid3tag +libmad))
$(eval $(call GstBuildPlugin,mpeg2dec,MPEG decoder,video,,+libmpeg2))

$(eval $(call BuildPackage,gst1-plugins-ugly))
