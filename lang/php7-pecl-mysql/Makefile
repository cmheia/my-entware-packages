#
# Copyright (C) 2012-2015 OpenWrt.org
# Copyright (C) 2015 「有事燒紙」 <router@cmheia.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PECL_NAME:=mysql
PECL_LONGNAME:=MySQL database access functions

PKG_VERSION:=1.0.0-dev
PKG_RELEASE:=1

PKG_NAME:=php7-pecl-$(PECL_NAME)

PKG_SOURCE_URL:=https://github.com/php/pecl-database-mysql.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=230a8287c04c69dfc49f6a68a5debb4e4198e98f
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.xz

PKG_MAINTAINER:=cmheia <router@cmheia.com>

PKG_LICENSE:=PHPv3.01
PKG_LICENSE_FILES:=

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_PARALLEL:=1

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include ../php7/pecl.mk

define Package/$(PKG_NAME)/description
  This extension provides the mysql family of functions that were
  provided with PHP 3-5. These functions have been superseded by
  MySQLi and PDO_MySQL, which continue to be bundled with PHP 7.
  Although it should be possible to build this extension with PHP 7.0,
  you are strongly encouraged to port your code to use either MySQLi
  or PDO_MySQL, as this extension is not maintained and is
  available for historical reasons only.
endef

CONFIGURE_ARGS+= --with-mysql=shared,"$(STAGING_DIR)/opt"

$(eval $(call PECLPackage,$(PECL_NAME),$(PECL_LONGNAME),+libmysqlclient))
$(eval $(call BuildPackage,$(PKG_NAME)))
