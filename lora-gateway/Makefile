#
# Copyright (C) 2018 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libloragw
PKG_VERSION:=v5.0.1
PKG_RELEASE:=1
PKG_LICENSE:=BSD

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Lora-net/lora_gateway
PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_SOURCE_VERSION:=a955619271b5d0a46d32e08150acfbc1eed183b7
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_CAT:=zcat
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/libloragw
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=LoRa Gateway Driver/HAL library
  DEPENDS:= +librt +libm
  URL:=https://github.com/Lora-net
  MAINTAINER:=Anton Glukhov <anton.a.glukhov@gmail.com>
endef

define Package/description
  Driver/HAL to build a gateway using a concentrator board
  based on Semtech SX1301 multi-channel modem and SX1257/SX1255 RF transceivers.
endef

TARGET_CFLAGS += $(FPIC) -Iinc -std=c99 -I.

define Package/libloragw/install
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/libloragw
	$(CP) $(PKG_BUILD_DIR)/libloragw/inc/* $(1)/usr/include/libloragw
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/libloragw/libloragw.a $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libloragw))
