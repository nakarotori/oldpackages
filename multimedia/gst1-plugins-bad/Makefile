#
# Copyright (C) 2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gst1-plugins-bad
PKG_VERSION:=1.0.7
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/gst-plugins-bad-$(PKG_VERSION)
PKG_SOURCE:=gst-plugins-bad-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://gstreamer.freedesktop.org/src/gst-plugins-bad/
PKG_MD5SUM:=d1493d1219b836a8cbf54f4fba962420

PKG_BUILD_DEPENDS:= gstreamer1 gst1-plugins-base liboil

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


define Package/gst1-plugins-bad
$(call Package/gstreamer1/Default)
  TITLE+= plugins collection (bad)
  DEPENDS+= $(GST_DEPENDS)
endef

define Package/gts1-plugins-bad/description
$(call Package/gstreamer1/description/Default)
 .
 This meta package contains only dependencies to the other plugins from
 the bad plugins collection.
endef


GST_VERSION:=1.0

CONFIGURE_ARGS += \
	--disable-debug \
	--disable-examples \
	--disable-nls	\
	\
	--disable-directsound \
	--disable-directdraw \
	--disable-osx_video \
	--disable-quicktime \
	--disable-vcd \
	--disable-alsa \
	--disable-assrender \
	--disable-amrwb \
	--disable-apexsink \
	--disable-bz2 \
	--disable-cdaudio \
	--disable-celt \
	--disable-cog \
	--disable-dc1394 \
	--disable-directfb \
	--disable-dirac \
	--disable-dts \
	--disable-divx \
	--disable-resindvd \
	--disable-metadata \
	--disable-faac \
	--disable-faad \
	--disable-fbdev \
	--disable-flite \
	--disable-gsm \
	--disable-jack \
	--disable-jp2k \
	--disable-kate \
	--disable-ladspa \
	--disable-lv2 \
	--disable-modplug \
	--disable-mimic \
	--disable-libmms \
	--disable-mpeg2enc \
	--disable-mplex \
	--disable-musepack \
	--disable-musicbrainz \
	--disable-mythtv \
	--disable-nas \
	--disable-neon \
	--disable-ofa \
	--disable-rsvg \
	--disable-timidity \
	--disable-wildmidi \
	--disable-sdl \
	--disable-sdltest \
	--disable-sndfile \
	--disable-soundtouch \
	--disable-spc \
	--disable-gme \
	--disable-swfdec \
	--disable-theoradec \
	--disable-xvid \
	--disable-dvb \
	--disable-wininet \
	--disable-acm \
	--disable-vdpau \
	--disable-schro \
	--disable-zbar \
	--disable-vp8 \
	--disable-librfb \
	\
	--without-libiconv-prefix \
	--without-libintl-prefix \
	--without-x \

EXTRA_LDFLAGS+= \
	-Wl,-rpath-link=$(STAGING_DIR)/usr/lib \


define Package/gst1-plugins-ugly/install
	/bin/true
endef

# 1: short name
# 2: description
# 3: dependencies on other gstreamer libraries (short name)
# 4: dependencies on other packages
define GstBuildLibrary

  GST_DEPENDS += +libgst1$(1)

  define Package/libgst1$(1)
    $(call Package/gstreamer1/Default)
    TITLE+= $(2) library (base)
    DEPENDS+= +libgstreamer1 $$(foreach p,$(3),+libgst1$$(p)) $(4)
  endef

  define Package/libgst1$(1)/description
   $(call Package/gstreamer1/description/Default)
   .
   This package contains the GStreamer $(2) library.
  endef

  define Package/libgst1$(1)/install
	$(INSTALL_DIR) $$(1)/usr/lib
	( cd $(PKG_INSTALL_DIR); $(CP) \
		./usr/lib/libgst$(1)-$(GST_VERSION).so.* \
		$$(1)/usr/lib/ \
	)
  endef

  $$(eval $$(call BuildPackage,libgst1$(1)))
endef
$(eval $(call GstBuildLibrary,photography,photography,,))


# 1: short name
# 2: description
# 3: dependencies on other gstreamer libraries (short name)
# 4: dependencies on other gstreamer plugins (short name)
# 5: dependencies on other packages
define GstBuildPlugin

  GST_DEPENDS += +gst1-mod-$(1)

  define Package/gst1-mod-$(1)
    $(call Package/gstreamer1/Default)
    TITLE+= $(2) plugin (bad)
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

$(eval $(call GstBuildPlugin,adpcmdec,adpcm decoding support,audio,,))
$(eval $(call GstBuildPlugin,adpcmenc,adpcm encoding support,audio,,))
$(eval $(call GstBuildPlugin,asfmux,asf muxing support,rtp,,))
$(eval $(call GstBuildPlugin,autoconvert,autoconvert support,,,))
$(eval $(call GstBuildPlugin,camerabin2,camerabin support,photography basecamerabinsrc app pbutils tag,,@BROKEN))
$(eval $(call GstBuildPlugin,bayer,bayer support,video,,))
$(eval $(call GstBuildPlugin,dataurisrc,dataurisrc support,,,))
$(eval $(call GstBuildPlugin,debugutilsbad,debugutilsbad support,video,,))
$(eval $(call GstBuildPlugin,dtmf,dtmf support,rtp,,))
$(eval $(call GstBuildPlugin,dvdspu,dvdspu support,video,,))
$(eval $(call GstBuildPlugin,festival,festival support,audio,,))
$(eval $(call GstBuildPlugin,frei0r,frei0r support,controller video,,))
$(eval $(call GstBuildPlugin,id3tag,id3tag support,tag,,))
$(eval $(call GstBuildPlugin,jpegformat,jpegformat support,tag,,))
$(eval $(call GstBuildPlugin,liveadder,liveadder support,audio,,))
$(eval $(call GstBuildPlugin,mpegtsmux,mpegtsmux support,video,,))
$(eval $(call GstBuildPlugin,mpegpsmux,mpegpsmux support,,,))
$(eval $(call GstBuildPlugin,mpeg4videoparsersbad,mpeg4videoparsersbad esupport,,,))
$(eval $(call GstBuildPlugin,pcapparse,pcapparse support,,,))
$(eval $(call GstBuildPlugin,pnm,pnm support,video,,))
$(eval $(call GstBuildPlugin,rawparse,rawparse support,audio video,,))
$(eval $(call GstBuildPlugin,rtpmux,rtpmux support,rtp,,))
$(eval $(call GstBuildPlugin,scaletempoplugin,scaletempo support,audio,,))
$(eval $(call GstBuildPlugin,sdpelem,sdp support,rtp sdp,,))
$(eval $(call GstBuildPlugin,segmentclip,segmentclip support,audio,,))
$(eval $(call GstBuildPlugin,siren,siren support,audio rtp,,))
$(eval $(call GstBuildPlugin,speed,speed support,audio,,))
$(eval $(call GstBuildPlugin,subenc,subenc support,controller,,))

$(eval $(call BuildPackage,gst1-plugins-bad))
