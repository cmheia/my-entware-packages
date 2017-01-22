#
# Copyright (C) 2006-2015 OpenWrt.org
# Copyright (C) 2015 「有事燒紙」 <router@cmheia.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=php
PKG_VERSION:=7.1.1
PKG_RELEASE:=1

PKG_MAINTAINER:=cmheia <router@cmheia.com>

PKG_LICENSE:=PHPv3.01
PKG_LICENSE_FILES:=LICENSE

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://php.net/distributions/
PKG_MD5SUM:=65eef256f6e7104a05361939f5e23ada

PKG_FIXUP:=libtool autoreconf
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

PHP7_MODULES = \
	bcmath bz2 \
	calendar ctype curl \
	dom \
	exif \
	fileinfo ftp \
	gettext gd gmp \
	hash \
	iconv \
	json \
	ldap \
	imap \
	mbstring mcrypt mysqli mysqlnd \
	opcache openssl \
	pcntl pdo pdo-mysql pdo-pgsql pdo-sqlite pgsql phar \
	readline \
	session shmop simplexml soap sockets sqlite3 sysvmsg sysvsem sysvshm \
	tokenizer \
	xml xmlreader xmlwriter zip \

PKG_CONFIG_DEPENDS:= \
	$(patsubst %,CONFIG_PACKAGE_php7-mod-%,$(PHP7_MODULES)) \
	CONFIG_PHP7_FILTER CONFIG_PHP7_LIBXML

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/php7/Default
  SUBMENU:=PHP
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=PHP7 Hypertext preprocessor
  URL:=http://www.php.net/
  DEPENDS:=php7
endef

define Package/php7/Default/description
  PHP is a widely-used general-purpose scripting language that is especially
  suited for Web development and can be embedded into HTML.
endef

define Package/php7/config
	config PHP7_FILTER
		bool "PHP7 Filter support"
		depends on PACKAGE_php7-cli || PACKAGE_php7-cgi

	config PHP7_LIBXML
		bool "PHP7 LIBXML support"
		depends on PACKAGE_php7-cli || PACKAGE_php7-cgi
endef

define Package/php7
  $(call Package/php7/Default)

  DEPENDS:=+libpcre +zlib \
           +libbz2 \
           +PHP7_LIBXML:libxml2
endef

define Package/php7/description
  $(call Package/php7/Default/description)
  This package contains only the PHP config file. You must actually choose
  your PHP flavour (cli, cgi or fastcgi).
endef

define Package/php7-cli
  $(call Package/php7/Default)
  TITLE+= (CLI)
endef

define Package/php7-cli/description
  $(call Package/php7/Default/description)
  This package contains the CLI version of the PHP7 interpreter.
endef

define Package/php7-cgi
  $(call Package/php7/Default)
  TITLE+= (CGI & FastCGI)
endef

define Package/php7-cgi/description
  $(call Package/php7/Default/description)
  This package contains the CGI version of the PHP7 interpreter.
endef

define Package/php7-fastcgi
  $(call Package/php7/Default)
  DEPENDS+= +php7-cgi
  TITLE:=FastCGI startup script
endef

define Package/php7-fastcgi/description
  As FastCGI support is now a core feature the php7-fastcgi package now depends
  on the php7-cgi package, containing just the README.FastCGI.
endef

define Package/php7-fpm
  $(call Package/php7/Default)
  DEPENDS+= +php7-cgi
  TITLE+= (FPM)
endef

define Package/php7-fpm/description
  $(call Package/php7/Default/description)
  This package contains the FastCGI Process Manager of the PHP7 interpreter.
endef

define Package/php7-dbg
  $(call Package/php7/Default)
  DEPENDS+= +libreadline
  TITLE:=The interactive PHP debugger
endef

define Package/php7-dbg/description
  $(call Package/php7/Default/description)
  Implemented as a SAPI module, phpdbg can exert complete control over
  the environment without impacting the functionality or performance of your code.
  phpdbg aims to be a lightweight, powerful,
  easy to use debugging platform for PHP 5.4+
  https://github.com/krakjoe/phpdbg/issues/103
endef

CONFIGURE_ARGS+= \
	--enable-cli \
	--enable-cgi \
	--enable-fpm \
	--enable-phpdbg \
	--enable-shared \
	--disable-static \
	--disable-rpath \
	--disable-debug \
	--without-pear \
	\
	--with-config-file-path=/opt/etc \
	--with-config-file-scan-dir=/opt/etc/php7 \
	--disable-short-tags \
	\
	--with-zlib="$(STAGING_DIR)/opt" \
	--with-zlib-dir="$(STAGING_DIR)/opt" \
	--with-pcre-regex="$(STAGING_DIR)/opt"


ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-bcmath),)
  CONFIGURE_ARGS+= --enable-bcmath=shared
else
  CONFIGURE_ARGS+= --disable-bcmath
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-bz2),)
  CONFIGURE_ARGS+= --with-bz2=shared,"$(STAGING_DIR)/opt"
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-calendar),)
  CONFIGURE_ARGS+= --enable-calendar=shared
else
  CONFIGURE_ARGS+= --disable-calendar
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-ctype),)
  CONFIGURE_ARGS+= --enable-ctype=shared
else
  CONFIGURE_ARGS+= --disable-ctype
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-curl),)
  CONFIGURE_ARGS+= --with-curl=shared,"$(STAGING_DIR)/opt"
else
  CONFIGURE_ARGS+= --without-curl
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-fileinfo),)
  CONFIGURE_ARGS+= --enable-fileinfo=shared
else
  CONFIGURE_ARGS+= --disable-fileinfo
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-dom),)
  CONFIGURE_ARGS+= --enable-dom=shared
else
  CONFIGURE_ARGS+= --disable-dom
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-exif),)
  CONFIGURE_ARGS+= --enable-exif=shared
else
  CONFIGURE_ARGS+= --disable-exif
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-ftp),)
  CONFIGURE_ARGS+= --enable-ftp=shared
else
  CONFIGURE_ARGS+= --disable-ftp
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-gettext),)
  CONFIGURE_ARGS+= --with-gettext=shared,"$(STAGING_DIR)/opt/lib/libintl-full"
else
  CONFIGURE_ARGS+= --without-gettext
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-gd),)
  CONFIGURE_ARGS+= \
    --with-gd=shared \
    --with-freetype-dir="$(STAGING_DIR)/opt" \
    --with-jpeg-dir="$(STAGING_DIR)/opt" \
    --with-png-dir="$(STAGING_DIR)/opt" \
    --without-xpm-dir \
    --without-t1lib \
    --enable-gd-native-ttf \
    --disable-gd-jis-conv
else
  CONFIGURE_ARGS+= --without-gd
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-gmp),)
  CONFIGURE_ARGS+= --with-gmp=shared,"$(STAGING_DIR)/opt"
else
  CONFIGURE_ARGS+= --without-gmp
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-hash),)
  CONFIGURE_ARGS+= --enable-hash=shared
else
  CONFIGURE_ARGS+= --disable-hash
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-iconv),)
  CONFIGURE_ARGS+= --with-iconv=shared,"$(ICONV_PREFIX)"
else
  CONFIGURE_ARGS+= --without-iconv
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-json),)
  CONFIGURE_ARGS+= --enable-json=shared
else
  CONFIGURE_ARGS+= --disable-json
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-ldap),)
  CONFIGURE_ARGS+= \
	--with-ldap=shared,"$(STAGING_DIR)/opt" \
	--with-ldap-sasl="$(STAGING_DIR)/opt"
else
  CONFIGURE_ARGS+= --without-ldap
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-mbstring),)
  CONFIGURE_ARGS+= --enable-mbstring=shared --enable-mbregex
else
  CONFIGURE_ARGS+= --disable-mbstring
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-mcrypt),)
  CONFIGURE_ARGS+=  --with-mcrypt=shared,"$(STAGING_DIR)/opt"
else
  CONFIGURE_ARGS+= --without-mcrypt
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-mysqlnd),)
  CONFIGURE_ARGS+= --enable-mysqlnd=shared
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-mysqli),)
  ifneq ($(CONFIG_PACKAGE_php7-mod-mysqlnd),)
    CONFIGURE_ARGS+= --with-mysqli=shared
  else
    CONFIGURE_ARGS+= --with-mysqli=shared,"$(STAGING_DIR)/opt/bin/mysql_config"
  endif
else
  CONFIGURE_ARGS+= --without-mysqli
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-opcache),)
  CONFIGURE_ARGS+= --enable-opcache=shared
else
  CONFIGURE_ARGS+= --disable-opcache
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-openssl),)
  CONFIGURE_ARGS+= \
    --with-openssl=shared,"$(STAGING_DIR)/opt" \
    --with-openssl-dir="$(STAGING_DIR)/opt"
ifeq ($(SDK)$(CONFIG_PACKAGE_php7-mod-imap),)
  CONFIGURE_ARGS+= --with-kerberos=no
endif
else
  CONFIGURE_ARGS+= --without-openssl
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-pcntl),)
  CONFIGURE_ARGS+= --enable-pcntl=shared
else
  CONFIGURE_ARGS+= --disable-pcntl
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-pdo),)
  CONFIGURE_ARGS+= --enable-pdo=shared
  ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-pdo-mysql),)
    ifneq ($(CONFIG_PACKAGE_php7-mod-mysqlnd),)
      CONFIGURE_ARGS+= --with-pdo-mysql=shared
    else
      CONFIGURE_ARGS+= --with-pdo-mysql=shared,"$(STAGING_DIR)/opt"
    endif
  else
    CONFIGURE_ARGS+= --without-pdo-mysql
  endif
  ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-pdo-pgsql),)
    CONFIGURE_ARGS+= --with-pdo-pgsql=shared,"$(STAGING_DIR)/opt"
  else
    CONFIGURE_ARGS+= --without-pdo-pgsql
  endif
  ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-pdo-sqlite),)
    CONFIGURE_ARGS+= --with-pdo-sqlite=shared,"$(STAGING_DIR)/opt"
  else
    CONFIGURE_ARGS+= --without-pdo-sqlite
  endif
else
  CONFIGURE_ARGS+= --disable-pdo
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-pgsql),)
  CONFIGURE_ARGS+= --with-pgsql=shared,"$(STAGING_DIR)/opt"
else
  CONFIGURE_ARGS+= --without-pgsql
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-readline),)
  CONFIGURE_ARGS+= --with-readline=shared,"$(STAGING_DIR)/opt"
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-session),)
  CONFIGURE_ARGS+= --enable-session=shared
else
  CONFIGURE_ARGS+= --disable-session
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-shmop),)
  CONFIGURE_ARGS+= --enable-shmop=shared
else
  CONFIGURE_ARGS+= --disable-shmop
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-simplexml),)
  CONFIGURE_ARGS+= --enable-simplexml=shared
else
  CONFIGURE_ARGS+= --disable-simplexml
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-soap),)
  CONFIGURE_ARGS+= --enable-soap=shared
else
  CONFIGURE_ARGS+= --disable-soap
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-sockets),)
  CONFIGURE_ARGS+= --enable-sockets=shared
else
  CONFIGURE_ARGS+= --disable-sockets
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-sqlite3),)
  CONFIGURE_ARGS+= --with-sqlite3=shared,"$(STAGING_DIR)/opt"
else
  CONFIGURE_ARGS+= --without-sqlite3
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-sysvmsg),)
  CONFIGURE_ARGS+= --enable-sysvmsg=shared
else
  CONFIGURE_ARGS+= --disable-sysvmsg
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-sysvsem),)
  CONFIGURE_ARGS+= --enable-sysvsem=shared
else
  CONFIGURE_ARGS+= --disable-sysvsem
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-sysvshm),)
  CONFIGURE_ARGS+= --enable-sysvshm=shared
else
  CONFIGURE_ARGS+= --disable-sysvshm
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-tokenizer),)
  CONFIGURE_ARGS+= --enable-tokenizer=shared
else
  CONFIGURE_ARGS+= --disable-tokenizer
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-xml),)
  CONFIGURE_ARGS+= --enable-xml=shared,"$(STAGING_DIR)/opt"
  ifneq ($(CONFIG_PHP7_LIBXML),)
    CONFIGURE_ARGS+= --with-libxml-dir="$(STAGING_DIR)/opt/include/libxml2"
  else
    CONFIGURE_ARGS+= --with-libexpat-dir="$(STAGING_DIR)/opt"
  endif
else
  CONFIGURE_ARGS+= --disable-xml
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-xmlreader),)
  CONFIGURE_ARGS+= --enable-xmlreader=shared,"$(STAGING_DIR)/opt"
else
  CONFIGURE_ARGS+= --disable-xmlreader
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-xmlwriter),)
  CONFIGURE_ARGS+= --enable-xmlwriter=shared,"$(STAGING_DIR)/opt"
else
  CONFIGURE_ARGS+= --disable-xmlwriter
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-phar),)
  CONFIGURE_ARGS+= --enable-phar=shared,"$(STAGING_DIR)/opt"
else
  CONFIGURE_ARGS+= --disable-phar
endif

# WARN: if error: utf8_mime2text() has new signature, but U8T_CANONICAL is missing
# FIXIT: sudo apt-get install libc-client2007e-dev
ifneq ($(SDK)$(CONFIG_PACKAGE_php7-mod-imap),)
  CONFIGURE_ARGS+= --with-imap=shared,"$(STAGING_DIR_ROOT)/opt" \
  --with-kerberos \
  --with-imap-ssl
endif

ifneq ($(CONFIG_PACKAGE_php7-mod-zip),)
  CONFIGURE_ARGS+= --enable-zip=shared
else
  CONFIGURE_ARGS+= --disable-zip
endif

ifneq ($(SDK)$(CONFIG_PHP7_FILTER),)
  CONFIGURE_ARGS+= --enable-filter
else
  CONFIGURE_ARGS+= --disable-filter
endif

ifneq ($(SDK)$(CONFIG_PHP7_LIBXML),)
  CONFIGURE_ARGS+= --enable-libxml
  CONFIGURE_ARGS+= --with-libxml-dir="$(STAGING_DIR)/opt/include/libxml2"
else
  CONFIGURE_ARGS+= --disable-libxml
endif

CONFIGURE_VARS+= \
  ac_cv_c_bigendian_php=$(if $(CONFIG_BIG_ENDIAN),yes,no) \
  php_cv_cc_rpath="no" \
  iconv_impl_name="gnu_libiconv" \
  ac_cv_php_xml2_config_path="$(STAGING_DIR)/host/bin/xml2-config" \

define Package/php7/conffiles
/opt/etc/php.ini
endef

define Package/php7-fpm/conffiles
/opt/etc/php7-fpm.conf
/opt/etc/php7-fpm.d/www.conf
endef

define Package/php7/install
	$(INSTALL_DIR) $(1)/opt/etc
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/php.ini-{production,development} $(1)/opt/etc/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/php.ini-production $(1)/opt/etc/php.ini
	sed -i 's@^zlib.output_compression.*@zlib.output_compression = On@' $(1)/opt/etc/php.ini
	sed -i 's@^;zlib.output_handler.*@zlib.output_handler = Off@' $(1)/opt/etc/php.ini
	sed -i 's@^memory_limit.*@memory_limit = 16M@' $(1)/opt/etc/php.ini
	sed -i 's@^; extension_dir = "./"@extension_dir = "/opt/lib/php"@' $(1)/opt/etc/php.ini
	sed -i 's@^;upload_tmp_dir.*@upload_tmp_dir = /tmp@' $(1)/opt/etc/php.ini
	sed -i 's@^default_socket_timeout.*@default_socket_timeout = 5@' $(1)/opt/etc/php.ini
	sed -i 's@^;session.save_path.*@session.save_path = "/tmp"@' $(1)/opt/etc/php.ini
	sed -i 's@^session.gc_divisor.*@session.gc_divisor = 100@' $(1)/opt/etc/php.ini
	sed -i 's@^;date.timezone.*@date.timezone = Asia/Shanghai@' $(1)/opt/etc/php.ini
	sed -i 's@^upload_max_filesize.*@upload_max_filesize = 4M@' $(1)/opt/etc/php.ini
endef

define Package/php7-cli/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_BUILD_DIR)/sapi/cli/php $(1)/opt/bin/php-cli
endef

define Package/php7-cgi/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_BUILD_DIR)/sapi/cgi/php-cgi $(1)/opt/bin/php-cgi
	$(LN) php-cgi $(1)/opt/bin/php-fcgi
endef

define Package/php7-fastcgi/install
	$(INSTALL_DIR) $(1)/opt/etc
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/sapi/cgi/README.FastCGI $(1)/opt/etc/
endef

define Package/php7-fpm/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/sapi/fpm/php-fpm $(1)/opt/sbin/php7-fpm

	$(INSTALL_DIR) $(1)/opt/etc
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/sapi/fpm/php-fpm.conf $(1)/opt/etc/php7-fpm.conf
	sed -i 's@^;error_log.*@error_log=/opt/var/log/php7-fpm.log@' $(1)/opt/etc/php7-fpm.conf
	sed -i 's@^;emergency_restart_threshold.*@emergency_restart_threshold=30@' $(1)/opt/etc/php7-fpm.conf
	sed -i 's@^;emergency_restart_interval.*@emergency_restart_interval=60s@' $(1)/opt/etc/php7-fpm.conf
	sed -i 's@^;process_control_timeout.*@process_control_timeout=10s@' $(1)/opt/etc/php7-fpm.conf
	sed -i 's@^; process.max.*@process.max=16@' $(1)/opt/etc/php7-fpm.conf
	sed -i 's@php-fpm@php7-fpm@' $(1)/opt/etc/php7-fpm.conf

	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/sapi/fpm/init.d.php-fpm $(1)/opt/etc/init.d/S86php7-fpm
	sed -i 's@php-fpm@php7-fpm@' $(1)/opt/etc/init.d/S86php7-fpm

	$(INSTALL_DIR) $(1)/opt/etc/php7-fpm.d
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/sapi/fpm/www.conf $(1)/opt/etc/php7-fpm.d/
	sed -i 's@^listen.*@listen=/dev/shm/php7-fpm.sock@' $(1)/opt/etc/php7-fpm.d/www.conf
	sed -i 's@^;listen.mode.*@listen.mode=0666@' $(1)/opt/etc/php7-fpm.d/www.conf
	sed -i 's@^;listen.allowed_clients.*@listen.allowed_clients=127.0.0.1@' $(1)/opt/etc/php7-fpm.d/www.conf
	sed -i 's@^pm.max_children.*@pm.max_children=3@' $(1)/opt/etc/php7-fpm.d/www.conf
	sed -i 's@^;pm.max_requests.*@pm.max_requests=2048@' $(1)/opt/etc/php7-fpm.d/www.conf
	sed -i 's@^;request_terminate_timeout.*@request_terminate_timeout=120s@' $(1)/opt/etc/php7-fpm.d/www.conf
	sed -i 's@^;env\[TMP\].*@env\[TMP\]=/tmp@' $(1)/opt/etc/php7-fpm.d/www.conf
	sed -i 's@^;env\[TMPDIR\].*@env\[TMPDIR\]=/tmp@' $(1)/opt/etc/php7-fpm.d/www.conf
	sed -i 's@^;env\[TEMP\].*@env\[TEMP\]=/tmp@' $(1)/opt/etc/php7-fpm.d/www.conf
	sed -i 's@php-fpm@php7-fpm@' $(1)/opt/etc/php7-fpm.d/www.conf

	$(INSTALL_DIR) $(1)/opt/share/www/www
	echo "<?php phpinfo(); ?>" > $(1)/opt/share/www/www/phpinfo.php
endef

define Package/php7-dbg/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_BUILD_DIR)/sapi/phpdbg/phpdbg $(1)/opt/bin/
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	( cd $(PKG_BUILD_DIR); touch configure.in; ./buildconf --force )
endef

define Build/InstallDev
	mkdir -p $(PKG_BUILD_DIR)/staging/opt/bin
	make -C $(PKG_BUILD_DIR) install INSTALL_ROOT=$(PKG_BUILD_DIR)/staging
	rm -f $(PKG_BUILD_DIR)/staging/opt/bin/php
	$(CP) $(PKG_BUILD_DIR)/staging/* $(STAGING_DIR_HOST)
	sed -i -e "s#prefix='/opt'#prefix='$(STAGING_DIR_HOST)/opt'#" $(STAGING_DIR_HOST)/opt/bin/phpize
	sed -i -e "s#exec_prefix=\"\`eval echo /opt\`\"#exec_prefix='$(STAGING_DIR_HOST)/opt'#" $(STAGING_DIR_HOST)/opt/bin/phpize
	sed -i -e "s#prefix=\"/opt\"#prefix=\"$(STAGING_DIR_HOST)/opt\"#" $(STAGING_DIR_HOST)/opt/bin/php-config
endef

define BuildModule
	# DEBUG: BuildModule $(1) $(2) $(3)
  define Package/php7-mod-$(1)
	$(call Package/php7/Default)

    ifneq ($(3),)
      DEPENDS+=$(3)
    endif

    TITLE:=$(2) shared module
  endef

  define Package/php7-mod-$(1)/install
	# DEBUG: BuildModule install
	$(INSTALL_DIR) $$(1)/opt/lib/php
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/modules/$(subst -,_,$(1)).so $$(1)/opt/lib/php/
	$(INSTALL_DIR) $$(1)/opt/etc/php7
    ifeq ($(4),zend)
	  echo "zend_extension=/opt/lib/php/$(subst -,_,$(1)).so" > $$(1)/opt/etc/php7/$(subst -,_,$(1)).ini
    else
	  echo "extension=$(subst -,_,$(1)).so" > $$(1)/opt/etc/php7/$(subst -,_,$(1)).ini
    endif
  endef

  $$(eval $$(call BuildPackage,php7-mod-$(1)))

endef

$(eval $(call BuildPackage,php7))
$(eval $(call BuildPackage,php7-cgi))
$(eval $(call BuildPackage,php7-cli))
$(eval $(call BuildPackage,php7-fastcgi))
$(eval $(call BuildPackage,php7-fpm))
$(eval $(call BuildPackage,php7-dbg))

#$(eval $(call BuildModule,NAME,TITLE[,PKG DEPENDS]))
$(eval $(call BuildModule,bcmath,bc style precision math functions))
$(eval $(call BuildModule,bz2,BZip2 support,+PACKAGE_php7-mod-bz2:libbz2))
$(eval $(call BuildModule,calendar,Calendar))
$(eval $(call BuildModule,ctype,Ctype))
$(eval $(call BuildModule,curl,cURL,+PACKAGE_php7-mod-curl:libcurl))
$(eval $(call BuildModule,dom,DOM,+@PHP7_LIBXML +PACKAGE_php7-mod-dom:libxml2))
$(eval $(call BuildModule,exif,EXIF))
$(eval $(call BuildModule,fileinfo,Fileinfo))
$(eval $(call BuildModule,ftp,FTP,+PACKAGE_php7-mod-ftp:libopenssl))
$(eval $(call BuildModule,gd,GD graphics,+PACKAGE_php7-mod-gd:libjpeg +PACKAGE_php7-mod-gd:libpng +PACKAGE_php7-mod-gd:libfreetype))
$(eval $(call BuildModule,gettext,Gettext,+PACKAGE_php7-mod-gettext:libintl-full))
$(eval $(call BuildModule,gmp,GMP,+PACKAGE_php7-mod-gmp:libgmp))
$(eval $(call BuildModule,hash,Hash))
$(eval $(call BuildModule,iconv,iConv,$(ICONV_DEPENDS)))
$(eval $(call BuildModule,imap,IMAP,+PACKAGE_php7-mod-imap:libc-client +PACKAGE_php7-mod-imap:libext2fs +PACKAGE_php7-mod-imap:libopenssl))
$(eval $(call BuildModule,json,JSON))
$(eval $(call BuildModule,ldap,LDAP,+PACKAGE_php7-mod-ldap:libopenldap +PACKAGE_php7-mod-ldap:libsasl2))
$(eval $(call BuildModule,mbstring,MBString))
$(eval $(call BuildModule,mcrypt,Mcrypt,+PACKAGE_php7-mod-mcrypt:libmcrypt +PACKAGE_php7-mod-mcrypt:libltdl))
$(eval $(call BuildModule,mysqlnd,a replacement for libmysqlclient))
$(eval $(call BuildModule,mysqli,MySQL Improved Extension,+PACKAGE_php7-mod-mysqlnd:libmysqlclient))
$(eval $(call BuildModule,opcache,OPcache,,zend))
$(eval $(call BuildModule,openssl,OpenSSL,+PACKAGE_php7-mod-openssl:libopenssl +PACKAGE_php7-mod-openssl:krb5-libs +PACKAGE_php7-mod-openssl:libext2fs))
$(eval $(call BuildModule,pcntl,PCNTL))
$(eval $(call BuildModule,pdo,PHP Data Objects))
$(eval $(call BuildModule,pdo-mysql,PDO driver for MySQL,+php7-mod-pdo +PACKAGE_php7-mod-pdo-mysql:libmysqlclient))
$(eval $(call BuildModule,pdo-pgsql,PDO driver for PostgreSQL,+php7-mod-pdo +PACKAGE_php7-mod-pdo-pgsql:libpq))
$(eval $(call BuildModule,pdo-sqlite,PDO driver for SQLite 3.x,+php7-mod-pdo +PACKAGE_php7-mod-pdo-sqlite:libsqlite3 +PACKAGE_php7-mod-pdo-sqlite:librt))
$(eval $(call BuildModule,pgsql,PostgreSQL,+PACKAGE_php7-mod-pgsql:libpq))
$(eval $(call BuildModule,phar,PHP Archive,+PACKAGE_php7-mod-phar:libopenssl +PACKAGE_php7-mod-phar:zlib +PACKAGE_php7-mod-phar:libbz2))
$(eval $(call BuildModule,readline,readline,+PACKAGE_php7-mod-readline:libreadline))
$(eval $(call BuildModule,session,Session))
$(eval $(call BuildModule,shmop,Shared Memory))
$(eval $(call BuildModule,simplexml,SimpleXML,+@PHP7_LIBXML +PACKAGE_php7-mod-simplexml:libxml2))
$(eval $(call BuildModule,soap,SOAP,+@PHP7_LIBXML +PACKAGE_php7-mod-soap:libxml2))
$(eval $(call BuildModule,sockets,Sockets))
$(eval $(call BuildModule,sqlite3,SQLite3,+PACKAGE_php7-mod-sqlite3:libsqlite3))
$(eval $(call BuildModule,sysvmsg,System V messages))
$(eval $(call BuildModule,sysvsem,System V shared memory))
$(eval $(call BuildModule,sysvshm,System V semaphore))
$(eval $(call BuildModule,tokenizer,Tokenizer))
$(eval $(call BuildModule,xml,XML,+PHP7_LIBXML:libxml2 +!PHP7_LIBXML:libexpat))
$(eval $(call BuildModule,xmlreader,XMLReader,+@PHP7_LIBXML +PACKAGE_php7-mod-xmlreader:libxml2))
$(eval $(call BuildModule,xmlwriter,XMLWriter,+@PHP7_LIBXML +PACKAGE_php7-mod-xmlwriter:libxml2))
$(eval $(call BuildModule,zip,ZIP,+PACKAGE_php7-mod-zip:zlib))
