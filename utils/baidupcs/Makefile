#
# Copyright (C) 2009-2012 OpenWrt.org
# Copyright (C) 2015 「有事燒紙」 <router@cmheia.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=baidupcs
PKG_VERSION=0.2.2-20151016-$(PKG_SOURCE_VERSION)
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/GangZhuo/BaiduPCS.git
PKG_SOURCE_VERSION:=0eff5897bfefc3d75e671e24380d5233d383fe82
PKG_LICENSE:=MIT

PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.xz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=BaiduPCS
	URL:=https://github.com/GangZhuo/BaiduPCS
	MAINTAINER:=Gang Zhuo <gang.zhuo@gmail.com>
	DEPENDS:=+libopenssl +libcurl +libpthread
endef

define Package/$(PKG_NAME)/description
	The client for baidu net disk.
endef

TARGET_LDFLAGS+= -lm -lcurl -lssl -lcrypto -lpthread

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/pcs $(1)/opt/bin
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
