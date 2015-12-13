#
# Copyright (C) 2012-2015 OpenWrt.org
# Copyright (C) 2015 「有事燒紙」 <router@cmheia.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PECL_NAME:=xdebug
PECL_LONGNAME:=Provides functions for function traces and profiling

PKG_VERSION:=2.4.0RC2
PHP_VERSION:=7.0.0
PKG_RELEASE:=1

PKG_NAME:=php7-pecl-$(PECL_NAME)
PKG_SOURCE:=$(PECL_NAME)-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=http://pecl.php.net/get/
PKG_MD5SUM:=8b3d7d5e3dbf439fd21f8cd618f839f2

PKG_MAINTAINER:=cmheia <router@cmheia.com>

PKG_LICENSE:=PHPv3.01
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)-$(PHP_VERSION)
PKG_BUILD_PARALLEL:=1

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include ../php7/pecl.mk

define Package/$(PKG_NAME)/description
	The Xdebug extension helps you debugging your script by providing a lot of valuable debug information.
endef

define Build/Prepare
	# DEBUG: Prepare $(PECL_NAME)
	# DEBUG: $(PKG_BUILD_DIR)
	$(PKG_UNPACK)
	mv $(BUILD_DIR)/$(PECL_NAME)-$(PKG_VERSION)/* $(PKG_BUILD_DIR)/
	rmdir $(BUILD_DIR)/$(PECL_NAME)-$(PKG_VERSION)
	$(Build/Patch)
	# DEBUG: run phpize
	( cd $(PKG_BUILD_DIR); $(STAGING_DIR_HOST)/opt/bin/phpize )
endef

$(eval $(call PECLPackage,$(PECL_NAME),$(PECL_LONGNAME),,zend))
$(eval $(call BuildPackage,$(PKG_NAME)))
