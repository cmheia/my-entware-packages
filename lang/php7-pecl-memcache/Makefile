#
# Copyright (C) 2012-2015 OpenWrt.org
# Copyright (C) 2016 「有事燒紙」 <router@cmheia.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PECL_NAME:=memcache
PECL_LONGNAME:=memcached extension

PKG_NAME:=php7-pecl-$(PECL_NAME)

PKG_MAINTAINER:=cmheia <router@cmheia.com>

PKG_LICENSE:=PHPv3.01
PKG_LICENSE_FILES:=LICENSE

PKG_RELEASE:=1

PKG_SOURCE_VERSION:=php7
PKG_SOURCE_URL:=https://github.com/websupport-sk/pecl-memcache.git
PKG_SOURCE_PROTO:=git
PKG_VERSION:=5041d2fc36e8364fa6ccb04554ae16e9b12c355c
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.xz

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_PARALLEL:=1

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include ../php7/pecl.mk

define Package/$(PKG_NAME)/description
  Memcached is a caching daemon designed especially for  dynamic web applications to decrease database load by  storing objects in memory. This extension allows you to work with memcached through handy OO and procedural interfaces.
endef

CONFIGURE_ARGS+= --enable-memcache

$(eval $(call PECLPackage,$(PECL_NAME),$(PECL_LONGNAME),+zlib))
$(eval $(call BuildPackage,$(PKG_NAME)))
