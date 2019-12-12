#
# Copyright (C) 2017 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

# Warning by default OpenWrt does not have a root password which is necessery for NETCONF server.

include $(TOPDIR)/rules.mk

PKG_NAME:=Netopeer2
PKG_VERSION:=1.0.11
PKG_RELEASE:=4

PKG_LICENSE:=BSD-3-Clause
PKG_MAINTAINER:=Luka Paulic <luka.paulic@sartura.hr>

#PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
#PKG_SOURCE_URL:=http://192.168.110.14:7777/tmp/
#PKG_HASH:=e74d8002b252fa110eef32aff7ad51c7dda918ff92092f23866fe7004c1f1df9

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git@github.com:CESNET/Netopeer2.git
PKG_SOURCE_VERSION:=b18f506107ac0627c159529149414a3c3965a03d

CMAKE_INSTALL:=1

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/netopeer2-server
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=NETCONF server
  URL:=$(PKG_SOURCE_URL)
  DEPENDS:=+libcurl +libpthread +libyang +libnetconf2 +libsysrepo +sysrepocfg +sysrepoctl
  MENU:=1
endef

define Package/netopeer2-cli
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Netopeer2 cli tool
  URL:=$(PKG_SOURCE_URL)
  DEPENDS:=+libpthread +libyang +libnetconf2 +libopenssl
endef

define Package/Netopeer2/description
 Netopeer2 is a set of tools implementing network configuration tools based on the NETCONF
 Protocol. This is the second generation of the toolset, originally available as the Netopeer
 project. Netopeer2 is based on the new generation of the NETCONF and YANG libraries -
 libyang and libnetconf2. The Netopeer server uses sysrepo as a NETCONF datastore implementation.
endef

CMAKE_OPTIONS += \
	-DCMAKE_INSTALL_PREFIX:PATH=/usr \
	-DCMAKE_BUILD_TYPE:STRING=Release \
	-DINSTALL_MODULES:BOOL=OFF \
	-DGENERATE_HOSTKEY:BOOL=OFF \
	-DMERGE_LISTEN_CONFIG:BOOL=OFF \

define Package/netopeer2-server/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/server/netopeer2-server $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_DIR) $(1)/etc/Netopeer2/modules
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/ietf-netconf-acm@2018-02-14.yang $(1)/etc/Netopeer2/modules/ietf-netconf-acm@2018-02-14.yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/ietf-netconf@2013-09-29.yang $(1)/etc/Netopeer2/modules/ietf-netconf@2013-09-29.yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/ietf-netconf-monitoring@2010-10-04.yang $(1)/etc/Netopeer2/modules/ietf-netconf-monitoring@2010-10-04.yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/ietf-datastores@2017-08-17.yang  $(1)/etc/Netopeer2/modules/ietf-datastores@2017-08-17.yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/ietf-netconf-nmda@2019-01-07.yang $(1)/etc/Netopeer2/modules/ietf-netconf-nmda@2019-01-07.yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/notifications@2008-07-14.yang $(1)/etc/Netopeer2/modules/notifications@2008-07-14.yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/nc-notifications@2008-07-14.yang $(1)/etc/Netopeer2/modules/nc-notifications@2008-07-14.yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/ietf-x509-cert-to-name@2014-12-10.yang $(1)/etc/Netopeer2/modules/ietf-x509-cert-to-name@2014-12-10.yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/ietf-crypto-types@2019-07-02.yang $(1)/etc/Netopeer2/modules/ietf-crypto-types@2019-07-02.yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/ietf-keystore@2019-07-02.yang $(1)/etc/Netopeer2/modules/ietf-keystore@2019-07-02.yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/ietf-truststore@2019-07-02.yang $(1)/etc/Netopeer2/modules/ietf-truststore@2019-07-02.yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/ietf-tcp-common@2019-07-02.yang $(1)/etc/Netopeer2/modules/ietf-tcp-common@2019-07-02.yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/ietf-tcp-client@2019-07-02.yang $(1)/etc/Netopeer2/modules/ietf-tcp-client@2019-07-02.yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/ietf-tcp-server@2019-07-02.yang $(1)/etc/Netopeer2/modules/ietf-tcp-server@2019-07-02.yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/iana-crypt-hash@2014-08-06.yang $(1)/etc/Netopeer2/modules/iana-crypt-hash@2014-08-06.yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/ietf-ssh-server@2019-07-02.yang $(1)/etc/Netopeer2/modules/ietf-ssh-server@2019-07-02.yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/ietf-ssh-common@2019-07-02.yang $(1)/etc/Netopeer2/modules/ietf-ssh-common@2019-07-02.yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/ietf-tls-common@2019-07-02.yang $(1)/etc/Netopeer2/modules/ietf-tls-common@2019-07-02.yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/ietf-tls-server@2019-07-02.yang $(1)/etc/Netopeer2/modules/ietf-tls-server@2019-07-02.yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/ietf-netconf-server@2019-07-02.yang $(1)/etc/Netopeer2/modules/ietf-netconf-server@2019-07-02.yang

	$(INSTALL_DIR) $(1)/etc/Netopeer2/scripts
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/server/setup.sh $(1)/etc/Netopeer2/scripts/setup.sh
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/server/merge_hostkey.sh $(1)/etc/Netopeer2/scripts/merge_hostkey.sh
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/server/merge_config.sh $(1)/etc/Netopeer2/scripts/merge_config.sh

	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/netopeer2-server.default $(1)/etc/uci-defaults/98_netopeer2-server

	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_BIN) ./files/netopeer2-server.init $(1)/etc/init.d/netopeer2-server
endef

define Package/netopeer2-cli/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/cli/netopeer2-cli $(1)/usr/bin/
endef

$(eval $(call BuildPackage,netopeer2-server))
$(eval $(call BuildPackage,netopeer2-cli))
