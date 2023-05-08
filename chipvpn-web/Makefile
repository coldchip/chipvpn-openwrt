#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=chipvpn-web
PKG_RELEASE:=4

include $(INCLUDE_DIR)/package.mk

PKG_MAINTAINER:=Ryan Loh <ryan@coldchip.ru>

define Package/chipvpn-web
	SECTION:=net
	CATEGORY:=ChipVPN OS
	TITLE:=ChipVPN Web
	URL:=https://coldchip.ru
	DEPENDS+=+chipvpn +nginx
endef

define Package/chipvpn-web/description
	ChipVPN Web
endef

define Build/Compile
	
endef

define Package/chipvpn-web/install
	$(INSTALL_DIR) $(1)/www/
	$(CP) -r $(PKG_BUILD_DIR)/bin/* $(1)/www/
endef

$(eval $(call BuildPackage,chipvpn-web))
