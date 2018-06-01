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
PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_CAT:=zcat
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

PKG_CONFIG_DEPENDS:=CONFIG_PACKAGE_libloragw

include $(INCLUDE_DIR)/package.mk

define Package/packet-forwarder
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Routing and Redirection
  TITLE:=Lora network packet forwarder
  DEPENDS:= +librt +libpthread
  URL:=https://github.com/Lora-net
  MAINTAINER:=Anton Glukhov <anton.a.glukhov@gmail.com>
endef

define Package/packet-forwarder/description
  A LoRa packet forwarder is a program running on the host of a LoRa gateway
  that forwards RF packets receive by the concentrator to a server through a
  IP/UDP link, and emits RF packets that are sent by the server.
endef

TARGET_CFLAGS += $(FPIC) -Iinc -std=c99 -I.

MAKE_FLAGS += LGW_PATH="$(BUILD_DIR)/libloragw/libloragw" \
		CROSS_COMPILE="$(TARGET_CROSS)" \
		ARCH="$(ARCH)"

define Package/packet-forwarder/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lora_pkt_fwd/lora_pkt_fwd $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/etc/init.d/lora_pkt_fwd.init $(1)/etc/init.d/lora_pkt_fwd
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/lora_pkt_fwd/global_conf.json $(1)/etc/global_conf.json
endef

$(eval $(call BuildPackage,packet-forwarder))
