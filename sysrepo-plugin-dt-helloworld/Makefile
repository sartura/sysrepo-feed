#
# Copyright (C) 2006-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=sysrepo-plugin-dt-helloworld
PKG_VERSION:=1.0

PKG_LICENSE:=GPL-2.0+
PKG_MAINTAINER:=Antonio Paunovic <antonio.paunovic@sartura.hr>

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=cfdd28225ca2529a8a46053a663c17a58875e8b5
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/sartura/sysrepo-plugin-helloworld
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)

CMAKE_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/sysrepo-plugin-dt-helloworld/description
  sysrepo-plugin-dt-helloworld is a plugin daemon for sysrepo datastore. It can be used to manipulate example UCI configuration.
endef

define Package/sysrepo-plugin-dt-helloworld
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+sysrepoctl +sysrepocfg +sysrepo +libuci
  TITLE:=sysrepo-plugin-dt-helloworld
endef

define Package/sysrepo-plugin-dt-helloworld/install
	$(INSTALL_DIR) $(1)/usr/lib/sysrepo/plugins
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/sysrepo-plugin-dt-helloworld.so $(1)/usr/lib/sysrepo/plugins

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/yang/helloworld@2017-06-07.yang $(1)/etc/sysrepo/yang

	$(INSTALL_DIR) $(1)/etc/config/
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/uci_example/helloworld $(1)/etc/config

	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/helloworld.default $(1)/etc/uci-defaults/helloworld.default
endef

$(eval $(call BuildPackage,sysrepo-plugin-dt-helloworld))
