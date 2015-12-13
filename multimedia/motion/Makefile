#
# Copyright (C) 2008-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=motion
PKG_VERSION=3.4.1~rc01-20151004-$(PKG_SOURCE_VERSION)
PKG_RELEASE:=1

PKG_MAINTAINER:=cmheia <router@cmheia.com>
PKG_LICENSE:=GPLv2
PKG_LICENSE_FILES:=COPYING

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Mr-Dave/motion.git
PKG_SOURCE_VERSION:=9b4c16cae0ea77950cc156a9c82947ac51825f68

PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)
PKG_BUILD_PARALLEL:=1
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/motion
  SECTION:=multimedia
  CATEGORY:=Multimedia
  DEPENDS:=+libjpeg +libpthread
  TITLE:=webcam motion sensing and logging
  URL:=http://www.lavrsen.dk/twiki/bin/view/Motion/WebHome
endef

define Package/motion/conffiles
/opt/etc/motion
endef

CONFIGURE_ARGS+= \
	--without-optimizecpu \
	--without-ffmpeg \
	--without-jpeg-mmx \
	--without-sdl \
	--without-pgsql \
	--without-sqlite3 \

define Package/motion/install
	$(INSTALL_DIR) $(1)/opt/etc/motion
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/motion-dist.conf $(1)/opt/etc/motion/motion.conf
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/motion $(1)/opt/bin/
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S99motion  $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,motion))
