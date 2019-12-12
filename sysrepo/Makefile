#
# Copyright (C) 2017 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_LICENSE:=ASL-2.0
PKG_MAINTAINER:=Luka Paulic <luka.paulic@sartura.hr>

PKG_NAME:=sysrepo
PKG_VERSION:=1.3.20
PKG_RELEASE:=4

#PKG_SOURCE:=${PKG_NAME}-${PKG_VERSION}.tar.gz
#PKG_SOURCE_URL:=http://192.168.110.14:7777/tmp/
#PKG_HASH:=5dd40a49e14412059e747762244c8800c91aec74237d86ff51e08fb0b9db3868

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/sysrepo/sysrepo.git
PKG_SOURCE_VERSION:=d5f9d633409e1bbe6de65930fad51248e4744b01

CMAKE_INSTALL:=1

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/libsysrepo
  SECTION:=utils
  CATEGORY:=Utilities
  URL:=$(PKG_SOURCE_URL)
  TITLE:=YANG-based data store library
  DEPENDS:=+libyang +libpthread
  MENU:=1
endef

define Package/sysrepoctl
  SECTION:=utils
  CATEGORY:=Utilities
  URL:=$(PKG_SOURCE_URL)
  TITLE:=sysrepo cli tool
  DEPENDS:=+libsysrepo
endef

define Package/sysrepocfg
  SECTION:=utils
  CATEGORY:=Utilities
  URL:=$(PKG_SOURCE_URL)
  TITLE:=sysrepo configuration tool
  DEPENDS:=+libsysrepo
endef

define Package/sysrepo/description
Sysrepo is an YANG-based configuration and operational state data store for Unix/Linux applications.
endef

CMAKE_OPTIONS += \
	-DCMAKE_BUILD_TYPE:STRING=Release \
	-DREPO_PATH:PATH=/etc/sysrepo \
	-DCMAKE_INSTALL_PREFIX:PATH=/usr \

define Package/libsysrepo/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libsysrepo.so* $(1)/usr/lib/

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/ietf-netconf-notifications.yang $(1)/etc/sysrepo/yang/ietf-netconf-notifications@2012-02-06.yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/ietf-netconf-with-defaults.yang $(1)/etc/sysrepo/yang/ietf-netconf-with-defaults@2011-06-01.yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/ietf-netconf.yang $(1)/etc/sysrepo/yang/ietf-netconf@2011-06-01.yang

	$(INSTALL_DIR) $(1)/etc/sysrepo/data
#
#	$(INSTALL_DIR) $(1)/etc/uci-defaults
#	$(INSTALL_BIN) ./files/libsysrepo.default $(1)/etc/uci-defaults/95_libsysrepo

	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/sysrepo-plugind $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_BIN) ./files/sysrepo.init $(1)/etc/init.d/sysrepo

	$(INSTALL_DIR) $(1)/usr/lib/sysrepo/plugins
endef

define Package/sysrepoctl/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/sysrepoctl $(1)/usr/bin/
endef

define Package/sysrepocfg/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/sysrepocfg $(1)/usr/bin/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libsysrepo.so* $(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/libsysrepo.pc $(1)/usr/lib/pkgconfig/

	$(INSTALL_DIR) $(1)/usr/include/sysrepo
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include
endef

$(eval $(call BuildPackage,libsysrepo))
$(eval $(call BuildPackage,sysrepoctl))
$(eval $(call BuildPackage,sysrepocfg))
