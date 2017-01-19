#
# Copyright (C) 2012-2015 OpenWrt.org
# Copyright (C) 2017 然而并没有 <router@cmheia.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=nginx
PKG_VERSION:=1.11.8
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://nginx.org/download/
PKG_MD5SUM:=8f68f49b6db510e567bba9e0c271a3ac
PKG_MAINTAINER:=cmheia <router@cmheia.com>
PKG_LICENSE:=2-clause BSD-like license

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(BUILD_VARIANT)/$(PKG_NAME)-$(PKG_VERSION)

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

LUA_MODULE_VERSION:=0.9.19
LUA_MODULE_MD5SUM:=987b6dd138f831d4b524c5e7c28a4f84

LIBRESSL_VERSION:=2.5.0
LIBRESSL_MD5SUM:=99ce3203d1031b2503080104845b1bf0

PKG_CONFIG_DEPENDS := \
	CONFIG_NGINX_SSL \
	CONFIG_NGINX_DAV \
	CONFIG_NGINX_FLV \
	CONFIG_NGINX_STUB_STATUS \
	CONFIG_NGINX_HTTP_CHARSET \
	CONFIG_NGINX_HTTP_GZIP \
	CONFIG_NGINX_HTTP_SSI \
	CONFIG_NGINX_HTTP_USERID \
	CONFIG_NGINX_HTTP_ACCESS \
	CONFIG_NGINX_HTTP_AUTH_BASIC \
	CONFIG_NGINX_HTTP_AUTOINDEX \
	CONFIG_NGINX_HTTP_GEO \
	CONFIG_NGINX_HTTP_MAP \
	CONFIG_NGINX_HTTP_SPLIT_CLIENTS \
	CONFIG_NGINX_HTTP_REFERER \
	CONFIG_NGINX_HTTP_REWRITE \
	CONFIG_NGINX_HTTP_PROXY \
	CONFIG_NGINX_HTTP_FASTCGI \
	CONFIG_NGINX_HTTP_UWSGI \
	CONFIG_NGINX_HTTP_SCGI \
	CONFIG_NGINX_HTTP_MEMCACHED \
	CONFIG_NGINX_HTTP_LIMIT_CONN \
	CONFIG_NGINX_HTTP_LIMIT_REQ \
	CONFIG_NGINX_HTTP_EMPTY_GIF \
	CONFIG_NGINX_HTTP_BROWSER \
	CONFIG_NGINX_HTTP_UPSTREAM_HASH \
	CONFIG_NGINX_HTTP_UPSTREAM_IP_HASH \
	CONFIG_NGINX_HTTP_UPSTREAM_LEAST_CONN \
	CONFIG_NGINX_HTTP_UPSTREAM_KEEPALIVE \
	CONFIG_NGINX_HTTP_UPSTREAM_ZONE \
	CONFIG_NGINX_HTTP_CACHE \
	CONFIG_NGINX_PCRE \
	CONFIG_NGINX_HTTP_GUNZIP \
	CONFIG_NGINX_GZIP_STATIC \
	CONFIG_NGINX_HTTP_SECURE_LINK \
	CONFIG_NGINX_HTTP_V2 \
	CONFIG_NGINX_LIBATOMIC_OPS \
	CONFIG_NGINX_LUA

include $(INCLUDE_DIR)/package.mk

define Package/nginx/Default
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Web Servers/Proxies
  TITLE:=Nginx web server
  TITLE+=$(2)
  URL:=http://nginx.org/
  VARIANT:=$(1)
  DEPENDS:=+NGINX_PCRE:libpcre +NGINX_HTTP_GZIP:zlib +libssp
  DEPENDS+=$(3)

#ifeq ($(CONFIG_NGINX_LUA),y)
#  DEPENDS += +NGINX_LUA:liblua
#endif

ifneq ($(CONFIG_NGINX_USE_LIBRESSL),y)
  DEPENDS += +(NGINX_SSL||NGINX_HTTP_CACHE||NGINX_HTTP_AUTH_BASIC):libopenssl
endif

#  MENU:=1
endef

Package/nginx=$(call Package/nginx/Default,default,,+libpthread)
Package/nginx-lua=$(call Package/nginx/Default,lua,(LUA),+libpthread +liblua)

define Package/nginx/Default/description
 nginx is an HTTP and reverse proxy server, as well as a mail proxy server,
 written by Igor Sysoev.
endef

define Package/nginx/description
$(call Package/nginx/Default/description)
endef

define Package/nginx-lua/description
$(call Package/nginx/Default/description)
 This build include lua-nginx-module.
endef

define Package/nginx/config
  source "$(SOURCE)/Config.in"
endef

ifeq ($(BUILD_VARIANT),lua)
  CONFIG_NGINX_LUA:=y
endif

config_files=nginx.conf mime.types fastcgi_params koi-utf koi-win win-utf fastcgi.conf
vhost_files=blog.conf

define Package/nginx/conffiles
/opt/etc/nginx/
endef

Package/nginx-lua/conffiles=$(Package/nginx/conffiles)

ADDITIONAL_MODULES:=
ifeq ($(CONFIG_IPV6),y)
  ADDITIONAL_MODULES += --with-ipv6
endif
ifeq ($(CONFIG_NGINX_STUB_STATUS),y)
  ADDITIONAL_MODULES += --with-http_stub_status_module
endif
ifeq ($(CONFIG_NGINX_FLV),y)
  ADDITIONAL_MODULES += --with-http_flv_module
endif
ifeq ($(CONFIG_NGINX_SSL),y)
  ADDITIONAL_MODULES += --with-http_ssl_module
endif
ifeq ($(CONFIG_NGINX_DAV),y)
  ADDITIONAL_MODULES += --with-http_dav_module
endif
ifneq ($(CONFIG_NGINX_HTTP_CACHE),y)
  ADDITIONAL_MODULES += --without-http-cache
endif
ifneq ($(CONFIG_NGINX_PCRE),y)
  ADDITIONAL_MODULES += --without-pcre
endif
ifneq ($(CONFIG_NGINX_HTTP_CHARSET),y)
  ADDITIONAL_MODULES += --without-http_charset_module
endif
ifneq ($(CONFIG_NGINX_HTTP_GZIP),y)
  ADDITIONAL_MODULES += --without-http_gzip_module
endif
ifneq ($(CONFIG_NGINX_HTTP_SSI),y)
  ADDITIONAL_MODULES += --without-http_ssi_module
endif
ifneq ($(CONFIG_NGINX_HTTP_USERID),y)
  ADDITIONAL_MODULES += --without-http_userid_module
endif
ifneq ($(CONFIG_NGINX_HTTP_ACCESS),y)
  ADDITIONAL_MODULES += --without-http_access_module
endif
ifneq ($(CONFIG_NGINX_HTTP_AUTH_BASIC),y)
  ADDITIONAL_MODULES += --without-http_auth_basic_module
endif
ifneq ($(CONFIG_NGINX_HTTP_AUTOINDEX),y)
  ADDITIONAL_MODULES += --without-http_autoindex_module
endif
ifneq ($(CONFIG_NGINX_HTTP_GEO),y)
  ADDITIONAL_MODULES += --without-http_geo_module
endif
ifneq ($(CONFIG_NGINX_HTTP_MAP),y)
  ADDITIONAL_MODULES += --without-http_map_module
endif
ifneq ($(CONFIG_NGINX_HTTP_SPLIT_CLIENTS),y)
  ADDITIONAL_MODULES += --without-http_split_clients_module
endif
ifneq ($(CONFIG_NGINX_HTTP_REFERER),y)
  ADDITIONAL_MODULES += --without-http_referer_module
endif
ifneq ($(CONFIG_NGINX_HTTP_REWRITE),y)
  ADDITIONAL_MODULES += --without-http_rewrite_module
endif
ifneq ($(CONFIG_NGINX_HTTP_PROXY),y)
  ADDITIONAL_MODULES += --without-http_proxy_module
endif
ifneq ($(CONFIG_NGINX_HTTP_FASTCGI),y)
  ADDITIONAL_MODULES += --without-http_fastcgi_module
endif
ifneq ($(CONFIG_NGINX_HTTP_UWSGI),y)
  ADDITIONAL_MODULES += --without-http_uwsgi_module
endif
ifneq ($(CONFIG_NGINX_HTTP_SCGI),y)
  ADDITIONAL_MODULES += --without-http_scgi_module
endif
ifneq ($(CONFIG_NGINX_HTTP_MEMCACHED),y)
  ADDITIONAL_MODULES += --without-http_memcached_module
endif
ifneq ($(CONFIG_NGINX_HTTP_LIMIT_CONN),y)
  ADDITIONAL_MODULES += --without-http_limit_conn_module
endif
ifneq ($(CONFIG_NGINX_HTTP_LIMIT_REQ),y)
  ADDITIONAL_MODULES += --without-http_limit_req_module
endif
ifneq ($(CONFIG_NGINX_HTTP_EMPTY_GIF),y)
  ADDITIONAL_MODULES += --without-http_empty_gif_module
endif
ifneq ($(CONFIG_NGINX_HTTP_BROWSER),y)
  ADDITIONAL_MODULES += --without-http_browser_module
endif
ifneq ($(CONFIG_NGINX_HTTP_UPSTREAM_HASH),y)
  ADDITIONAL_MODULES += --without-http_upstream_hash_module
endif
ifneq ($(CONFIG_NGINX_HTTP_UPSTREAM_IP_HASH),y)
  ADDITIONAL_MODULES += --without-http_upstream_ip_hash_module
endif
ifneq ($(CONFIG_NGINX_HTTP_UPSTREAM_LEAST_CONN),y)
  ADDITIONAL_MODULES += --without-http_upstream_least_conn_module
endif
ifneq ($(CONFIG_NGINX_HTTP_UPSTREAM_KEEPALIVE),y)
  ADDITIONAL_MODULES += --without-http_upstream_keepalive_module
endif
ifeq ($(CONFIG_NGINX_HTTP_UPSTREAM_CHECK),y)
  ADDITIONAL_MODULES += --add-module=nginx-upstream-check
endif
ifeq ($(CONFIG_NGINX_HTTP_GUNZIP),y)
  ADDITIONAL_MODULES += --with-http_gunzip_module
endif
ifeq ($(CONFIG_NGINX_GZIP_STATIC),y)
  ADDITIONAL_MODULES += --with-http_gzip_static_module
endif
ifeq ($(CONFIG_NGINX_HTTP_SECURE_LINK),y)
  ADDITIONAL_MODULES += --with-http_secure_link_module
endif
ifeq ($(CONFIG_NGINX_HTTP_V2),y)
  ADDITIONAL_MODULES += --with-http_v2_module
endif
ifeq ($(CONFIG_NGINX_SUBSTITUTIONS_FILTER),y)
  ADDITIONAL_MODULES += --add-module=nginx-substitutions-filter
endif
ifeq ($(CONFIG_NGINX_USE_LIBRESSL),y)
  ADDITIONAL_MODULES += --with-openssl=libressl
  TARGET_LDFLAGS += -lssp
endif
ifeq ($(CONFIG_NGINX_LIBATOMIC_OPS),y)
  ADDITIONAL_MODULES += --with-libatomic=libatomic_ops
endif
ifeq ($(CONFIG_NGINX_LUA),y)
  ADDITIONAL_MODULES += --add-module=lua-nginx
endif

define Build/Configure
	# DEBUG: Configure nginx
	( cd $(PKG_BUILD_DIR) ; \
		$(if $(CONFIG_NGINX_LUA),LUA_INC=$(STAGING_DIR)/opt/include LUA_LIB=$(STAGING_DIR)/opt/lib) \
		./configure \
			--crossbuild=Linux::$(ARCH) \
			--prefix=/opt \
			--conf-path=/opt/etc/nginx/nginx.conf \
			$(ADDITIONAL_MODULES) \
			--error-log-path=/opt/var/log/nginx/error.log \
			--pid-path=/var/run/nginx.pid \
			--lock-path=/var/lock/nginx.lock \
			--http-log-path=/opt/var/log/nginx/access.log \
			--http-client-body-temp-path=/opt/var/lib/nginx/body \
			--http-proxy-temp-path=/opt/var/lib/nginx/proxy \
			--http-fastcgi-temp-path=/opt/var/lib/nginx/fastcgi \
			--http-uwsgi-temp-path=/opt/var/lib/nginx/uwsgi \
			--http-scgi-temp-path=/opt/var/lib/nginx/scgi \
			--with-cc="$(TARGET_CC)" \
			--with-cc-opt="$(TARGET_CPPFLAGS) $(TARGET_CFLAGS)" \
			--with-ld-opt="$(TARGET_LDFLAGS)" \
	)
endef

define Package/nginx/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/nginx $(1)/opt/sbin/
	$(INSTALL_DIR) $(1)/opt/etc/nginx/vhost
	$(INSTALL_DATA) $(addprefix $(PKG_INSTALL_DIR)/opt/etc/nginx/,$(config_files)) $(1)/opt/etc/nginx/
	$(INSTALL_DATA) $(addprefix $(PKG_INSTALL_DIR)/opt/etc/nginx/vhost/,$(vhost_files)) $(1)/opt/etc/nginx/vhost
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S80nginx $(1)/opt/etc/init.d
	$(INSTALL_DIR) $(1)/opt/share/nginx/html
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/opt/html/{index,50x}.html $(1)/opt/share/nginx/html
	$(INSTALL_DIR) $(1)/opt/var/log/nginx
	$(INSTALL_DIR) $(1)/opt/var/lib/nginx/{body,fastcgi}
	$(INSTALL_DIR) $(1)/opt/var/proxy/nginx/{temp,cache}
endef

Package/nginx-lua/install=$(Package/nginx/install)

define Build/Prepare
	# DEBUG: Prepare nginx
	$(call Build/Prepare/Default)
	$(if $(CONFIG_NGINX_LUA),$(call Prepare/lua-nginx))
	$(if $(CONFIG_NGINX_LIBATOMIC_OPS),$(call Prepare/libatomic_ops))
	$(if $(CONFIG_NGINX_HTTP_UPSTREAM_CHECK),$(call Prepare/nginx-upstream-check))
	$(if $(CONFIG_NGINX_SUBSTITUTIONS_FILTER),$(call Prepare/nginx-substitutions-filter))
	$(if $(CONFIG_NGINX_USE_LIBRESSL),$(call Prepare/libressl))
endef

define Download/libatomic_ops
	VERSION:=45896dc8681951f6ef3e0fcb7dd38e7e2a435411
	SUBDIR:=libatomic_ops
	FILE:=libatomic_ops-$(PKG_VERSION)-$$(VERSION).tar.gz
	URL:=https://github.com/ivmai/libatomic_ops.git
	PROTO:=git
endef

define Prepare/libatomic_ops
	$(eval $(call Download,libatomic_ops))
	gzip -dc $(DL_DIR)/$(FILE) | tar -C $(PKG_BUILD_DIR) $(TAR_OPTIONS)
	# DEBUG: patch autoreconf & crosscompile libatomic_ops
	$(call PatchDir,$(PKG_BUILD_DIR),./patches-libatomic_ops)
	sed -i 's!\&\& ./configure!\&\& ./configure --host=$(REAL_GNU_TARGET_NAME)!' $(PKG_BUILD_DIR)/auto/lib/libatomic/make
endef

define Download/lua-nginx
	SUBDIR:=lua-nginx
	FILE:=v$(LUA_MODULE_VERSION).tar.gz
	MD5SUM:=$(LUA_MODULE_MD5SUM)
	URL:=https://github.com/openresty/lua-nginx-module/archive
endef

define Prepare/lua-nginx
	$(eval $(call Download,lua-nginx))
	gzip -dc $(DL_DIR)/$(FILE) | tar -C $(PKG_BUILD_DIR) $(TAR_OPTIONS)
	mv $(PKG_BUILD_DIR)/lua-nginx-module-$(LUA_MODULE_VERSION) $(PKG_BUILD_DIR)/lua-nginx
	$(call PatchDir,$(PKG_BUILD_DIR),./patches-lua-nginx)
endef

define Download/nginx-upstream-check
	VERSION:=d6341aeeb86911d4798fbceab35015c63178e66f
	SUBDIR:=nginx-upstream-check
	FILE:=nginx-upstream-check-$(PKG_VERSION)-$$(VERSION).tar.gz
	URL:=https://github.com/yaoweibin/nginx_upstream_check_module.git
	PROTO:=git
endef

define Prepare/nginx-upstream-check
	$(eval $(call Download,nginx-upstream-check))
	gzip -dc $(DL_DIR)/$(FILE) | tar -C $(PKG_BUILD_DIR) $(TAR_OPTIONS)
	# DEBUG: Prepare nginx-upstream-check
	# DEBUG: dir contents:
	ls -lh
	# DEBUG: PKG_BUILD_DIR $(PKG_BUILD_DIR)
	cat $(PKG_BUILD_DIR)/nginx-upstream-check/check_1.11.5+.patch | patch -f -p0 -d $(PKG_BUILD_DIR)
	# DEBUG: ---end---
endef

define Download/nginx-substitutions-filter
	VERSION:=bc58cb11844bc42735bbaef7085ea86ace46d05b
	SUBDIR:=nginx-substitutions-filter
	FILE:=nginx-substitutions-filter-$(PKG_VERSION)-$$(VERSION).tar.gz
	URL:=https://github.com/yaoweibin/ngx_http_substitutions_filter_module.git
	PROTO:=git
endef

define Prepare/nginx-substitutions-filter
	$(eval $(call Download,nginx-substitutions-filter))
	gzip -dc $(DL_DIR)/$(FILE) | tar -C $(PKG_BUILD_DIR) $(TAR_OPTIONS)
endef

define Download/libressl
	SUBDIR:=libressl
	FILE:=libressl-$(LIBRESSL_VERSION).tar.gz
	MD5SUM:=$(LIBRESSL_MD5SUM)
	URL:=http://ftp.openbsd.org/pub/OpenBSD/LibreSSL/
endef

define Prepare/libressl
	# DEBUG: Prepare libressl
	$(eval $(call Download,libressl))
	gzip -dc $(DL_DIR)/$(FILE) | tar -C $(PKG_BUILD_DIR) $(TAR_OPTIONS)
	mv $(PKG_BUILD_DIR)/libressl-$(LIBRESSL_VERSION) $(PKG_BUILD_DIR)/libressl
	# DEBUG: patch crosscompile libressl
	# DEBUG: REAL_GNU_TARGET_NAME $(REAL_GNU_TARGET_NAME)
	sed -i 's/^ARGS=""/ARGS="--host=$(REAL_GNU_TARGET_NAME) "/' $(PKG_BUILD_DIR)/libressl/config
	$(call PatchDir,$(PKG_BUILD_DIR),./patches-libressl)
	# DEBUG: ---begin---
	# DEBUG: current working dir:
	pwd
	# DEBUG: dir contents:
	ls -lh
	# DEBUG: PKG_BUILD_DIR $(PKG_BUILD_DIR)
	# DEBUG: ---end---
endef

$(eval $(call BuildPackage,nginx))
$(eval $(call BuildPackage,nginx-lua))
