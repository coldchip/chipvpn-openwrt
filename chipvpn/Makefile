#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=chipvpn
PKG_VERSION:=0.1
PKG_RELEASE:=1

PKG_SOURCE_URL=https://github.com/coldchip/chipvpn-udp.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=main
PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

PKG_MAINTAINER:=Ryan Loh <ryan@chip.sg>

define Package/$(PKG_NAME)
	SECTION:=net
	CATEGORY:=ChipVPN OS
	TITLE:=ChipVPN Binary
	URL:=https://chip.sg
	DEPENDS+=+kmod-tun +libsodium
endef

define Package/$(PKG_NAME)/description
	ChipVPN Binary
endef

define Build/Configure
	$(call Build/Configure/Default,--with-linux-headers=$(LINUX_DIR))
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC="$(TARGET_CC)" \
		CFLAGS="$(TARGET_CFLAGS)" \
		LDFLAGS="$(TARGET_LDFLAGS)" \
		OUTPUT="$(PKG_BUILD_DIR)/chipvpn"
endef

define Package/$(PKG_NAME)/conffiles
	/etc/chipvpn/chipvpn.ini
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/etc/init.d $(1)/etc/chipvpn/ $(1)/usr/sbin/

	$(INSTALL_BIN) ./files/chipvpn.init $(1)/etc/init.d/chipvpn

	$(INSTALL_CONF) $(PKG_BUILD_DIR)/client.ini $(1)/etc/chipvpn/chipvpn.ini
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/route.sh $(1)/etc/chipvpn/route.sh

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/chipvpn $(1)/usr/sbin
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
