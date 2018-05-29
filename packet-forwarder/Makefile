#
# Copyright (C) 2018 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=packet-forwarder
PKG_VERSION:=4.0.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Lora-net/packet_forwarder
PKG_SOURCE_VERSION:=d0226eae6e7b6bbaec6117d0d2372bf17819c438
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_CAT:=zcat
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_CONFIG_DEPENDS:=CONFIG_PACKAGE_libloragw

include $(INCLUDE_DIR)/package.mk

define Package/packet-forwarder
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Routing and Redirection
  TITLE:=Lora network packet forwarder
  DEPENDS:= +libloragw +librt +libm +libpthread
  URL:=https://github.com/Lora-net
  MAINTAINER:=Anton Glukhov <anton.a.glukhov@gmail.com>
endef

define Package/packet-forwarder/description
  A LoRa packet forwarder is a program running on the host of a LoRa gateway
  that forwards RF packets receive by the concentrator to a server through a
  IP/UDP link, and emits RF packets that are sent by the server.
endef

TARGET_CFLAGS += $(FPIC) -Iinc -std=c99 -I.
TARGET_LGW_PATH = $(BUILD_DIR)/libloragw
EXTRA_CFLAGS += -DLGW_PATH=$(BUILD_DIR)/libloragw

PACKET_FORWARDER_MAKEOPTS= -C $(PKG_BUILD_DIR) \
	LGW_PATH="$(PKG_BUILD_DIR)/libloragw"

MAKE_FLAGS = GW_PATH="$(PKG_BUILD_DIR)/libloragw"

define Package/packet-forwarder/install
	$(INSTALL_DIR) $(1)/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/packet-forwarder/lora_pkt_fwd $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/packaet_forwarder.init $(1)/etc/init.d/packet_porwarder
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DATA) ./files/global_conf.json $(1)/etc/global_conf.json
endef

$(eval $(call BuildPackage,packet-forwarder))
