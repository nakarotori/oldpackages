#
# Copyright (C) 2006-2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ffmpeg
PKG_VERSION:=2.1.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://ffmpeg.org/releases/
PKG_MD5SUM:=711b795bbc7b527c0f4a1828f324fd5a

PKG_LICENSE:=LGPLv2.1+ GPLv2+ LGPLv3
PKG_LICENSE_FILES:=COPYING.GPLv2 COPYING.GPLv3 COPYING.LGPLv2.1 COPYING.LGPLv3

FFMPEG_CUSTOM_ENCODERS:= \
	ac3 \
	jpegls \
	mpeg1video \
	mpeg2video \
	mpeg4 \
	pcm_s16be \
	pcm_s16le \
	png \
	vorbis \
	zlib \

FFMPEG_CUSTOM_DECODERS:= \
	aac \
	ac3 \
	atrac3 \
	flac \
	gif \
	h264 \
	jpegls \
	mp2 \
	mp3 \
	mpeg1video \
	mpeg2video \
	mpeg4 \
	mpegvideo \
	pcm_s16be \
	pcm_s16le \
	png \
	vorbis \
	wmav1 \
	wmav2 \
	zlib \

FFMPEG_CUSTOM_MUXERS:= \
	ac3 \
	ffm \
	h264 \
	mp3 \
	mp4 \
	mpeg1video \
	mpeg2video \
	mpegts \
	ogg \
	rtp \

FFMPEG_CUSTOM_DEMUXERS:= \
	aac \
	ac3 \
	avi \
	flac \
	ffm \
	h264 \
	matroska \
	mov \
	mp3 \
	mpegps \
	mpegts \
	mpegvideo \
	ogg \
	rm \
	rtsp \
	sdp \
	v4l2 \

FFMPEG_CUSTOM_PARSERS:= \
	aac \
	ac3 \
	h264 \
	mpegaudio \
	mpeg4video \
	mpegvideo \

FFMPEG_CUSTOM_PROTOCOLS:= \
	file http pipe rtp tcp udp

FFMPEG_MINI_ENCODERS:= \

FFMPEG_MINI_DECODERS:= \
	aac \
	ac3 \
	atrac3 \
	flac \
	h263 \
	h264 \
	jpegls \
	mp3 \
	mpeg1video \
	mpeg2video \
	mpeg4 \
	mpegvideo \
	png \
	wmav1 \
	wmav2 \

FFMPEG_MINI_MUXERS:= \
	ffm \

FFMPEG_MINI_DEMUXERS := \
	aac \
	ac3 \
	asf \
	avi \
	ffm \
	flac \
	h264 \
	matroska \
	mov \
	mp3 \
	mpegts \
	mpegvideo \
	rtsp \

FFMPEG_MINI_PARSERS:= \
	ac3 \
	flac \
	h263 \
	h264 \
	mpeg4video \
	mpegaudio \

FFMPEG_MINI_PROTOCOLS := \
	file http rtp tcp udp \

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(BUILD_VARIANT)/$(PKG_NAME)-$(PKG_VERSION)

PKG_CONFIG_DEPENDS:= \
	$(patsubst %,CONFIG_FFMPEG_CUSTOM_ENCODER_%,$(FFMPEG_CUSTOM_ENCODERS)) \
	$(patsubst %,CONFIG_FFMPEG_CUSTOM_DECODER_%,$(FFMPEG_CUSTOM_DECODERS)) \
	$(patsubst %,CONFIG_FFMPEG_CUSTOM_MUXER_%,$(FFMPEG_CUSTOM_DEMUXERS)) \
	$(patsubst %,CONFIG_FFMPEG_CUSTOM_DEMUXER_%,$(FFMPEG_CUSTOM_DEMUXERS)) \
	$(patsubst %,CONFIG_FFMPEG_CUSTOM_PARSER_%,$(FFMPEG_CUSTOM_PARSERS)) \
	$(patsubst %,CONFIG_FFMPEG_CUSTOM_PROTOCOL_%,$(FFMPEG_CUSTOM_PROTOCOLS))

include $(INCLUDE_DIR)/package.mk

define Package/ffmpeg2/Default
 TITLE:=FFmpeg
 URL:=http://ffmpeg.mplayerhq.hu/
endef

define Package/ffmpeg2/Default/description
 FFmpeg is a a software package that can record, convert and stream digital
 audio and video in numerous formats.
endef


define Package/ffmpeg2
$(call Package/ffmpeg2/Default)
 SECTION:=multimedia
 CATEGORY:=Multimedia
 TITLE+= program
 DEPENDS+= +libpthread +libffmpeg2-full
 VARIANT:=full
endef

define Package/ffmpeg2/description
$(call Package/ffmpeg2/Default/description)
 .
 This package contains the FFmpeg command line tool.
endef


define Package/ffprobe2
$(call Package/ffmpeg2/Default)
 SECTION:=multimedia
 CATEGORY:=Multimedia
 TITLE+= CLI media identifier
 DEPENDS+= +libffmpeg2-full
 VARIANT:=full
endef

define Package/ffprobe2/description
$(call Package/ffmpeg2/Default/description)
 .
 This package contains the FFprobe command line tool.
endef


define Package/ffserver2
$(call Package/ffserver2/Default)
 SECTION:=multimedia
 CATEGORY:=Multimedia
 TITLE+= streaming server
 DEPENDS+= +libpthread +libffmpeg2-full
 VARIANT:=full
endef

define Package/ffserver2/description
$(call Package/ffmpeg2/Default/description)
 .
 This package contains the FFmpeg streaming server.
endef


define Package/libffmpeg2/Default
$(call Package/ffmpeg2/Default)
 SECTION:=libs
 CATEGORY:=Libraries
 TITLE+= libraries
 DEPENDS+= +libpthread +zlib +libbz2
 PROVIDES:= libffmpeg2
endef


define Package/libffmpeg2-custom
$(call Package/libffmpeg2/Default)
 TITLE+= (mini)
 DEPENDS+= @DEVEL
 VARIANT:=custom
 MENU:=1
endef

define Package/libffmpeg2-custom/config
source "$(SOURCE)/Config.in"
endef

define Package/libffmpeg2-custom/description
$(call Package/ffmpeg2/Default/description)
 .
 This package contains customized FFmpeg shared libraries.
endef


define Package/libffmpeg2-full
$(call Package/libffmpeg2/Default)
 TITLE+= (full)
 DEPENDS+= @BUILD_PATENTED +alsa-lib
 VARIANT:=full
endef

define Package/libffmpeg2-full/description
$(call Package/ffmpeg2/Default/description)
 .
 This package contains full-featured FFmpeg shared libraries.
endef


define Package/libffmpeg2-mini
$(call Package/libffmpeg2/Default)
 TITLE+= (mini)
 DEPENDS+= @BUILD_PATENTED
 VARIANT:=mini
endef

define Package/libffmpeg2-mini/description
$(call Package/ffmpeg2/Default/description)
 .
 This package contains minimal-featured FFmpeg shared libraries.
endef


FFMPEG_CONFIGURE:= \
	CFLAGS="$(TARGET_CFLAGS) $(TARGET_CPPFLAGS) $(FPIC)" \
	LDFLAGS="$(TARGET_LDFLAGS)" \
	./configure \
	--enable-cross-compile \
	--cross-prefix="$(TARGET_CROSS)" \
	--arch="$(ARCH)" \
	--target-os=linux \
	--prefix="/usr" \
	--enable-shared \
	--enable-static \
	--disable-debug \
	--pkg-config="pkg-config" \
	\
	--enable-gpl \
	--enable-version3 \
	\
	--disable-altivec \
	--disable-asm \
	--disable-doc \
	--disable-dxva2 \
	--enable-pthreads \
	--disable-optimizations \
	--enable-small \
	--disable-stripping \
	--enable-zlib \
	--disable-outdevs

ifeq ($(BUILD_VARIANT),custom)

  FFMPEG_ENABLE= \
	$(foreach c, $(2), \
		$(if $($(3)_$(c)),--enable-$(1)="$(c)") \
	)

  FFMPEG_CONFIGURE+= \
	--disable-ffmpeg \
	--disable-ffplay \
	--disable-ffprobe \
	--disable-ffserver \
	--disable-avfilter \
	--disable-postproc \
	--disable-swresample \
	--disable-swscale \
	--disable-everything \
	$(call FFMPEG_ENABLE,encoder,$(FFMPEG_CUSTOM_ENCODERS),CONFIG_FFMPEG_CUSTOM_ENCODER) \
	$(call FFMPEG_ENABLE,decoder,$(FFMPEG_CUSTOM_DECODERS),CONFIG_FFMPEG_CUSTOM_DECODER) \
	$(call FFMPEG_ENABLE,muxer,$(FFMPEG_CUSTOM_MUXERS),CONFIG_FFMPEG_CUSTOM_MUXER) \
	$(call FFMPEG_ENABLE,demuxer,$(FFMPEG_CUSTOM_DEMUXERS),CONFIG_FFMPEG_CUSTOM_DEMUXER) \
	$(call FFMPEG_ENABLE,parser,$(FFMPEG_CUSTOM_PARSERS),CONFIG_FFMPEG_CUSTOM_PARSER) \
	$(call FFMPEG_ENABLE,protocol,$(FFMPEG_CUSTOM_PROTOCOLS),CONFIG_FFMPEG_CUSTOM_PROTOCOL) \

endif

ifeq ($(BUILD_VARIANT),mini)

  FFMPEG_ENABLE= \
	$(foreach c, $(2), \
		--enable-$(1)="$(c)" \
	)

  FFMPEG_CONFIGURE+= \
	--disable-ffmpeg \
	--disable-ffplay \
	--disable-ffprobe \
	--disable-ffserver \
	--disable-avfilter \
	--disable-postproc \
	--disable-swresample \
	--disable-swscale \
	--disable-everything \
	$(call FFMPEG_ENABLE,encoder,$(FFMPEG_MINI_ENCODERS)) \
	$(call FFMPEG_ENABLE,decoder,$(FFMPEG_MINI_DECODERS)) \
	$(call FFMPEG_ENABLE,muxer,$(FFMPEG_MINI_MUXERS)) \
	$(call FFMPEG_ENABLE,demuxer,$(FFMPEG_MINI_DEMUXERS)) \
	$(call FFMPEG_ENABLE,parser,$(FFMPEG_MINI_PARSERS)) \
	$(call FFMPEG_ENABLE,protocol,$(FFMPEG_MINI_PROTOCOLS)) \

endif

ifneq ($(CONFIG_TARGET_x86),)
  TARGET_CFLAGS += -fomit-frame-pointer
endif

define Build/Configure
	( cd $(PKG_BUILD_DIR); $(FFMPEG_CONFIGURE) )
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		all install
endef

define Build/InstallDev/custom
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/lib{avcodec,avdevice,avformat,avutil} $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/lib{avcodec,avdevice,avformat,avutil}.{a,so*} $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/lib{avcodec,avdevice,avformat,avutil}.pc $(1)/usr/lib/pkgconfig/
endef

define Build/InstallDev/full
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/lib{avcodec,avdevice,avfilter,avformat,avutil,postproc,swresample,swscale} $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/lib{avcodec,avdevice,avfilter,avformat,avutil,postproc,swresample,swscale}.{a,so*} $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/lib{avcodec,avdevice,avfilter,avformat,avutil,postproc,swresample,swscale}.pc $(1)/usr/lib/pkgconfig/
endef

Build/InstallDev/mini = $(Build/InstallDev/custom)

# XXX: attempt at installing "best" dev files available
ifeq ($(BUILD_VARIANT),custom)
  # XXX: only install "custom" dev files if -full & -mini are not selected
  ifeq ($(CONFIG_PACKAGE_libffmpeg2-full)$(CONFIG_PACKAGE_libffmpeg2-mini),)
    Build/InstallDev = $(Build/InstallDev/custom)
  endif
endif
ifeq ($(BUILD_VARIANT),full)
  # XXX: always install "full" dev files if -full is selected
  Build/InstallDev = $(Build/InstallDev/full)
endif
ifeq ($(BUILD_VARIANT),mini)
  # XXX: only install "mini" dev files if -full is not selected
  ifeq ($(CONFIG_PACKAGE_libffmpeg2-full),)
    Build/InstallDev = $(Build/InstallDev/mini)
  endif
endif

define Package/ffmpeg2/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/ffmpeg $(1)/usr/bin/
endef

define Package/ffprobe2/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/ffprobe $(1)/usr/bin/
endef

define Package/ffserver2/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/ffserver $(1)/usr/bin/
endef

define Package/libffmpeg2-custom/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/lib{avcodec,avdevice,avformat,avutil}.so.* $(1)/usr/lib/
endef

define Package/libffmpeg2-full/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/lib{avcodec,avdevice,avfilter,avformat,avutil,postproc,swresample,swscale}.so.* $(1)/usr/lib/
endef

Package/libffmpeg2-mini/install = $(Package/libffmpeg2-custom/install)

$(eval $(call BuildPackage,ffmpeg2))
$(eval $(call BuildPackage,ffprobe2))
$(eval $(call BuildPackage,ffserver2))
$(eval $(call BuildPackage,libffmpeg2-custom))
$(eval $(call BuildPackage,libffmpeg2-full))
$(eval $(call BuildPackage,libffmpeg2-mini))
